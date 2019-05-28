---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: Verbundserverfarm mit SQL Server
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 66c8bae2fbccca2bf618e46ffd3ccc05cb52f911
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191505"
---
# <a name="federation-server-farm-using-sql-server"></a>Verbundserverfarm mit SQL Server

Diese Topologie wird für Active Directory Federation Services \(AD FS\) unterscheidet sich von der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Bereitstellungstopologie, werden sie nicht die Daten repliziert jedem Verbundserver in der Farm. Stattdessen können allen Verbundservern in der Farm lesen und Schreiben von Daten in einer allgemeinen Datenbank, die gespeichert werden, auf einem Server mit Microsoft SQL Server, die im Unternehmensnetzwerk befindet.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnitt beschreibt verschiedene Überlegungen zu den Zielgruppe, Vorteile und Einschränkungen, die mit dieser Bereitstellungstopologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Große Unternehmen mit mehr als 100 Vertrauensstellungen, die sowohl für ihre interne Benutzer und externe Benutzer mit Einmaliger Anmeldung bieten\-auf \(SSO\) Zugriff auf die verbundanwendung oder der Dienste  
  
-   Organisationen, die bereits SQL Server verwenden und ihre vorhandenen Tools und Kenntnisse maximal nutzen möchten  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Unterstützung für eine größere Anzahl von Vertrauensstellungen \(mehr als 100\)  
  
-   Unterstützung für die Erkennung einer tokenmehrfachverwendung \(eine Sicherheitsfunktion\) und artefaktauflösung \(Teil der Security Assertion Markup Language \(SAML\) 2.0-Protokolls\)  
  
-   Unterstützung für die Vorteile wie z. B. datenbankspiegelung, Failoverclustering, berichterstellung und Verwaltung von SQL Server-tools  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Einschränkungen bei der Verwendung dieser Topologie?  
  
-   Diese Topologie bietet standardmäßig keine datenbankredundanz. Obwohl eine Verbundserverfarm mit WID-Topologie automatisch die WID-Datenbank auf jedem Verbundserver in der Farm repliziert wird, enthält die Verbundserverfarm mit SQL Server-Topologie nur eine Kopie der Datenbank  
  
> [!NOTE]  
> SQL Server unterstützt viele unterschiedliche Daten- und Optionen für Speicherredundanz Anwendung einschließlich Failoverclustering, datenbankspiegelung und verschiedene Arten von SQL Server-Replikation.  
  
Das Microsoft Information Technology \(IT\) Abteilung verwendet SQL Server-datenbankspiegelung hohen\-Sicherheit \(synchrone\) -Modus und Failover-Clusterunterstützung zum Bereitstellen hoher\- Unterstützung für SQL Server-Instanz. SQL Server, die transaktionale \(Peer\-zu\-Peer\) und Mergereplikation wurde vom AD FS-Produktteam bei Microsoft nicht getestet. Weitere Informationen zu SQL Server, finden Sie unter [Übersicht über Lösungen von hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853) oder [Auswählen der geeigneten Typ der Replikation](https://go.microsoft.com/fwlink/?LinkId=214648).  
  
### <a name="supported-sql-server-versions"></a>Unterstützte SQL Server-Versionen  
Die folgenden SQL Server-Versionen werden mit AD FS, installiert mit Windows Server 2012 unterstützt:  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Server Platzierung und Netzwerk-Layout-Empfehlungen  
Ähnlich wie die Verbundserverfarm mit WID-Topologie, alle Verbundserver in der Farm sind so konfiguriert, dass ein Domain Name System-Cluster verwenden \(DNS\) Namen \(steht für den Namen des Verbunddiensts\)und einem-Cluster-IP-Adresse als Teil der Netzwerklastenausgleich \(NLB\) Clusterkonfiguration. Dadurch wird den NLB-Host, der Clientanforderungen an den einzelnen Verbundservern zugeordnet. Verbundserverproxys können auf die Proxy-Clientanforderungen an die Verbundserverfarm verwendet werden.  
  
Die folgende Abbildung zeigt, wie das fiktive Unternehmen Contoso Pharmaceuticals die Verbundserverfarm mit SQL Server-Topologie im Unternehmensnetzwerk bereitgestellt wird. Außerdem wird gezeigt, wie diese Unternehmen Umkreisnetzwerk mit Zugriff auf einen DNS-Server, einen zusätzlichen NLB-Host konfiguriert, die den gleichen DNS-Clusternamen verwendet \("FS.contoso.com"\) , die verwendet wird, auf dem Unternehmensnetzwerk NLB-Cluster, und klicken Sie mit zwei Verbundserverproxys \(fsp1 und fsp2\).  
  
![Mithilfe von SQL Server-farm](media/FarmSQLProxies.gif)  
  
Weitere Informationen dazu, wie Sie Ihre Netzwerkumgebung für die Verwendung mit Verbundserver oder Verbundserverproxys konfigurieren zu können, finden Sie unter [Namensauflösungsanforderungen für Verbundserver](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Name Anforderungen für die namensauflösung für Verbundserverproxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
