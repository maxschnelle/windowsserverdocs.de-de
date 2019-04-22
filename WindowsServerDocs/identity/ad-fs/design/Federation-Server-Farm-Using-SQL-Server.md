---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: Verbundserverfarm mit SQL Server
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e26b7cac971f472bc8b5e48e3dc8cd2592dc22ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814781"
---
# <a name="federation-server-farm-using-sql-server"></a>Verbundserverfarm mit SQL Server

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Diese Topologie wird für Active Directory Federation Services \(AD FS\) unterscheidet sich von der Verbundserverfarm mit internen Windows-Datenbank \(WID\) Bereitstellungstopologie, werden sie nicht die Daten repliziert jedem Verbundserver in der Farm. Stattdessen können allen Verbundservern in der Farm lesen und Schreiben von Daten in einer allgemeinen Datenbank, die gespeichert werden, auf einem Server mit Microsoft SQL Server, die im Unternehmensnetzwerk befindet.  
  
> [!IMPORTANT]  
> Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012 und SQL Server 2014.  
  
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
Die folgenden SQL Server-Versionen werden mit AD FS unter Windows Server 2012 R2 unterstützt:  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Server Platzierung und Netzwerk-Layout-Empfehlungen  
Ähnlich wie die Verbundserverfarm mit WID-Topologie, alle Verbundserver in der Farm sind so konfiguriert, dass ein Domain Name System-Cluster verwenden \(DNS\) Namen \(steht für den Namen des Verbunddiensts\)und einem-Cluster-IP-Adresse als Teil der Netzwerklastenausgleich \(NLB\) Clusterkonfiguration. Dadurch wird den NLB-Host, der Clientanforderungen an den einzelnen Verbundservern zugeordnet. Verbundserverproxys können auf die Proxy-Clientanforderungen an die Verbundserverfarm verwendet werden.  
  
Die folgende Abbildung zeigt, wie das fiktive Unternehmen Contoso Pharmaceuticals die Verbundserverfarm mit SQL Server-Topologie im Unternehmensnetzwerk bereitgestellt wird. Außerdem wird gezeigt, wie diese Unternehmen Umkreisnetzwerk mit Zugriff auf einen DNS-Server, einen zusätzlichen NLB-Host konfiguriert, die den gleichen DNS-Clusternamen verwendet \("FS.contoso.com"\) , die verwendet wird, auf dem Unternehmensnetzwerk NLB-Cluster, und klicken Sie mit zwei Web Anwendungsproxys \(wap1 und wap2\).  
  
![Mithilfe von SQL Server-farm](media/SQLFarmADFSBlue.gif)  
  
