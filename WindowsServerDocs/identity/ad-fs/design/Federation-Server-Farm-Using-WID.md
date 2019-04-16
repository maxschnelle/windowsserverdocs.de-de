---
ms.assetid: f775cbda-a75d-439d-9aa7-82f3bc8dc932
title: Verbundserverfarm mit WID
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 41c2179cbd8bf2c6032f233335099b512c02f880
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="federation-server-farm-using-wid"></a>Verbundserverfarm mit WID

>Gilt für: Windows Server 2016, Windows Server2012 R2

Die Standardtopologie für Active Directory Federation Services \(AD FS\) ist eine Verbundserverfarm mithilfe der internen Windows-Datenbank \(WID\). In dieser Topologie verwendet AD FS WID als Speicher für die AD FS-Konfigurationsdatenbank für alle Verbundserver, die mit der betreffenden Farm verbunden sind. Die Farm repliziert und verwaltet die verbunddienstdaten in der Konfigurationsdatenbank auf alle Server in der Farm. AD FS unter Windows Server2012 R2 ermöglicht Organisationen mit bis zu 100 Vertrauensstellungen vertrauenden Seite Verbund-Serverfarmen mit WID mit bis zu 30 Server konfigurieren.  
  
Der Vorgang der Erstellung des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt. Bei der Verwendung von WID für die AD FS-Konfigurationsdatenbank des ersten Verbundservers, die Sie in der Farm erstellen genannt wird die *primärer Verbundserver*. Dies bedeutet, dass der Computer mit einer Lese-/Schreibkopie der AD FS-Konfigurationsdatenbank konfiguriert ist.  
  
Alle anderen Verbundserver, die Sie für diese Farm konfigurieren als bezeichnet *sekundäre Verbundserver*, da sie keine Änderungen replizieren müssen, die auf dem primären Verbundserver der schreibgeschützte Kopien der AD FS-Konfigurationsdatenbank vorgenommen werden, die sie lokal zu speichern.  
  
> [!IMPORTANT]  
> Wir empfehlen die Verwendung von mindestens zwei Verbundserver in einer Konfiguration mit Lastenausgleich Load\.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnittbeschreibt die verschiedenen Aspekte über die Zielgruppe, Vorteile und Einschränkungen, die dieser Bereitstellungstopologie zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Organisationen mit bis zu 100 konfigurierten Vertrauensstellungen, die die interne Benutzer bereitstellen müssen \ (angemeldet bei Computern, auf denen das Unternehmen vom Netzwerk physisch verbunden sind) mit einzelnen Standardparameter-\(SSO\) Zugriff auf verbundanwendungen oder -Dienste  
  
-   Organisationen, die die interne Benutzer SSO-Zugriff auf Microsoft Online Services oder Microsoft Office365 ermöglichen möchten  
  
-   Kleinere Organisationen, die redundante, skalierbare Dienste erfordern  
  
> [!NOTE]  
> Organisationen mit größeren Datenbanken sollten die [Federation Server Farm mithilfe von SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Bereitstellungstopologie. Organisationen mit Benutzern, die von außerhalb des Netzwerks anmelden sollten entweder mithilfe der [Verbundserver mit WID und Proxys](Federation-Server-Farm-Using-WID-and-Proxies.md) Topologie oder die [Federation Server Farm mithilfe von SQL Server](Federation-Server-Farm-Using-SQL-Server.md) Topologie.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Ermöglicht den SSO-Zugriff auf interne Benutzer  
  
-   Daten und Verbunddienst Redundanz \ (jeder Verbundserver repliziert Änderungen an andere Verbundserver in der gleichen Farm\)  
  
-   Interne Windows-Datenbank ist in Windows enthalten. aus diesem Grund müssen SQL Server erwerben  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Grenzen der Verwendung dieser Topologie?  
  
-   Ein Windows-datenbankfarm darf maximal 30 Verbundserver, besitzen Sie bis zu 100 Vertrauensstellungen vertrauenden Seite.  
  
-   Ein Windows-datenbankfarm unterstützt keine Erkennung oder Artefakt Auflösung von tokenwiederholungen \ (Teil der \(SAML\) protocol\ Security Assertion Markup Language).  
  
Die folgende Tabelle enthält eine Zusammenfassung für die Verwendung einer Windows-datenbankfarm.  Verwenden Sie, um die Planung der Implementierung.  
  
|| 1 \-100 RP-Vertrauensstellungen | Mehr als 100 RP-Vertrauensstellungen |
| --- | --- | --- |
|1 \-30-AD FS-Knoten|Interne Windows-Datenbank unterstützt|Bei Verwendung von WID - erforderlichen SQL nicht unterstützt 
|Mehr als 30 AD FS-Knoten|Bei Verwendung von WID - erforderlichen SQL nicht unterstützt|Bei Verwendung von WID - erforderlichen SQL nicht unterstützt  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Der Empfehlungen für die Platzierung und Netzwerk Layout Server  
Wenn Sie zum Bereitstellen dieser Topologie Ihres Netzwerks bereit sind, sollten Sie planen, zu platzieren alle Verbundserver im Unternehmensnetzwerk hinter einem Netzwerklastenausgleich \(NLB\)-Host, der für einen NLB-Cluster mit einer dedizierten Domain Name System \(DNS\)-Clusternamen und die Cluster-IP-Adresse konfiguriert werden kann.  
  
> [!NOTE]  
> Dieser DNS-Clustername muss den Namen des Verbunddiensts, z.B. fs.fabrikam.com übereinstimmen.  
  
Der NLB-Host können die Einstellungen, die in diesem NLB-Cluster auf Clientanforderungen an den einzelnen Verbundservern zugeordnet werden sollen. Die folgende Abbildungzeigt, wie der fiktive Unternehmen Fabrikam, Inc. die erste Phase der Bereitstellung einer Verbundserverfarm Two\-Computer mit einrichtet \(fs1 and fs2\) mit WID und die Position von einem DNS-Server und einem einzelnen NLB-Host, die mit dem Unternehmensnetzwerk verknüpft wird.  
  
![Server-Farm mit WID](media/FarmWID.gif)  
  
> [!NOTE]  
> Wenn ein Fehler auf dieses einzelnen NLB-Host vorhanden ist, werden Benutzer nicht auf verbundanwendungen oder -Dienste zugreifen. Fügen Sie weitere NLB-Hosts hinzu, wenn Ihre geschäftlichen Anforderungen müssen eine einzelne Fehlerquelle nicht zulassen.  
  
Weitere Informationen dazu, wie Sie die Netzwerkumgebung für die Verwendung mit Verbundserver konfigurieren, finden Sie im AbschnittNamensauflösungsanforderungen in [AD FS-Anforderungen](AD-FS-Requirements.md).  
  
## <a name="see-also"></a>Siehe auch  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

