---
ms.assetid: f775cbda-a75d-439d-9aa7-82f3bc8dc932
title: Verbundserverfarm mit WID
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b0a84940018a0e71aaa1b47c7af3aba5966fe0ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408055"
---
# <a name="federation-server-farm-using-wid"></a>Verbundserverfarm mit WID

Die Standard Topologie für Active Directory-Verbunddienste (AD FS) \(AD FS\) ist eine Verbund Serverfarm, die die interne Windows-Datenbank \(wid\)verwendet. In dieser Topologie verwendet AD FS wid als Speicher für die AD FS Konfigurations Datenbank für alle Verbund Server, die mit dieser Farm verknüpft sind. Die Verbunddienstdaten in der Konfigurationsdatenbank werden von der Farm auf alle Server der Farm repliziert und dort verwaltet. AD FS in Windows Server 2012 R2 ermöglicht es Organisationen mit 100 oder weniger Vertrauens Stellungen der vertrauenden Seite, Verbund Server Farmen mithilfe von wid mit bis zu 30 Servern zu konfigurieren.  
  
Beim Erstellen des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt. Wenn Sie wid für die AD FS Konfigurations Datenbank verwenden, wird der erste Verbund Server, den Sie in der Farm erstellen, als *primärer Verbund Server*bezeichnet. Dies bedeutet, dass dieser Computer mit einer Lese\/Schreib Kopie der AD FS Konfigurations Datenbank konfiguriert ist.  
  
Alle anderen für diese Farm konfigurierten Verbund Server werden als *sekundäre* Verbund Server bezeichnet, da Sie alle Änderungen, die auf dem primären Verbund Server vorgenommen werden, an den Lese\-nur Kopien der AD FS Konfigurations Datenbank replizieren müssen, die Sie lokal speichern.  
  
> [!IMPORTANT]  
> Es wird empfohlen, mindestens zwei Verbund Server in einer Konfiguration mit Lasten\-ausgeglichen zu verwenden.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit 100 oder weniger konfigurierten Vertrauens Stellungen, die ihre internen Benutzer bereitstellen müssen, \(bei Computern angemeldet, die physisch mit dem Unternehmensnetzwerk verbunden sind\) mit einmaligem\-anmelden \(SSO\) Zugriff auf Verbund Anwendungen oder-Dienste.  
  
-   Organisationen, die ihren internen Benutzern SSO-Zugriff auf Microsoft Online Services oder Microsoft Office 365 bereitstellen möchten  
  
-   Kleinere Unternehmen, die redundante, skalierbare Dienste benötigen  
  
> [!NOTE]  
> Organisationen mit größeren Datenbanken sollten die Verwendung der Verbund [Server Farm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Bereitstellungs Topologie in Erwägung gezogen werden. Organisationen mit Benutzern, die sich von außerhalb des Netzwerks anmelden, sollten entweder die Verbund [Serverfarm mithilfe der wid-und](Federation-Server-Farm-Using-WID-and-Proxies.md) Proxys-Topologie oder der Verbund [Serverfarm mithilfe SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Topologie verwenden.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Ermöglicht SSO-Zugriff auf interne Benutzer.  
  
-   Die Daten-und Verbunddienst Redundanz \(jeden Verbund Server repliziert Änderungen an anderen Verbund Servern in derselben Farm\)  
  
-   WID ist in Windows enthalten. Daher ist es nicht erforderlich, SQL Server zu erwerben.  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Eine wid-Farm hat ein Limit von 30 Verbund Servern, wenn Sie über 100 oder weniger Vertrauens Stellungen der vertrauenden Seite verfügen.  
  
-   Eine wid-Farm unterstützt keine Erkennung von tokenwiederholungen oder artefaktauflösung \(Teil der Security Assertion Markup Language \(SAML-\) Protokoll\).  
  
In der folgenden Tabelle finden Sie eine Zusammenfassung zur Verwendung einer wid-Farm.  Verwenden Sie es, um Ihre Implementierung zu planen.  
  
|| 1 \- 100 RP-Vertrauens Stellungen | Mehr als 100 RP-Vertrauens Stellungen |
| --- | --- | --- |
|1 \- 30 AD FS Knoten|Unterstützt wid|Nicht unterstützt mit wid-SQL erforderlich 
|Mehr als 30 AD FS Knoten|Nicht unterstützt mit wid-SQL erforderlich|Nicht unterstützt mit wid-SQL erforderlich  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Wenn Sie bereit sind, mit der Bereitstellung dieser Topologie in Ihrem Netzwerk zu beginnen, sollten Sie planen, alle Verbund Server im Unternehmensnetzwerk hinter einem Netzwerk Lastenausgleich \(NLB-\) Host zu platzieren, der für einen NLB-Cluster mit einem dedizierten Cluster Domain Name System \(DNS-\) Namen und die IP-Adresse des Clusters konfiguriert werden kann.  
  
> [!NOTE]  
> Der DNS-Cluster Name muss mit dem Verbunddienst Namen, z. b. fs.fabrikam.com, identisch sein.  
  
Der NLB-Host kann die in diesem NLB-Cluster definierten Einstellungen verwenden, um Client Anforderungen den einzelnen Verbund Servern zuzuordnen. In der folgenden Abbildung wird gezeigt, wie das fiktive Unternehmen Fabrikam, Inc., die erste Phase der Bereitstellung mithilfe einer zwei\-Computer-Verbund Serverfarm \(FS1 und FS2\) mit wid und die Positionierung eines DNS-Servers und eines einzelnen NLB-Hosts, der mit dem Unternehmensnetzwerk verdrahtet ist, festlegt.  
  
![Serverfarm mit wid](media/FarmWID.gif)  
  
> [!NOTE]  
> Bei einem Ausfall dieses einzelnen NLB-Hosts können die Benutzer nicht auf Verbund Anwendungen oder-Dienste zugreifen. Fügen Sie weitere NLB-Hosts hinzu, wenn Ihre Geschäftsanforderungen eine einzelne Fehlerquelle nicht zulassen.  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern finden Sie im Abschnitt Anforderungen für die Namensauflösung unter [AD FS Anforderungen](AD-FS-Requirements.md).  
  
## <a name="see-also"></a>Weitere Informationen  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

