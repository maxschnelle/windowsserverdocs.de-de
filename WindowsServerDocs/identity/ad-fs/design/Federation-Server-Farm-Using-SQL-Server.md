---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: Verbundserverfarm mit SQLServer
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2333f79c733415833b1d54afc8c385700ac5581e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>Verbundserverfarm mit SQLServer

>Gilt für: Windows Server 2016, Windows Server2012 R2

Diese Topologie wird für Active Directory Federation Services \(AD FS\) unterscheidet sich von der Verbundserverfarm mithilfe von Windows Internal Database \(WID\) Bereitstellungstopologie, dass sie die Daten nicht auf jedem Verbundserver der Farm repliziert wird. Stattdessen können allen Verbundservern in der Farm lesen und Schreiben von Daten in einer allgemeinen Datenbank, die auf einem Server mit Microsoft SQL Server, die sich im Unternehmensnetzwerk befindet gespeichert sind.  
  
> [!IMPORTANT]  
> Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server2008 und höhere Versionen, einschließlich SQL Server2012 und SQL Server2014.  
  
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
Die folgenden SQL Server-Versionen werden von AD FS unter Windows Server2012 R2 unterstützt:  
  
-   SQLServer 2008 \ / R2  
  
-   SQLServer 2012  
  
-   SQLServer 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Der Empfehlungen für die Platzierung und Netzwerk Layout Server  
Ähnlich wie die Verbundserverfarm mit WID-Topologie, alle Verbundserver in der Farm sind so konfiguriert, dass ein Domain Name System \(DNS\)-Clusternamens \ (die steht für den Verbunddienst Tokentypen) und ein Cluster-IP-Adresse als Teil der Netzwerklastenausgleich \(NLB\) Cluster-Konfiguration. Dadurch wird den NLB-Host-Anfragen an den einzelnen Verbundservern zugeordnet werden. Verbundserverproxys können zum Proxy-Clientanforderungen an die Verbundserverfarm verwendet werden.  
  
Die folgende Abbildungzeigt, wie die fiktive Contoso Pharmaceuticals Firma die Verbundserverfarm mit SQL Server-Topologie im Unternehmensnetzwerk bereitgestellt. Außerdem wird gezeigt, wie dieses Unternehmens Umkreisnetzwerk konfiguriert mit Zugriff auf einen DNS-Server, einen zusätzlichen NLB-Host, der die gleiche Cluster-DNS-Namen \(fs.contoso.com\) verwendet, die im Unternehmensnetzwerk NLB-Cluster verwendet wird und mit zwei webanwendungsproxys \(wap1 and wap2\).  
  
