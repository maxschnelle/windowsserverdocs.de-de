---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: Verbundserverfarm mit SQLServer
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a0fff975b9cb278e59686323d2bd72e641597573
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>Verbundserverfarm mit SQLServer

>Gilt für: Windows Server 2012

Diese Topologie wird für Active Directory Federation Services \(AD FS\) unterscheidet sich von der Verbundserverfarm mithilfe von Windows Internal Database \(WID\) Bereitstellungstopologie, dass sie die Daten nicht auf jedem Verbundserver der Farm repliziert wird. Stattdessen können allen Verbundservern in der Farm lesen und Schreiben von Daten in einer allgemeinen Datenbank, die auf einem Server mit Microsoft SQL Server, die sich im Unternehmensnetzwerk befindet gespeichert sind.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
Dieser Abschnittbeschreibt die verschiedenen Aspekte über die Zielgruppe, Vorteile und Einschränkungen, die dieser Bereitstellungstopologie zugeordnet sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Große Unternehmen mit mehr als 100 Vertrauensstellungen, die ihre interne Benutzer und die externe Benutzer einzelne Standardparameter auf \(SSO\) Zugriff auf die verbundanwendung oder Dienste ermöglichen  
  
-   Organisationen, die bereits mithilfe von SQL Server und ihre vorhandenen Tools und Kenntnisse nutzen möchten  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Was sind die Vorteile der Verwendung dieser Topologie?  
  
-   Unterstützung für eine größere Anzahl von Vertrauensstellungen \(more than 100\)  
  
-   Unterstützung für die Erkennung von tokenwiederholungen \(a security Feature\) und Artefaktauflösung \ (Security Assertion Markup Language-\(SAML\) 2.0 Teil Protocol\)  
  
-   Unterstützung für die Vorteile von SQL Server, z.B. spiegeln, Tools für die Failover-Clusterunterstützung, Berichterstellung und Verwaltung von Datenbanken  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Was sind die Grenzen der Verwendung dieser Topologie?  
  
-   Diese Topologie stellt keine datenbankredundanz standardmäßig bereit. Obwohl eine Verbundserverfarm mit WID-Topologie automatisch die WID-Datenbank auf jedem Verbundserver in der Farm repliziert, enthält die Verbundserverfarm mit SQL Server-Topologie nur eine Kopie der Datenbank  
  
> [!NOTE]  
> SQL Server unterstützt viele unterschiedliche Daten und Redundanz Anwendungsoptionen einschließlich Failover-Clusterunterstützung, datenbankspiegelung und verschiedene Arten von SQL Server-Replikation.  
  
Das Microsoft Information Technology \(IT\) Abteilung verwendet SQL Server-datenbankspiegelung in allgemeine \(synchronous\)-Modus und Failover-Clusterunterstützung Hochverfügbarkeitsszenarien Unterstützung für SQL Server-Instanz bereitstellen. SQL Server-Transaktions-\(peer\-to\-peer\) und Mergereplikation wurden nicht vom AD FS-Produktteam bei Microsoft getestet. Weitere Informationen zu SQL Server finden Sie unter [Übersicht über Lösungen mit hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853) oder [Auswählen der entsprechenden Typ der Replikation](https://go.microsoft.com/fwlink/?LinkId=214648).  
  
### <a name="supported-sql-server-versions"></a>Unterstützte SQL Server-Versionen  
Die folgenden SQL Server-Versionen werden von AD FS, installiert mit Windows Server2012 unterstützt:  
  
-   SQLServer 2008 \ / R2  
  
-   SQLServer 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Der Empfehlungen für die Platzierung und Netzwerk Layout Server  
Ähnlich wie die Verbundserverfarm mit WID-Topologie, alle Verbundserver in der Farm sind so konfiguriert, dass ein Domain Name System \(DNS\)-Clusternamens \ (die steht für den Verbunddienst Tokentypen) und ein Cluster-IP-Adresse als Teil der Netzwerklastenausgleich \(NLB\) Cluster-Konfiguration. Dadurch wird den NLB-Host-Anfragen an den einzelnen Verbundservern zugeordnet werden. Verbundserverproxys können zum Proxy-Clientanforderungen an die Verbundserverfarm verwendet werden.  
  
Die folgende Abbildungzeigt, wie die fiktive Contoso Pharmaceuticals Firma die Verbundserverfarm mit SQL Server-Topologie im Unternehmensnetzwerk bereitgestellt. Außerdem wird gezeigt, wie dieses Unternehmens Umkreisnetzwerk konfiguriert mit Zugriff auf einen DNS-Server, einen zusätzlichen NLB-Host, der die gleiche Cluster-DNS-Namen \(fs.contoso.com\) verwendet, die im Unternehmensnetzwerk NLB-Cluster verwendet wird und mit zwei Verbundserverproxys \(fsp1 and fsp2\).  
  
![Mithilfe von SQL Server-farm](media/FarmSQLProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung Verbundserver und Verbundserverproxys finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Name Resolution Requirements for Federation Server Proxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
