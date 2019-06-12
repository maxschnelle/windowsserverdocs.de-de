---
title: Häufig gestellte Fragen zu Speicherreplikaten
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: d03407292a797b1cd511937ba40fc0fa373f5dc0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447568"
---
# <a name="frequently-asked-questions-about-storage-replica"></a>Häufig gestellte Fragen zu Speicherreplikaten

>Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal)

In diesem Thema erhalten Sie Antworten auf häufig gestellte Fragen (FAQs) zu Speicherreplikaten.

## <a name="FAQ1"></a> Werden Funktion "Speicherreplikat" ist in Azure unterstützt?
Ja. Sie können die folgenden Szenarien mit Azure verwenden:

1. Server-zu-Server-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in ein oder zwei Fehlerdomänen im Rechenzentrum oder asynchron zwischen zwei unterschiedlichen Regionen)
2. Server-zu-Server die asynchrone Replikation zwischen Azure und lokal (mit VPN oder Azure ExpressRoute)
3. Cluster-zu-Cluster-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in ein oder zwei Fehlerdomänen im Rechenzentrum oder asynchron zwischen zwei unterschiedlichen Regionen)
4. Cluster-zu-Cluster, asynchrone Replikation zwischen Azure und lokal (mit VPN oder Azure ExpressRoute)