![Mithilfe von SQL Server-farm](media/SQLFarmADFSBlue.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbundserver oder webanwendungsproxys finden Sie unter "Namensauflösungsanforderungen" im Abschnitt [AD FS-Anforderungen](AD-FS-Requirements.md) und [Planen der Web Application Proxy-Infrastruktur (WAP)](https://technet.microsoft.com/library/dn383648.aspx).  
  
## <a name="high-availability-options-for-sql-server-farms"></a>Optionen für hohe Verfügbarkeit für SQL Server-Farmen  
In Windows Server2012 R2 sind AD FS gibt es zwei neue Optionen für die hohen Verfügbarkeit in AD FS-Farmen mit SQL Server unterstützen.  
  
-   Unterstützung für SQL Server AlwaysOn-Verfügbarkeitsgruppen  
  
-   Unterstützung für geografisch verteilten hohe Verfügbarkeit mithilfe der SQL Server-Mergereplikation  
  
In diesem Abschnittwird beschrieben, jede dieser Optionen, welche Probleme sie bzw. zu beheben, und einige wichtigen Überlegungen für die Entscheidung, welche Optionen bereitstellen.  
  
> [!NOTE]  
> AD FS-Farmen, mit denen Windows Internal Database \(WID\) Redundanz grundlegende Daten mit Lese-/Schreibzugriff auf dem primären Server-Knoten und schreibgeschützte Zugriff auf sekundären Knoten.  Dies kann in einem geografisch lokalen oder einem geografisch verteilten Topologie verwendet werden.  
>   
> Bei Verwendung von WID Beachten Sie die folgenden Einschränkungen:  
>   
> -   Ein Windows-datenbankfarm darf maximal 30 Verbundserver, besitzen Sie bis zu 100 Vertrauensstellungen vertrauenden Seite.  
> -   Ein Windows-datenbankfarm unterstützt keine Erkennung oder Artefakt Auflösung von tokenwiederholungen \ (Teil der \(SAML\) protocol\ Security Assertion Markup Language).  
  
Die folgende Tabelle enthält eine Zusammenfassung für die Verwendung einer Windows-datenbankfarm.  
  
||||  
|-|-|-|  
||1 \-100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen|  
|1 \-30-AD FS-Knoten|Interne Windows-Datenbank unterstützt|Nicht unterstützt, mit WID \-SQL erforderlich|  
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \-SQL erforderlich|Nicht unterstützt, mit WID \-SQL erforderlich|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn-Verfügbarkeitsgruppen  
**(Übersicht)**  
  
AlwaysOn-Verfügbarkeitsgruppen in SQL Server2012 eingeführt wurden, und geben eine neue Methode zum Erstellen einer SQL Server-Instanz mit hoher Verfügbarkeit.  AlwaysOn Availability Groups kombinieren Elemente von Clustering und der datenbankspiegelung für Redundanz und Failover auf die Ebene der SQL-Instanz und die Datenbankebene.  Im Gegensatz zu vorherigen Optionen für hohe Verfügbarkeit, AlwaysOn Availability Groups erfordern eine gemeinsame Speicher \ (oder vom Netzwerk Speicher-Bereich) auf der Datenbankebene.  
  
Eine verfügbarkeitsgruppe besteht aus einem primären Replikat \ (eine Reihe von primären Databases\ Lese-/ Schreibzugriff) und bis zu vier Verfügbarkeit Replikate \ (Gruppe von entsprechenden sekundären Databases\).  Der verfügbarkeitsgruppe unterstützt eine Kopie der einzelnen Lese-/ Schreibzugriff \ (die primäre Replica\), und bis zu vier schreibgeschützte Verfügbarkeit Replikate.  Jedes Replikat Verfügbarkeit muss auf einem anderen Knoten für einen einzelnen \(WSFC\) Failoverclustering in Windows Server-Cluster befinden.  Weitere Informationen zu AlwaysOn Availability Gruppen finden Sie unter [Übersicht über AlwaysOn Availability Groups \(SQL Server\)](https://technet.microsoft.com/library/ff877884.aspx).  
  
Aus der Perspektive der Knoten von einem AD FS SQL Server-Farm, ersetzt die AlwaysOn Availability Group als die Richtlinie für die SQL Server-Instanz \ / Artefakt-Datenbank.  Verfügbarkeitsgruppenlisteners des Clients ist \ (das AD FS Security Token Service\) Verbindung zum SQL verwendet.  
  
Das folgende Diagramm zeigt eine AD FS SQL Server-Farm mit AlwaysOn Availability Group.  
  
![Mithilfe von SQL Server-farm](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn Availability Groups erfordern, dass die SQL Server-Instanzen auf Windows Server-Failoverclustering \(WSFC\)-Knoten befinden.  
  
> [!NOTE]  
> Wie ein automatisches Failover-Ziel, die anderen drei manuelle Failover davon ausgegangen wird, kann nur ein Replikat der Verfügbarkeit fungieren.  
  
**Wichtige Hinweise**  
  
Wenn Sie AlwaysOn Availability Groups in Kombination mit SQL Server-Mergereplikation verwenden möchten, beachten Sie bitte die unter "Schlüssel Überlegungen zur Bereitstellung für die Verwendung von AD FS mit SQL Server-Mergereplikation" unten beschriebenen Probleme.  Insbesondere beim Failover einer AlwaysOn-verfügbarkeitsgruppe mit einer Datenbank, die ein Abonnent ist, das Abonnement Replikation schlägt fehl. Zum Fortsetzen der Replikation muss ein Replikationsadministrator der Abonnent manuell neu konfigurieren.  Weitere Informationen finden Sie in der SQL Server-Beschreibung der speziellen Problem am [Replikation Abonnenten und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx) und allgemeine Informationen zur Unterstützung für AlwaysOn-Verfügbarkeitsgruppen mit Optionen für die Replikation auf [Replikation, Änderungsnachverfolgung, Änderung der Datenerfassung und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
**Konfigurieren von AD FS ein AlwaysOn Availability Group verwenden**  
  
Konfigurieren von AD FS-Farm mit AlwaysOn Availability Groups erfordert eine geringfügige Änderung an der AD FS-Bereitstellungsverfahren:  
  
1.  Die Datenbanken, die Sie sichern möchten müssen erstellt werden, bevor die AlwaysOn Availability Groups konfiguriert werden können.  AD FS erstellt die Datenbanken als Teil der Installation und Erstkonfiguration von dem ersten Federation Service Knoten einen neuen AD FS-SQL Server-Farm.  Als Teil der AD FS-Konfiguration, müssen Sie eine SQL-Verbindungszeichenfolge angeben, sodass Sie so konfigurieren Sie den ersten AD FS-Farmknoten direkt Verbindung mit einer SQL-Instanz \ (Dies ist nur Temporary\).   Spezifische Anweisungen zum Konfigurieren von einem AD FS-Farm, einschließlich der Konfiguration von eines AD FS-Farm Knotens mit einer SQL Server-Verbindungszeichenfolge finden Sie unter [Konfigurieren eines Verbundservers](../../ad-fs/deployment/Configure-a-Federation-Server.md).  
  
2.  Nachdem Sie die AD FS-Datenbanken erstellt wurden, AlwaysOn Availability Groups zuweisen und den allgemeinen TCP/IP-Listener mit SQL Server-Tools erstellen und verarbeiten [Erstellung und Konfiguration von Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/ff878265.aspx).  
  
3.  Abschließend verwenden Sie PowerShell so bearbeiten Sie die AD FS-Eigenschaften, um die SQL-Verbindungszeichenfolge Verwendung der DNS-Adresse der AlwaysOn Availability Group des Listeners aktualisieren.  
  
    Beispiel für PSH Befehle aus, um die SQL-Verbindungszeichenfolge für die AD FS-Konfigurationsdatenbank Richtlinie aktualisieren:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  Beispiel für PSH Befehle aus, um die SQL-Verbindungszeichenfolge für die AD FS-Konfigurationsdatenbank Richtlinie aktualisieren:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server-Mergereplikation  
Auch in SQL Server2012 eingeführt wurde, können Mergereplikation für AD FS-Richtlinie Datenredundanz mit den folgenden Merkmalen:  
  
-   Lesen und Schreiben von Funktionen auf allen Knoten \ (nicht nur die Primary\)  
  
-   Kleinere Mengen an Daten asynchron repliziert werden, um zu vermeiden, Einführung in die Latenz für das System  
  
Das folgende Diagramm zeigt eine geografisch redundante AD FS-SQL Server-Farmen mit Mergereplikation \ (Herausgeber 1, 2 Subscribers\):  
  
![Mithilfe von SQL Server-farm](media/ADFSSQLGeoRedundancy3.png)  
  
**Bereitstellungsüberlegungen für die Verwendung von AD FS mit SQL Server-Mergereplikation Schlüssel \ (Beachten Sie Zahlen in der AbbildungAbove\)**  
  
-   Die Verteilerdatenbank ist für die Verwendung mit AlwaysOn Availability Groups oder die datenbankspiegelung nicht unterstützt.  Weitere Informationen finden Sie in SQL Server-Anweisungen für AlwaysOn-Verfügbarkeitsgruppen mit Optionen für die Replikation zur Unterstützung [Replikation, Änderungsnachverfolgung, Änderung der Datenerfassung und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
-   Wenn eine AlwaysOn-verfügbarkeitsgruppe mit einer Datenbank, die ein Abonnent ist, ein Failover durchgeführt, schlägt fehl, das Abonnement für die Replikation. Zum Fortsetzen der Replikation muss ein Replikationsadministrator der Abonnent manuell neu konfigurieren.  Weitere Informationen finden Sie in der SQL Server-Beschreibung der speziellen Problem am [Replikation Abonnenten und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx) und allgemeine Informationen zur Unterstützung für AlwaysOn-Verfügbarkeitsgruppen mit Optionen für die Replikation [Replikation, Änderungsnachverfolgung, Änderung der Datenerfassung und AlwaysOn-Verfügbarkeitsgruppen \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx).  
  
Weitere Informationen zum Konfigurieren von AD FS eine Mergereplikation SQL Server verwenden, finden Sie unter [Setup geografischen Redundanz mit SQL Server-Replikation](https://technet.microsoft.com/en-us/library/dn632406.aspx).  
  
## <a name="see-also"></a>Siehe auch  
[Planen der AD FS-Bereitstellungstopologie](Plan-Your-AD-FS-Deployment-Topology.md)  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

