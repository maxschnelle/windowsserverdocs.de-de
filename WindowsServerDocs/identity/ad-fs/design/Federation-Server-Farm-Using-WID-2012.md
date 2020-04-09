---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: Verbundserverfarm mit WID
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4704928213de4ed1ed71630fe6a49b54f2019af5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853113"
---
# <a name="federation-server-farm-using-wid"></a>Verbundserverfarm mit WID

Die Standard Topologie für Active Directory-Verbunddienste (AD FS) \(AD FS\) ist eine Verbund Serverfarm unter Verwendung der internen Windows-Datenbank \(wid\), die aus bis zu fünf Verbund Servern besteht, die das Verbunddienst Ihrer Organisation hosten. In dieser Topologie verwendet AD FS wid als Speicher für die AD FS Konfigurations Datenbank für alle Verbund Server, die mit dieser Farm verknüpft sind. Die Verbunddienstdaten in der Konfigurationsdatenbank werden von der Farm auf alle Server der Farm repliziert und dort verwaltet.  
  
Beim Erstellen des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt. Wenn Sie wid für die AD FS Konfigurations Datenbank verwenden, wird der erste Verbund Server, den Sie in der Farm erstellen, als *primärer Verbund Server*bezeichnet. Dies bedeutet, dass dieser Computer mit einer Lese\/Schreib Kopie der AD FS Konfigurations Datenbank konfiguriert ist.  
  
Alle anderen für diese Farm konfigurierten Verbund Server werden als *sekundäre* Verbund Server bezeichnet, da Sie alle Änderungen, die auf dem primären Verbund Server vorgenommen werden, an den Lese\-nur Kopien der AD FS Konfigurations Datenbank replizieren müssen, die Sie lokal speichern.  
  
> [!NOTE]  
> Es wird empfohlen, mindestens zwei Verbund Server in einer Konfiguration mit Lasten\-ausgeglichen zu verwenden.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die ihre internen Benutzer bereitstellen müssen, \(bei Computern angemeldet, die physisch mit dem Unternehmensnetzwerk verbunden sind\) mit einmaligem\-anmelden \(SSO\) Zugriff auf Verbund Anwendungen oder-Dienste.  
  
-   Organisationen, die ihren internen Benutzern SSO-Zugriff auf Microsoft Online Services oder Microsoft Office 365 bereitstellen möchten  
  
-   Kleinere Unternehmen, die redundante, skalierbare Dienste benötigen  
  
> [!NOTE]  
> Organisationen mit größeren Datenbanken sollten die Verwendung der Verbund [Server Farm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Bereitstellungs Topologie in Erwägung gezogen werden, die weiter unten in diesem Abschnitt beschrieben wird. Organisationen mit Benutzern, die sich von außerhalb des Netzwerks anmelden, sollten entweder die Verbund [Serverfarm mithilfe der wid-und](Federation-Server-Farm-Using-WID-and-Proxies.md) Proxys-Topologie oder der Verbund [Serverfarm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Topologie verwenden.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Ermöglicht SSO-Zugriff auf interne Benutzer.  
  
-   Die Daten-und Verbunddienst Redundanz \(jeden Verbund Server repliziert Änderungen an anderen Verbund Servern in derselben Farm\)  
  
-   Die Farm kann durch Hinzufügen von bis zu fünf Verbund Servern horizontal hochskaliert werden.  
  
-   WID ist in Windows enthalten. Daher ist es nicht erforderlich, SQL Server zu erwerben.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Für eine wid-Farm sind maximal fünf Verbund Server beschränkt. Weitere Informationen finden Sie unter [Überlegungen zur AD FS-Bereitstellungstopologie](AD-FS-Deployment-Topology-Considerations.md).  
  
-   Eine wid-Farm unterstützt keine Erkennung von tokenwiederholungen oder artefaktauflösung \(Teil der Security Assertion Markup Language \(SAML-\) Protokoll\).  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Wenn Sie bereit sind, mit der Bereitstellung dieser Topologie in Ihrem Netzwerk zu beginnen, sollten Sie planen, alle Verbund Server im Unternehmensnetzwerk hinter einem Netzwerk Lastenausgleich \(NLB-\) Host zu platzieren, der für einen NLB-Cluster mit einem dedizierten Cluster Domain Name System \(DNS-\) Namen und die IP-Adresse des Clusters konfiguriert werden kann.  
  
> [!NOTE]  
> Der DNS-Cluster Name muss mit dem Verbunddienst Namen, z. b. fs.fabrikam.com, identisch sein.  
  
Der NLB-Host kann die in diesem NLB-Cluster definierten Einstellungen verwenden, um Client Anforderungen den einzelnen Verbund Servern zuzuordnen. In der folgenden Abbildung wird gezeigt, wie das fiktive Unternehmen Fabrikam, Inc., die erste Phase der Bereitstellung mithilfe einer zwei\-Computer-Verbund Serverfarm \(FS1 und FS2\) mit wid und die Positionierung eines DNS-Servers und eines einzelnen NLB-Hosts, der mit dem Unternehmensnetzwerk verdrahtet ist, festlegt.  
  
![Serverfarm mit wid](media/FarmWID.gif)  
  
> [!NOTE]  
> Bei einem Ausfall dieses einzelnen NLB-Hosts können die Benutzer nicht auf Verbund Anwendungen oder-Dienste zugreifen. Fügen Sie weitere NLB-Hosts hinzu, wenn Ihre Geschäftsanforderungen eine einzelne Fehlerquelle nicht zulassen.  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern finden Sie im AD FS Entwurfs Handbuch unter [Anforderungen für die Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) .  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
