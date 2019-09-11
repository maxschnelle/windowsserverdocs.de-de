---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: Verbundserverfarm mit WID
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2298ba360bb59c950a78514d137c0b4d5fbdd1af
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867814"
---
# <a name="federation-server-farm-using-wid"></a>Verbundserverfarm mit WID

Die Standard Topologie für Active Directory-Verbunddienste (AD FS) \(AD FS\) ist eine Verbund Serverfarm, die die interne Windows- \(Datenbank\)-wid verwendet, die aus bis zu fünf Verbund Servern besteht, auf denen Ihre die Verbunddienst der Organisation. In dieser Topologie verwendet AD FS wid als Speicher für die AD FS Konfigurations Datenbank für alle Verbund Server, die mit dieser Farm verknüpft sind. Die Verbunddienstdaten in der Konfigurationsdatenbank werden von der Farm auf alle Server der Farm repliziert und dort verwaltet.  
  
Beim Erstellen des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt. Wenn Sie wid für die AD FS Konfigurations Datenbank verwenden, wird der erste Verbund Server, den Sie in der Farm erstellen, als *primärer Verbund Server*bezeichnet. Dies bedeutet, dass dieser Computer mit einer Lese\/-/Schreibkopie der AD FS Konfigurations Datenbank konfiguriert ist.  
  
Alle anderen für diese Farm konfigurierten Verbund Server werden als *sekundäre* Verbund Server bezeichnet, da Sie alle auf dem primären Verbund Server vorgenommenen Änderungen auf die\-schreibgeschützten Kopien der AD FS replizieren müssen. die Konfigurations Datenbank, die lokal gespeichert wird.  
  
> [!NOTE]  
> Es wird empfohlen, mindestens zwei Verbund Server in einer Konfiguration mit Lasten\-Ausgleich zu verwenden.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die ihre internen Benutzer \(für Computer, die physisch mit dem Unternehmensnetzwerk\) verbunden sind, mit einmaligem Anmelden\- \(bereitstellenmüssenSSO\) -Zugriff auf Verbund Anwendungen oder-Dienste  
  
-   Organisationen, die ihren internen Benutzern SSO-Zugriff auf Microsoft Online Services oder Microsoft Office 365 bereitstellen möchten  
  
-   Kleinere Unternehmen, die redundante, skalierbare Dienste benötigen  
  
> [!NOTE]  
> Organisationen mit größeren Datenbanken sollten die Verwendung der Verbund [Server Farm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Bereitstellungs Topologie in Erwägung gezogen werden, die weiter unten in diesem Abschnitt beschrieben wird. Organisationen mit Benutzern, die sich von außerhalb des Netzwerks anmelden, sollten entweder die Verbund [Serverfarm mithilfe der wid-und](Federation-Server-Farm-Using-WID-and-Proxies.md) Proxys-Topologie oder der Verbund [Serverfarm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Topologie verwenden.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Ermöglicht SSO-Zugriff auf interne Benutzer.  
  
-   Daten-und Verbunddienst \(Redundanz repliziert jeder Verbund Serveränderungen an anderen Verbund Servern in derselben Farm.\)  
  
-   Die Farm kann durch Hinzufügen von bis zu fünf Verbund Servern horizontal hochskaliert werden.  
  
-   WID ist in Windows enthalten. Daher ist es nicht erforderlich, SQL Server zu erwerben.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Für eine wid-Farm sind maximal fünf Verbund Server beschränkt. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md).  
  
-   Eine wid-Farm unterstützt keine tokenwiedergabe-oder \(artefaktauflösungs Teile \(des Security Assertion Markup Language\) SAML-Protokolls\).  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Wenn Sie bereit sind, mit der Bereitstellung dieser Topologie in Ihrem Netzwerk zu beginnen, sollten Sie planen, alle Verbund Server im Unternehmensnetzwerk hinter einem NLB \(\) -Host für den Netzwerk Lastenausgleich zu platzieren, der für einen NLB-Cluster konfiguriert werden kann. mit einem dedizierten Cluster \(Domain Name System\) DNS-Namen und einer Cluster-IP-Adresse.  
  
> [!NOTE]  
> Der DNS-Cluster Name muss mit dem Verbunddienst Namen, z. b. fs.fabrikam.com, identisch sein.  
  
Der NLB-Host kann die in diesem NLB-Cluster definierten Einstellungen verwenden, um Client Anforderungen den einzelnen Verbund Servern zuzuordnen. Die folgende Abbildung zeigt, wie das fiktive Fabrikam, Inc., Unternehmen die erste Phase der Bereitstellung mithilfe einer Verbund\-Serverfarm \(mit zwei Computern FS1 und\) FS2 mit wid und der Positionierung eines DNS-Servers einrichtet. und ein einzelner NLB-Host, der mit dem Unternehmensnetzwerk verdrahtet ist.  
  
![Serverfarm mit wid](media/FarmWID.gif)  
  
> [!NOTE]  
> Bei einem Ausfall dieses einzelnen NLB-Hosts können die Benutzer nicht auf Verbund Anwendungen oder-Dienste zugreifen. Fügen Sie weitere NLB-Hosts hinzu, wenn Ihre Geschäftsanforderungen eine einzelne Fehlerquelle nicht zulassen.  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern finden Sie im AD FS Entwurfs Handbuch unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) .  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