Weitere Hinweise zur Gast-clustering in Azure finden Sie unter: [Bereitstellen von IaaS-VM-Gastclustern in Microsoft Azure](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

Wichtige Hinweise:

1. Azure unterstützt keine freigegebenen VHDX-Gast-clustering, damit Windows Failover Cluster-VMs iSCSI-Zielen für klassische freigegebenem Speicher persistenten Datenträger Reservierung Failoverclustering oder "direkte Speicherplätze" verwenden müssen.
2. Es werden Azure Resource Manager-Vorlagen für "direkte Speicherplätze"-basierte Funktion "Speicherreplikat" clustering auf [erstellen Sie ein Storage Leerzeichen direkte SOFS-Clustern mit der Funktion "Speicherreplikat" für die Notfallwiederherstellung in Azure-Regionen](https://aka.ms/azure-storage-replica-cluster).  
3. RPC-Kommunikation des Clusters in Azure (indem Sie die Cluster-APIs zum Gewähren von Zugriff zwischen Clustern erforderlich)-Cluster erfordert Zugriff auf das Netzwerk für das CNO konfigurieren. Sie müssen die TCP-Port 135 und den dynamischen Bereich über TCP-Port 49152 zulassen. Verweis [Erstellen von Windows Server-Failovercluster auf Azure IaaS-VM – Teil 2 Netzwerk- und Erstellung](https://blogs.technet.microsoft.com/askcore/2015/06/24/building-windows-server-failover-cluster-on-azure-iaas-vm-part-2-network-and-creation/).  
4. Es ist möglich, zwei Knoten gastcluster zu verwenden, in dem jeder Knoten Loopback-iSCSI für einen asymmetrischen Cluster repliziert werden, indem die Funktion "Speicherreplikat" verwendet. Aber dies wird wahrscheinlich sehr schlechten Leistung aufweisen und sollte nur für sehr begrenzten Workloads oder Testzwecke verwendet werden.  

## <a name="FAQ2"></a> Wie sehe ich den Fortschritt der Replikation während der ersten Synchronisierung?  
Die auf dem Zielserver im Ereignisprotokoll für die Speicherreplikatverwaltung angezeigte Ereignismeldung 1237 zeigt alle 10 Sekunden die Anzahl der kopierten Bytes sowie die Anzahl von verbleibenden Bytes an. Sie können auch den Speicherreplikat-Leistungsindikator auf dem Ziel verwenden, der **\Speicherreplikatstatistik\Gesamtzahl empfangener Bytes** für mindestens ein repliziertes Volume anzeigt. Die Replikationsgruppe kann auch mithilfe von Windows PowerShell abgefragt werden. Über diesen Beispielbefehl wird z. B. der Name der Gruppen auf dem Ziel abgerufen und die Gruppe **Replication 2** alle 10 Sekunden abgefragt, um den Fortschritt anzuzeigen:  

```  
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```  

## <a name="FAQ3"></a>Kann ich bestimmte Netzwerkschnittstellen für die Replikation angeben?  

Ja, mithilfe von `Set-SRNetworkConstraint`. Dieses Cmdlet wird auf Schnittstellenebene ausgeführt und kann sowohl in Clusterszenarios als auch in Szenarios ohne Cluster verwendet werden.  
Beispiel mit einem eigenständigen Server (auf jedem Knoten):  

```  
Get-SRPartnership  

Get-NetIPConfiguration  
```  
Beachten Sie die Informationen zu Gateway und Schnittstelle (auf beiden Servern) sowie die Richtungen der Partnerschaften. Führen Sie dann Folgendes aus:  

```  
Set-SRNetworkConstraint -SourceComputerName sr-srv06 -SourceRGName rg02 -  
SourceNWInterface 2 -DestinationComputerName sr-srv05 -DestinationNWInterface 3 -DestinationRGName rg01  

Get-SRNetworkConstraint  

Update-SmbMultichannelConnection  

```  

So konfigurieren Sie Netzwerkeinschränkungen auf einem Stretched Cluster:  

    Set-SRNetworkConstraint -SourceComputerName sr-srv01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-srv03 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"  

## <a name="FAQ4"></a> Kann ich 1: n Replikation oder Transitive (A, B, C)-Replikation konfigurieren?  
Nein. Funktion "Speicherreplikat" unterstützt nur 1: 1-Replikation von einem Server, Cluster oder Stretched Cluster-Knoten. In einem späteren Release kann sich dies ändern. Sie können natürlich eine Replikation zwischen verschiedenen Servern eines bestimmten Volume-Paars in beide Richtungen konfigurieren. Beispielsweise kann Server 1 sein D-Volume an Server 2, und sein E-Volume von Server 3 replizieren.

## <a name="FAQ5"></a> Kann ich die vergrößert oder verkleinert werden replizierte Volumes, die durch das Speicherreplikatfeature repliziert?  
Sie können Volumes vergrößern (erweitern), aber nicht verkleinern. Speicherreplikate verhindern standardmäßig, dass Administratoren replizierte Volumes erweitern. Verwenden Sie die Option `Set-SRGroup -AllowVolumeResize $TRUE` in der Quellgruppe vor dem Ändern der Größe. Zum Beispiel:

1. Verwenden Sie auf dem Quellcomputer: `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. Vergrößern Sie das Volume mithilfe des bevorzugten Verfahrens
3. Verwenden Sie auf dem Quellcomputer: `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>Kann ich ein Zielvolume online für nur-Lese Zugriff verwenden?  
Nicht in Windows Server 2016. Das Speicherreplikat hebt das Zielvolumes bei Beginn der Replikation auf. 

Allerdings wird in Windows Server-2019 und Windows Server Halbjährlicher Kanal ab Version, ein 1709 die Option zum Bereitstellen der Zielspeicher ist jetzt möglich – dieses Feature heißt "Test-Failover". Dazu benötigen Sie ein nicht verwendetes NTFS oder ReFS-formatiertes Volume, das derzeit nicht auf dem Zielserver repliziert wird. Sie können dann eine Momentaufnahme des replizierten Speichers vorübergehend zu Test- und Sicherungszwecken bereitstellen. 

Geben Sie beispielsweise Folgendes ein, um ein Test-Failover zu erstellen, in dem Sie ein Volume "D:" in der Replikationsgruppe "RG2" auf dem Zielserver "SRV2" replizieren und das Laufwerk "T:" auf dem Computern SRV2 haben, das nicht repliziert wird:

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
Das replizierte Volume "D:" ist jetzt auf den Computern SRV2 verfügbar. Sie können das Lesen und schreiben, in der Regel kopieren Sie Dateien aus einem Dienst, oder führen Sie eine online-Sicherung, die Sie an anderer Stelle zur Aufbewahrung, unter dem Pfad "d:" speichern. Das T: Volume nur Daten enthalten.

So entfernen Sie den Test-Failover-Snapshot und Verwerfen die Änderungen:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
Sie sollten die Funktion zum Testen des Failovers nur für kurzfristige temporäre Vorgänge verwenden. Sie ist nicht für die langfristige Verwendung vorgesehen. Bei der Durchführung läuft die Replikation auf dem tatsächlichen Zielvolume. 

## <a name="FAQ7"></a> Kann ich die Skalierung (Scale-Out-Datei Server, SOFS) in einem Stretched Cluster konfigurieren?  
Wenngleich es technisch möglich ist, ist dies keine empfohlene Konfiguration aufgrund des Mangels an Standortinformationen in den Compute-Knoten, der die SOFS kontaktieren. Bei Verwendung von campusnetzwerken, in denen Wartezeiten in der Regel im Bereich unter Millisekunden, liegen funktioniert diese Konfiguration in der Regel ohne Probleme.   

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ7.5"></a> Werden CSV ist erforderlich, um in einem Stretched Cluster oder zwischen Clustern repliziert werden?  
Nein. Sie können mit CSV- oder persistenten Datenträger Reservierung (Laos) im Besitz einer Clusterressource, z. B. eine Rolle "Dateiserver" replizieren. 

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ8"></a>Kann ich "direkte Speicherplätze" in einem Stretched Cluster mit Speicherreplikaten konfigurieren?  
Dies ist keine unterstützte Konfiguration in Windows Server. In einem späteren Release kann sich dies ändern. Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature volle Unterstützung für Dateiserver mit horizontaler Skalierung und Hyper-V-Server (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ9"></a>Wie konfiguriere ich die asynchronen Replikation?  

Geben Sie `New-SRPartnership -ReplicationMode` und das Argument **Asynchronous** an. Standardmäßig wird jede Replikation im Speicherreplikatfeature synchron ausgeführt. Sie können den Modus auch mit `Set-SRPartnership -ReplicationMode` ändern.  

## <a name="FAQ10"></a>Wie verhindere ich Automatisches Failover eines Stretched Clusters?  
Um ein automatisches Failover zu verhindern, können Sie `Get-ClusterNode -Name "NodeName").NodeWeight=0` mithilfe von PowerShell konfigurieren. Dadurch wird die Abstimmung auf den einzelnen Knoten am Notfallwiederherstellungsstandort entfernt. Anschließend können Sie `Start-ClusterNode -PreventQuorum` auf Knoten am primären Standort und `Start-ClusterNode -ForceQuorum` auf Knoten am Notfallstandort verwenden, um ein Failover zu erzwingen. Es ist keine grafische Option verfügbar, um ein automatisches Failover zu verhindern, und das Verhindern des automatischen Failovers wird nicht empfohlen.  

## <a name="FAQ11"></a>Wie deaktiviere ich VM-resilienz?
Um zu verhindern, dass die neuen Hyper-V-VM-resilienzfeatures ausgeführt wird und daher virtuelle Computer anzuhalten anstatt ein Failover auf den Standort für die notfallwiederherstellung ausgeführt. `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> Wie kann ich Zeit für die erste Synchronisierung verkürzen?

Eine Möglichkeit, die Dauer der ersten Synchronisierung zu verkürzen, bietet die schlanke Speicherzuweisung. Das Speicherreplikatfeature führt eine Abfrage nach Speicher mit schlanker Zuweisung durch und verwendet diesen Speicher automatisch (einschließlich nicht gruppierter Speicherplätze, dynamischer Hyper-V-Datenträger und SAN-LUNs).  

Sie können auch per Seeding hinzugefügte Daten-Volumes zu verwenden, um die bandbreitennutzung zu verringern und manchmal Zeit, um sicherzustellen, dass das Ziel Volume weist eine Untermenge an Daten vom primären anschließend verwenden Sie die Option für ein ausgeführtes Seeding im Failovercluster-Manager oder `New-SRPartnership`. Wenn das Volume überwiegend leer ist, kann mit einer Seeding-Synchronisierung die Nutzung von Zeit und Bandbreite reduziert werden. Es gibt mehrere Möglichkeiten, mit verschiedenen Isolationsgraden Wirksamkeit der Seed-Daten:

1. Vorherigen Replikation – durch Replikation mit normalen anfängliche synchronisieren lokal zwischen Knoten, die die Datenträger und Volumes enthält, Entfernen von Replikationen, Protokollversand die Zieldatenträger an anderer Stelle, und die Replikation mit der Option per Seeding hinzugefügten hinzufügen. Dies ist die effektivste Methode, wie die Funktion "Speicherreplikat" definitiv eine Block-Copy-Spiegelung und das einzige replizieren Delta-Blöcke.
2. Momentaufnahme wiederhergestellt oder Wiederherstellung der Momentaufnahme-basierte backup – durch das Wiederherstellen einer Momentaufnahme volumenbasierten auf das Zielvolume, dürfte das minimaler Unterschiede in das Blocklayout. Dies ist die nächste effektivste Methode, wie Blöcke entsprechend Dank Speichervolume-Momentaufnahmen Spiegelbilder wird wahrscheinlich sind.
3. Kopieren Sie die kopierte Dateien - durch ein neues Volume auf dem Ziel, das nie vor dem verwendet wurde erstellen und Ausführen einer vollständigen Robocopy/mir-Struktur der Daten, gibt es wahrscheinlich Block entspricht. Mit dem Windows-Dateiexplorer, oder kopieren einen Teil der Struktur wird nicht viele Übereinstimmungen von Block erstellt. Manuelles Kopieren von Dateien ist die am wenigsten effektive Methode des Seedings.

## <a name="FAQ13"></a> Kann ich Benutzer für die replikationsverwaltung delegieren?  

Sie können die `Grant-SRDelegation` Cmdlet. Mit diesem Cmdlet können Sie bestimmte Benutzer in Server-zu-Server-, Cluster-zu-Cluster- und Stretched Cluster-Replikationsszenarien festlegen, die über die Berechtigungen zum Erstellen, Ändern oder Entfernen der Replikation verfügen, ohne Mitglied der lokalen Administratorengruppe zu sein. Zum Beispiel:  

    Grant-SRDelegation -UserName contso\tonywang  

Das Cmdlet weist Sie darauf hin, dass der Benutzer sich beim zu verwaltenden Server ab- und erneut anmelden muss, damit die Änderungen wirksam werden. Diese Konfiguration kann mithilfe von `Get-SRDelegation` und `Revoke-SRDelegation` weiter gesteuert werden.  

## <a name="FAQ13"></a> Was sind die sicherungs- und Wiederherstellungsoptionen für replizierte Volumes?
Das Speicherreplikatfeature unterstützt das Sichern und Wiederherstellen des Quellvolumes. Es bietet außerdem Unterstützung für das Erstellen und Wiederherstellen von Momentaufnahmen des Quellvolumes. Das Zielvolume kann nicht gesichert oder wiederhergestellt werden, während es durch das Speicherreplikatfeature geschützt ist. Es ist weder bereitgestellt, noch kann darauf zugegriffen werden. Bei Verlust des Quellvolumes in einem Notfallszenario können Sie mithilfe von `Set-SRPartnership` das vorherige Zielvolume als lesbare und beschreibbare Quelle festlegen, um dieses Volume sichern und wiederherstellen zu können. Sie können die Replikation auch mit `Remove-SRPartnership` und `Remove-SRGroup` entfernen, um das Volume als lesbares und beschreibbares Volume erneut bereitzustellen.
Für eine regelmäßige Erstellung von anwendungskonsistenten Momentaufnahmen können Sie VSSADMIN.EXE auf dem Quellserver ausführen, um Momentaufnahmen der replizierten Datenvolumes zu erstellen. Beispiel für die Replikation des Volumes F: mit dem Speicherreplikatfeature:

    vssadmin create shadow /for=F:
Anschließend können Sie eine beliebige Momentaufnahme wiederherstellen, nachdem Sie die Replikationsrichtung geändert oder die Replikation entfernt haben bzw. wenn Sie weiterhin dasselbe Quellvolume verwenden. Beispiel, wenn Sie weiterhin F: verwenden:

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
Mithilfe eines geplanten Tasks können Sie auch die regelmäßige Ausführung dieses Tools planen. Weitere Informationen zur Verwendung von VSS finden Sie unter [Vssadmin](../../administration/windows-commands/vssadmin.md). Das Sichern der Protokollvolumes ist nicht notwendig oder sinnvoll. Der Versuch, diesen Vorgang auszuführen, wird von VSS ignoriert.
Das Speicherreplikatfeature unterstützt die Verwendung von Windows Server-Sicherung, Microsoft Azure Backup, Microsoft DPM oder anderen Momentaufnahme-, VSS-, VM- oder dateibasierten Technologien, sofern diese auf Volume-Ebene eingesetzt werden. Das Speicherreplikatfeature bietet keine Unterstützung für blockbasierte Sicherungen und Wiederherstellungen.

## <a name="FAQ14"></a> Kann ich die Replikation, um eine eingeschränkte bandbreitennutzung konfigurieren?
Ja, über die SMB-Bandbreiteneinschränkung. Diese globale Einstellung gilt für den gesamten Speicherreplikatdatenverkehr und wirkt sich daher auf sämtliche Replikationsvorgänge von diesem Server aus. Dies ist üblicherweise nur bei der Einrichtung der ersten Speicherreplikatsynchronisierung erforderlich, bei der sämtliche Volumedaten übertragen werden müssen. Wenn eine solche Einschränkung nach der ersten Synchronisierung erforderlich ist, ist Ihre Netzwerkbandbreite zu gering für Ihre E/A-Workload. Reduzieren Sie E/A, oder erhöhen Sie die Bandbreite.

Diese Einstellung sollte nur bei der asynchronen Replikation verwendet werden. Hinweis: Die erste Synchronisierung erfolgt selbst dann immer asynchron, wenn Sie eine synchrone Replikation festgelegt haben.
Sie können auch die QoS-Netzwerkrichtlinien verwenden, um den Speicherreplikatdatenverkehr einzuschränken. Bei Verwendung der Speicherreplikatreplikation mit durchgeführtem Seeding mit großer Übereinstimmung wird die Bandbreitennutzung bei der ersten Synchronisierung ebenfalls erheblich reduziert.


So legen Sie die Bandbreiteneinschränkung fest:

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

So zeigen Sie die Bandbreiteneinschränkung an:

    Get-SmbBandwidthLimit -Category StorageReplication

So entfernen Sie die Bandbreiteneinschränkung:

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>Welche Netzwerkports erfordert die Funktion "Speicherreplikat"?
Speicherreplikate verwenden SMB und WSMAN für die Replikation und Verwaltung. Dies bedeutet, dass die folgenden Ports erforderlich sind:

 445 (SMB - Transportprotokoll für die Replikation, die Cluster RPC-Management-Protokoll) 5445 (iWARP SMB – nur erforderlich, wenn mit iWARP RDMA-Netzwerk) 5985 (WSManHTTP - Management-Protokoll für die WMI/CIM/PowerShell)

Hinweis: Das Cmdlet "Test-SRTopology" erfordert ICMPv4/ICMPv6, jedoch nicht für Replikation oder Verwaltung.

## <a name="FAQ15.5"></a>Was sind die empfohlenen Vorgehensweisen für Log Volume?
Die optimale Größe des Protokolls variiert stark pro Umgebung und Arbeitslast, und es wird bestimmt, um wie viel e/a schreiben, die Ihre Workload. 

1.  Ein kleineres oder größeres Protokoll bestimmt nicht die Schnelligkeit
2.  Ein kleineres oder größeres Protokoll wirkt sich beispielsweise nicht auf das Datenvolume von 10 GB im Gegensatz zu 10 TB aus.

Ein größeres Protokoll sammelt und bewahrt nur mehr Schreib-E/A-Auslastung auf, bevor es umschlossen wird. Dadurch wird die Unterbrechung des Diensts zwischen dem Quell- und Zielcomputer – z. B. ein Netzwerkausfall oder wenn der Zielcomputer offline ist - verlängert. Wenn das Protokoll 10 Stunden an Schreibvorgängen enthalten kann, und das Netzwerk für 2 Stunden ausfällt, kann der Quellcomputer nach erneutem Verbinden mit dem Netzwerk einfach das Delta der nicht synchronisierten Änderungen schnell zum Ziel zurückgeben, und Sie sind erneut sehr schnell geschützt. Wenn das Protokoll 10 Stunden enthält und der Ausfall 2 Tage beträgt, muss der Quellcomputer Daten aus einem anderen Protokoll zurückgeben, das Bitmap genannt wird – was wahrscheinlich langsamer ist, um zum Synchronisieren zurückzukehren. Wenn die Synchronisierung abgeschlossen ist, wird das Protokoll erneut verwendet.

Das Speicherreplikat nutzt das Protokoll für die gesamte Schreibleistung. Die Protokollleistung ist für die Replikationsleistung von entscheidender Bedeutung. Sie müssen sicherstellen, dass die Leistung des Protokollvolumens besser als die des Datenvolumens ist, da das Protokoll alle Schreib-E/A-Lasten serialisiert und sequenzialisiert. Sie sollten auf Protokollvolumes immer Flashmedien verwenden, z. B. SSD. Sie dürfen niemals zulassen, dass andere Workloads auf dem Protokollvolume ausgeführt werden, so wie Sie auch niemals zulassen würden, dass andere Workloads auf SQL-Datenbank-Protokollvolumes ausgeführt werden. 

Erneut: Microsoft empfiehlt dringend, dass der Protokollspeicher schneller als die datenspeicherung und protokollvolumes müssen niemals für andere arbeitsauslastungen verwendet werden.

Log-größenempfehlungen erhalten Sie durch Ausführen des Test-SRTopology-Tools. Alternativ können Sie Leistungsindikatoren auf vorhandenen Servern verwenden, auf eine Log Size Entscheidung. Die Formel ist einfach: Überwachen Sie die Datenträger-Datendurchsatz (Avg geschrieben/s) unter der arbeitsauslastung, und verwenden, um die Zeitspanne zu berechnen, dauert es sich um das Protokoll der verschiedenen Größen zu füllen. Z. B. Datenträger-Datendurchsatz 50 MBIT/s der Logarithmus von 120 GB in Sekunden von 120 GB/50 MB oder 2400 Sekunden oder 40 Minuten umschließen verursacht. Daher ist die Zeitspanne, die der Zielserver möglicherweise nicht erreichbar ist, bevor das Protokoll, das umschlossen 40 Minuten. Wenn dient als Wrapper für das Protokoll, jedoch das Ziel wieder erreichbar ist, würde die Quelle Blöcke über das Bit Map-Protokoll anstelle der wichtigste Protokolldatei wiedergeben. Die Größe des Protokolls wird nicht auf die Leistung auswirken.

NUR auf der Datenträger aus dem quellcluster sollten gesichert werden. Die Replikat-Speicherprotokoll Datenträger sollten nicht gesichert werden, da eine Sicherung mit der Funktion "Speicherreplikat" Vorgänge in Konflikt stehen.

## <a name="FAQ16"></a> Warum entscheiden Sie sich im Vergleich zu Cluster-zu-Cluster im Vergleich zu Server-zu-Server-Topologie ein Stretched Clusters?  
Funktion "Speicherreplikat" ist in drei Haupt-Konfigurationen: Stretched Cluster, Cluster-zu-Cluster und Server-zu-Server. Jede bietet verschiedene Vorteile.

Die Stretched Cluster-Topologie ist ideal für Auslastungen, die automatisches Failover mit Orchestrierung wie z. B. private Hyper-V-Cloud-Cluster und SQL Server-Failoverclusterinstanzen erfordern. Es verfügt außerdem über eine integrierte Benutzeroberfläche, die den Failovercluster-Manager verwendet. Sie verwendet die klassische asymmetrische gemeinsam genutzte Cluster Speicherarchitektur von Speicherplätzen, SAN, iSCSI und RAID-Reservierungssemantik. Sie können dies mit nur 2 Knoten ausführen.

Die Cluster-zu-Cluster-Topologie verwendet zwei separate Cluster und eignet sich besonders für Administratoren, die manuelles Failover möchten, insbesondere, wenn der zweite Speicherort für die Notfallwiederherstellung und nicht die alltägliche Verwendung konfiguriert ist. Die Orchestrierung erfolgt manuell. Im Gegensatz zu Stretched Cluster kann "direkte Speicherplätze" in dieser Konfiguration (mit Einschränkungen - finden Sie unter der Funktion "Speicherreplikat" – häufig gestellte Fragen und -Cluster-zu-Cluster-Dokumentation) verwendet werden. Sie können dies mit nur 4 Knoten ausführen. 

Die Server-zu-Server-Topologie ist ideal für Kunden mit Hardware, die nicht als Clustern gruppiert werden kann. Sie erfordert manuelles Failover und Orchestrierung. Es ist ideal für kostengünstige Bereitstellungen zwischen Zweigstellen und zentralen Datencentern, insbesondere, wenn die asynchrone Replikation verwenden. Diese Konfiguration ersetzt häufig Instanzen von DFSR-geschützten Dateiservern, die für die Single Master Notfallwiederherstellungszenarien verwendet werden.

In allen Fällen kann die Topologie sowohl auf physischer Hardware als auch auf virtuellen Computern ausgeführt werden. In virtuellen Computern erfordert der zugrunde liegenden Hypervisor nicht Hyper-V und kann anstatt VMware, KVM, Xen verwenden.

Das Speicherreplikatfeature verfügt außerdem über einen Server-to-Self-Modus, in dem die Replikation auf zwei Volumes auf demselben Computer verweist.

## <a name="FAQ18"></a> Werden die Datendeduplizierung wird mit dem Speicherreplikat unterstützt?

Ja, wird die Daten Deduplcation mit dem Speicherreplikat unterstützt. Aktivieren der Datendeduplizierung auf einem Volume auf dem Quellserver und während der Replikation der Zielserver eine deduplizierte Kopie des Volumes empfängt.

Zwar Sie sollten *installieren* der Datendeduplizierung auf dem Quell-und Ziel (finden Sie unter [installieren und Aktivieren der Datendeduplizierung](../data-deduplication/install-enable.md)), es ist wichtig, nicht zu *aktivieren*Der Datendeduplizierung auf dem Zielserver. Funktion "Speicherreplikat" kann Schreibvorgänge nur auf dem Quellserver. Da die Datendeduplizierung Schreibvorgänge auf dem Volume vornimmt, sollten sie nur auf dem Quellserver ausführen. 

## <a name="FAQ19"></a> Kann ich zwischen 2019 für Windows Server und Windows Server 2016 replizieren?

Leider können wir unterstützen keine, erstellen eine *neue* Partnerschaft zwischen 2019 für Windows Server und Windows Server 2016. Sie können problemlos aktualisieren, einen Server oder Cluster, die unter Windows Server 2016 für Windows Server-2019 sowie *vorhandenen* Partnerschaften sind weiterhin funktionsfähig.

Allerdings rufen Sie die verbesserte replikationsleistung von Windows Server-2019 müssen alle Mitglieder der Partnerschaft 2019 für Windows Server ausführen und Sie müssen vorhandene Partnerschaften löschen verknüpften Replikationsgruppen und per Seeding hinzugefügten Daten (entweder neu erstellt Wenn Sie die Partnerschaft in Windows Admin Center oder mit dem Cmdlet New-SRPartnership erstellen).

## <a name="FAQ17"></a> Wie melde ich ein Problem mit Speicherreplikaten oder diesem Leitfaden?  
Falls Sie technische Unterstützung für Speicherreplikate benötigen, können Sie Ihre Fragen in den [Microsoft TechNet-Foren](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview) stellen. Sie können uns auch eine E-Mail an srfeed@microsoft.com senden, wenn Sie Fragen zu Speicherreplikaten oder dieser Dokumentation haben. Die <https://windowsserver.uservoice.com> Standort wird für Design Change Requests, bevorzugt, da anderen Kunden Unterstützung und Feedback zu Ihren Ideen geben können.



## <a name="related-topics"></a>Verwandte Themen  
- [Übersicht über Speicherreplikate](storage-replica-overview.md) 
- [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Server-zu-Server-Replikation](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster-Speicherreplikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikat: Bekannte Probleme](storage-replica-known-issues.md)  

## <a name="see-also"></a>Siehe auch  
- [Speicher – Übersicht](../storage.md)  
- [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)  