Weitere Informationen dazu, wie Sie Ihre Netzwerkumgebung für die Verwendung mit Verbundserver oder webanwendungsproxys konfigurieren zu können, finden Sie unter "Anforderungen für die namensauflösung" im Abschnitt [AD FS-Anforderungen](AD-FS-Requirements.md) und [planen Sie das Web Infrastruktur für Webanwendungsproxy (WAP)](https://technet.microsoft.com/library/dn383648.aspx).  
  
## <a name="high-availability-options-for-sql-server-farms"></a>Optionen für hohe Verfügbarkeit für SQL Server-Farmen  
In Windows Server 2012 R2 sind die AD FS gibt es zwei neue Optionen zur Unterstützung von hohen Verfügbarkeit in AD FS-Farmen, die mithilfe von SQL Server.  
  
-   Unterstützung für SQL Server AlwaysOn-Verfügbarkeitsgruppen  
  
-   Unterstützung für geografisch verteilte hohe Verfügbarkeit mit SQL Server-Mergereplikation  
  
In diesem Abschnitt wird beschrieben, jede dieser Optionen an, welche Probleme sie jeweils zu lösen, und einige wichtigsten Überlegungen für die Entscheidung, welche Optionen für die Bereitstellung.  
  
> [!NOTE]  
> AD FS-Farmen, die interne Windows-Datenbank verwenden \(WID\) grundlegende Daten zur Redundanz mit Leseberechtigungen\/Zugriff auf die Knoten für den primären Verbundserver Server schreiben und Lesen von\-nur Zugriff auf sekundäre Knoten.  Dies kann in einem geografisch lokalen oder einer geografisch verteilten Topologie verwendet werden.  
>   
> Bei Verwendung von WID Achten Sie darauf, dass Sie die folgenden Einschränkungen:  
>   
> -   Eine WID-Farm hat ein Limit von 30 Verbundserver aus, wenn Sie bis zu 100 Vertrauensstellungen der vertrauenden Seite Partei haben.  
> -   Eine WID-Farm unterstützt keine token-Replay-Erkennung oder Artefakt Auflösung \(Teil der Security Assertion Markup Language \(SAML\) Protokoll\).  
  
Die folgende Tabelle enthält eine Zusammenfassung für die Verwendung einer Windows-datenbankfarm.  
  
||||  
|-|-|-|  
||1 \- 100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen|  
|1 \- 30 AD FS-Knoten|WID unterstützt|Nicht unterstützt, mit WID \- SQL erforderlich|  
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \- SQL erforderlich|Nicht unterstützt, mit WID \- SQL erforderlich|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn-Verfügbarkeitsgruppen  
**Übersicht**  
  
AlwaysOn-Verfügbarkeitsgruppen in SQL Server 2012 eingeführt wurden, und geben Sie eine neue Möglichkeit zum Erstellen einer SQL Server-Instanz hochverfügbarkeit.  AlwaysOn-Verfügbarkeitsgruppen kombinieren Sie Elemente von Failoverclustering und datenbankspiegelung für die Redundanz- und Failoverfunktionen auf der Ebene der SQL-Instanz und der Datenbankebene übernimmt.  Im Gegensatz zu vorherigen Optionen für hohe Verfügbarkeit, AlwaysOn-Verfügbarkeitsgruppen erfordern keinen gemeinsamen Speicher \(oder Storage Area Network\) auf der Datenbankschicht.  
  
Eine verfügbarkeitsgruppe besteht aus einem primären Replikat \(einen Satz von Read\-primäre Datenbanken schreiben\) und einen bis vier verfügbarkeitsreplikaten \(legt fest, der entsprechenden sekundären Datenbanken\).  Die verfügbarkeitsgruppe unterstützt einen einzigen Lesevorgang\-schreiben Kopie \(das primäre Replikat\), und einen bis vier lesen\-nur Replikate der verfügbarkeitsgruppe.  Jedes verfügbarkeitsreplikat muss auf einem anderen Knoten von einem einzelnen Windows Server Failover Clustering befinden \(WSFC\) Cluster.  Weitere Informationen zu AlwaysOn Availability Gruppen finden Sie unter [Übersicht über AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/ff877884.aspx).  
  
Aus der Perspektive der Knoten einer AD FS-SQL Server-Farm, ersetzt die AlwaysOn-verfügbarkeitsgruppe die einzelne SQL Server-Instanz als Richtlinie \/ Artefakt-Datenbank.  Listener der verfügbarkeitsgruppe ist, was der Client \(der AD FS-Sicherheitstokendienst\) verwendet, um die Verbindung zu SQL hergestellt.  
  
Das folgende Diagramm zeigt eine AD FS SQL Server-Farm mit AlwaysOn-verfügbarkeitsgruppe.  
  
![Mithilfe von SQL Server-farm](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn-Verfügbarkeitsgruppen erfordern, dass die SQL Server-Instanzen auf Windows Server Failover Clustering befinden \(WSFC\) Knoten.  
  
> [!NOTE]  
> Nur ein verfügbarkeitsreplikat kann fungieren, wie ein automatisches Failover-Ziel, den anderen drei auf manuelle Failover verwendet werden.  
  
**Wichtige Aspekte der Bereitstellung**  
  
Wenn Sie AlwaysOn-Verfügbarkeitsgruppen in Verbindung mit SQL Server-Mergereplikation verwenden möchten, beachten Sie bitte die unten unter "Schlüssel Überlegungen zur Bereitstellung mithilfe von AD FS mit der SQL Server-Mergereplikation" beschriebenen Probleme.  Wenn eine AlwaysOn-verfügbarkeitsgruppe, die mit einer Datenbank, die einen Replikationsabonnenten ist ein Failover ausführt, schlägt das Replikationsabonnement insbesondere fehl. Zum Fortsetzen der Replikation muss ein Replikationsadministrator den Abonnenten manuell neu konfigurieren.  Finden Sie in der SQL Server-Beschreibung von bestimmten Problem [Replikationsabonnenten und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\) ](https://technet.microsoft.com/library/hh882436.aspx) und allgemeine Unterstützung für AlwaysOn-Verfügbarkeitsgruppen mit an-Replikationsoptionen [Replikation, Änderungsnachverfolgung, Change Data Capture und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
**Konfigurieren von AD FS mit einer AlwaysOn-verfügbarkeitsgruppe**  
  
Konfigurieren von AD FS-Farm mit AlwaysOn-Verfügbarkeitsgruppen sind eine kleine Änderung an der AD FS-Bereitstellungsverfahren erforderlich:  
  
1.  Die Datenbanken, die Sie sichern möchten müssen erstellt werden, bevor die AlwaysOn-Verfügbarkeitsgruppen konfiguriert werden können.  AD FS erstellt seine Datenbanken als Teil der Installation und Erstkonfiguration des ersten Verbund Dienstknotens einer neuen AD FS-SQL Server-Farm.  Sie müssen im Rahmen der AD FS-Konfiguration wird eine SQL-Clientverbindungszeichenfolge, angeben, so dass Sie so konfigurieren Sie den ersten AD FS-farmknoten, die direkte Verbindung mit einer SQL-Instanz herzustellen \(Dies ist nur vorübergehend\).   Spezielle Anweisungen zum Konfigurieren einer AD FS-Farm, einschließlich der Konfiguration von eines Knotens der AD FS-Farm mit einer SQL Server-Verbindungszeichenfolge finden Sie [Konfigurieren eines Verbundservers](../../ad-fs/deployment/Configure-a-Federation-Server.md).  
  
2.  Sobald der AD FS-Datenbanken erstellt wurden, weisen Sie sie für AlwaysOn-Verfügbarkeitsgruppen und erstellen Sie den allgemeinen TCP/IP-Listener, die mithilfe von SQL Server-Tools und verarbeitet werden [Erstellung und Konfiguration von Verfügbarkeitsgruppen \(SQL Server\) ](https://technet.microsoft.com/library/ff878265.aspx).  
  
3.  Abschließend verwenden Sie PowerShell zum Bearbeiten der AD FS-Eigenschaften zum Aktualisieren der SQL-Verbindungszeichenfolge, um die DNS-Adresse des Listeners, der die AlwaysOn-verfügbarkeitsgruppe verwenden.  
  
    PSH-Beispielbefehle zum SQL-Verbindungszeichenfolge für die AD FS-Konfigurationsdatenbank zu aktualisieren:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  PSH-Beispielbefehle zum SQL-Verbindungszeichenfolge für die AD FS-Artefakt Auflösung-Service-Datenbank zu aktualisieren:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server-Mergereplikation  
Auch in SQL Server 2012 eingeführt wurde, können die Mergereplikation für von Redundanz für die Daten von AD FS-Richtlinie mit den folgenden Merkmalen:  
  
-   Lesen und Schreiben von Funktionen auf allen Knoten \(nicht nur das primäre\)  
  
-   Kleinere Datenmengen, die asynchron repliziert werden, um zu vermeiden, Einführung in die Latenz für das system  
  
Das folgende Diagramm zeigt eine geografisch redundant mit AD FS-SQL Server-Farmen mit Mergereplikation \(Verleger mit 1, 2-Abonnenten\):  
  
![Mithilfe von SQL Server-farm](media/ADFSSQLGeoRedundancy3.png)  
  
**Bereitstellungsüberlegungen für Schlüssel für die Verwendung von AD FS mit SQL Server-Mergereplikation \(Beachten Sie die Zahlen in der Abbildung oben\)**  
  
-   Die Verteilerdatenbank wird für die Verwendung mit AlwaysOn-Verfügbarkeitsgruppen oder datenbankspiegelung nicht unterstützt.  Finden Sie unter SQL Server-Anweisungen für AlwaysOn-Verfügbarkeitsgruppen mit Optionen für die Replikation an support [Replikation, Änderungsnachverfolgung, Change Data Capture und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
-   Beim Failover einer AlwaysOn-verfügbarkeitsgruppe, die mit einer Datenbank, die einen Replikationsabonnenten darstellt, schlägt das Replikationsabonnement fehl. Zum Fortsetzen der Replikation muss ein Replikationsadministrator den Abonnenten manuell neu konfigurieren.  Finden Sie in der SQL Server-Beschreibung von bestimmten Problem [Replikationsabonnenten und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\) ](https://technet.microsoft.com/library/hh882436.aspx) und allgemeine Unterstützung für AlwaysOn-Verfügbarkeitsgruppen mit Optionen für die Replikation [Replikation, Änderungsnachverfolgung, Change Data Capture und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
Ausführlichere Anweisungen zum Konfigurieren von AD FS zur Verwendung einer SQL Server-Mergereplikation finden Sie unter [Setup geografische Redundanz mit SQL Server-Replikation](https://technet.microsoft.com/library/dn632406.aspx).  
  
## <a name="see-also"></a>Siehe auch  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

