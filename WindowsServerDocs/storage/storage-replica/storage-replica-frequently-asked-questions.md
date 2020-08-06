---
title: Häufig gestellte Fragen zu Speicherreplikaten
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/15/2020
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: 04477ac9d7aa7905a4d5fc4dd58c7891c91f5baf
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769698"
---
# <a name="frequently-asked-questions-about-storage-replica"></a>Häufig gestellte Fragen zu Speicherreplikaten

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

In diesem Thema erhalten Sie Antworten auf häufig gestellte Fragen (FAQs) zu Speicherreplikaten.

## <a name="is-storage-replica-supported-on-azure"></a><a name="FAQ1"></a>Wird das Speicher Replikat in Azure unterstützt?

Ja. Sie können die folgenden Szenarien mit Azure verwenden:

1. Server-zu-Server-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in einer oder zwei Rechenzentrums Fehler Domänen oder asynchron zwischen zwei separaten Regionen)
2. Asynchrone Server-zu-Server-Replikation zwischen Azure und lokal (über VPN oder Azure expressroute)
3. Cluster-zu-Cluster-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in einer oder zwei Rechenzentrums Fehler Domänen oder asynchron zwischen zwei separaten Regionen)
4. Asynchrone Cluster-zu-Cluster-Replikation zwischen Azure und lokal (über VPN oder Azure expressroute)

Weitere Hinweise zum Gastclustering in Azure finden Sie unter: Bereitstellen von [IaaS-VM-Gast Clustern in Microsoft Azure](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

Wichtige Hinweise:

1. Azure unterstützt keine freigegebenen vhdx-Gastclustering. Daher müssen virtuelle Windows-Failovercluster-Computer iSCSI-Ziele für permanente Datenträger-Reservierungs Clustering oder direkte Speicherplätze für den klassischen freigegebenen Speicher verwenden.
2. Zum [Erstellen eines direkte Speicherplätze sofs-Clusters mit Speicher Replikat für die Notfall Wiederherstellung in Azure-Regionen](https://aka.ms/azure-storage-replica-cluster)gibt es Azure Resource Manager Vorlagen für direkte Speicherplätze-basiertes Speicher Replikat Cluster.
3. Cluster-zu-Cluster-RPC-Kommunikation in Azure (erforderlich für die Cluster-APIs zum Gewähren von Zugriff zwischen Clustern) erfordert das Konfigurieren des Netzwerk Zugriffs für das CNO. Sie müssen den TCP-Port 135 und den dynamischen Bereich oberhalb des TCP-Ports 49152 zulassen. Referenz [zum Erstellen eines Windows Server-Failoverclusters auf Azure IaaS-VM – Teil 2 Netzwerk und Erstellung](/archive/blogs/askcore/building-windows-server-failover-cluster-on-azure-iaas-vm-part-2-network-and-creation).
4. Es ist möglich, Gast Cluster mit zwei Knoten zu verwenden, bei denen jeder Knoten Loopback-iSCSI für einen vom Speicher Replikat replizierten asymmetrischen Cluster verwendet. Dies hat jedoch wahrscheinlich eine sehr schlechte Leistung und sollte nur für sehr begrenzte Workloads oder Tests verwendet werden.

## <a name="how-do-i-see-the-progress-of-replication-during-initial-sync"></a><a name="FAQ2"></a>Gewusst wie den Fortschritt der Replikation während der ersten Synchronisierung anzeigen?
Die auf dem Zielserver im Ereignisprotokoll für die Speicherreplikatverwaltung angezeigte Ereignismeldung 1237 zeigt alle 10 Sekunden die Anzahl der kopierten Bytes sowie die Anzahl von verbleibenden Bytes an. Sie können auch den Speicherreplikat-Leistungsindikator auf dem Ziel verwenden, der **\Speicherreplikatstatistik\Gesamtzahl empfangener Bytes** für mindestens ein repliziertes Volume anzeigt. Die Replikationsgruppe kann auch mithilfe von Windows PowerShell abgefragt werden. Über diesen Beispielbefehl wird z.B. der Name der Gruppen auf dem Ziel abgerufen und die Gruppe **Replication 2** alle 10 Sekunden abgefragt, um den Fortschritt anzuzeigen:

```
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```

## <a name="can-i-specify-specific-network-interfaces-to-be-used-for-replication"></a><a name="FAQ3"></a>Kann ich bestimmte Netzwerkschnittstellen für die Replikation angeben?

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

```
Set-SRNetworkConstraint -SourceComputerName sr-cluster01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-cluster02 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"
```

## <a name="can-i-configure-one-to-many-replication-or-transitive-a-to-b-to-c-replication"></a><a name="FAQ4"></a>Kann ich die 1: n-Replikation oder transitiv Replikation (A zu B zu C) konfigurieren?
Nein, das Speicher Replikat unterstützt nur eine Replikation eines Servers, Clusters oder eines Stretch-Cluster Knotens. In einem späteren Release kann sich dies ändern. Sie können natürlich eine Replikation zwischen verschiedenen Servern eines bestimmten Volume-Paars in beide Richtungen konfigurieren. Beispielsweise kann Server 1 sein D-Volume an Server 2, und sein E-Volume von Server 3 replizieren.

## <a name="can-i-grow-or-shrink-replicated-volumes-replicated-by-storage-replica"></a><a name="FAQ5"></a>Kann ich replizierte Volumes vergrößern oder verkleinern, die vom Speicher Replikat repliziert werden
Volumes können vergrößert (erweitert), aber nicht verkleinert werden. Standardmäßig verhindert das Speicher Replikat, dass Administratoren replizierte Volumes erweitern. verwenden `Set-SRGroup -AllowVolumeResize $TRUE` Sie die Option für die Quell Gruppe, bevor Sie die Größe ändern. Beispiel:

1. Verwendung für den Quellcomputer:`Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. Erweitern Sie das Volume mit der von Ihnen bevorzugten Methode.
3. Verwendung für den Quellcomputer:`Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE`

## <a name="can-i-bring-a-destination-volume-online-for-read-only-access"></a><a name="FAQ6"></a>Kann ich ein Zielvolume ausschließlich für den schreibgeschützten Zugriff online schalten?
Nicht in Windows Server 2016. Beim Start der Replikation wird das Ziel Volume von Speicher Replikaten getrennt.

In Windows Server 2019 und dem halbjährlichen Channel von Windows Server ab Version 1709 ist die Option zum Einbinden des Ziel Speichers nun jedoch möglich. diese Funktion wird als "Test Failover" bezeichnet. Zu diesem Zweck benötigen Sie ein nicht verwendetes, NTFS-oder Refs-formatiertes Volume, das derzeit nicht auf dem Ziel Replikat verwendet wird. Anschließend können Sie eine Momentaufnahme des replizierten Speichers temporär für Test-oder Sicherungszwecke einbinden.

So erstellen Sie z. b. ein Test Failover, bei dem Sie ein Volume "D:" in der Replikations Gruppe "RG2" auf dem Zielserver "SRV2" replizieren und ein Laufwerk "T:" auf SRV2 haben, das nicht repliziert wird:

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`

Auf das replizierte Volume "D:" kann jetzt über SRV2 zugegriffen werden. Sie können in diesem Fall Lese-und Schreibvorgänge ausführen, Dateien aus dem Verzeichnis kopieren oder eine Online Sicherung ausführen, die Sie an anderer Stelle für die Aufbewahrung speichern (unter dem Pfad "D:"). Das Volume "T:" enthält nur Protokolldaten.

So entfernen Sie die Test-failovermomentaufnahme und verwerfen die Änderungen:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`

Sie sollten die Funktion "Test Failover" nur für kurzfristige temporäre Vorgänge verwenden. Sie ist nicht für die langfristige Verwendung vorgesehen. Wenn die Replikation verwendet wird, wird die Replikation mit dem tatsächlichen Ziel Volume fortgesetzt

## <a name="can-i-configure-scale-out-file-server-sofs-in-a-stretch-cluster"></a><a name="FAQ7"></a>Kann ich einen Datei Server mit horizontaler Skalierung (sofs) in einem Stretch-Cluster konfigurieren?
Obwohl es technisch möglich ist, ist dies keine empfohlene Konfiguration, weil die Computeknoten, die mit dem sofs kontaktiert werden, nicht über die Standortinformationen verfügen. Bei Verwendung von Campus-Entfernungs Netzwerken, bei denen Wartezeiten in der Regel unter Millisekunden liegen, funktioniert diese Konfiguration in der Regel ohne Probleme.

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).

## <a name="is-csv-required-to-replicate-in-a-stretch-cluster-or-between-clusters"></a><a name="FAQ7.5"></a>Muss CSV in einem Stretch-Cluster oder zwischen Clustern repliziert werden?
Nein. Sie können eine Replikation mit einer CSV-oder persistenten Datenträger Reservierung (PDR) im Besitz einer Cluster Ressource (z. b. einer Datei Server Rolle) durch

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).

## <a name="can-i-configure-storage-spaces-direct-in-a-stretch-cluster-with-storage-replica"></a><a name="FAQ8"></a>Kann ich direkte Speicherplätze in einem Stretched Cluster mit Speicherreplikaten konfigurieren?
Dies ist keine unterstützte Konfiguration in Windows Server. In einem späteren Release kann sich dies ändern. Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature volle Unterstützung für Dateiserver mit horizontaler Skalierung und Hyper-V-Server (einschließlich Verwendung von direkten Speicherplätzen).

## <a name="how-do-i-configure-asynchronous-replication"></a><a name="FAQ9"></a>Wie konfiguriere ich die asynchrone Replikation?

Geben Sie `New-SRPartnership -ReplicationMode` und das Argument **Asynchronous** an. Standardmäßig wird jede Replikation im Speicherreplikatfeature synchron ausgeführt. Sie können den Modus auch mit `Set-SRPartnership -ReplicationMode` ändern.

## <a name="how-do-i-prevent-automatic-failover-of-a-stretch-cluster"></a><a name="FAQ10"></a>Wie verhindere ich das automatische Failover eines Stretched Clusters?
Um ein automatisches Failover zu verhindern, können Sie `Get-ClusterNode -Name "NodeName").NodeWeight=0` mithilfe von PowerShell konfigurieren. Dadurch wird die Abstimmung auf den einzelnen Knoten am Notfallwiederherstellungsstandort entfernt. Anschließend können Sie `Start-ClusterNode -PreventQuorum` auf Knoten am primären Standort und `Start-ClusterNode -ForceQuorum` auf Knoten am Notfallstandort verwenden, um ein Failover zu erzwingen. Es ist keine grafische Option verfügbar, um ein automatisches Failover zu verhindern, und das Verhindern des automatischen Failovers wird nicht empfohlen.

## <a name="how-do-i-disable-virtual-machine-resiliency"></a><a name="FAQ11"></a>Wie deaktiviere ich VM-Resilienz?

Führen Sie aus, um zu verhindern, dass die neue resilienzfunktion der virtuellen Hyper-V-Computer ausgeführt wird und daher virtuelle Computer angehalten werden, anstatt Sie an den Notfall Wiederherstellungs Standort zu übergeben.`(Get-Cluster).ResiliencyDefaultPeriod=0`

## <a name="how-can-i-reduce-time-for-initial-synchronization"></a><a name="FAQ12"></a>Wie kann ich die Zeit für die anfängliche Synchronisierung verkürzen?

Eine Möglichkeit, die Dauer der ersten Synchronisierung zu verkürzen, bietet die schlanke Speicherzuweisung. Das Speicherreplikatfeature führt eine Abfrage nach Speicher mit schlanker Zuweisung durch und verwendet diesen Speicher automatisch (einschließlich nicht gruppierter Speicherplätze, dynamischer Hyper-V-Datenträger und SAN-LUNs).

Sie können auch Datenvolumes mit Seeding verwenden, um die Bandbreitennutzung zu reduzieren, und gelegentlich Zeit, indem Sie sicherstellen, dass das Ziel Volume über eine Teilmenge der Daten vom primären Replikat verfügt, und die Option Seeding in Failovercluster-Manager oder verwenden `New-SRPartnership` . Wenn das Volume überwiegend leer ist, kann mit einer Seeding-Synchronisierung die Nutzung von Zeit und Bandbreite reduziert werden. Es gibt mehrere Möglichkeiten zum Seed von Daten mit unterschiedlichen Wirkungsgraden:

1. Vorherige Replikation: durch Replizieren der normalen anfänglichen Synchronisierung zwischen Knoten mit den Datenträgern und Volumes, Entfernen der Replikation, Versenden der Ziel Datenträger an andere Orte und anschließendes Hinzufügen der Replikation mit der Option Seeding Dies ist die effektivste Methode, da das Speicher Replikat eine Block Kopier Spiegelung garantiert und nur Delta Blöcke repliziert werden müssen.
2. Wiederhergestellte Momentaufnahme oder wiederhergestellte Momentaufnahme basierte Sicherung: indem Sie eine volumebasierte Momentaufnahme auf dem Ziel Volume wiederherstellen, sollte das Block Layout minimal unterschieden werden. Dies ist die nächst effektivste Methode, da Blöcke wahrscheinlich aufgrund von volumemomentaufnahmen mit Spiegelungs Bildern identisch sind.
3. Kopierte Dateien: durch Erstellen eines neuen Volumes auf dem Ziel, das noch nie verwendet wurde, und Durchführen einer vollständigen Robocopy/mir Tree-Kopie der Daten, sind wahrscheinlich Block Übereinstimmungen vorhanden. Wenn Sie den Windows-Datei-Explorer verwenden oder einen Teil der Struktur kopieren, werden nicht viele Block Übereinstimmungen erstellt. Das manuelle Kopieren von Dateien ist die am wenigsten effektive Methode für das Seeding.

## <a name="can-i-delegate-users-to-administer-replication"></a><a name="FAQ13"></a>Kann ich Benutzer zur Verwaltung der Replikation delegieren?

Sie können das `Grant-SRDelegation` Cmdlet verwenden. Mit diesem Cmdlet können Sie bestimmte Benutzer in Server-zu-Server-, Cluster-zu-Cluster- und Stretched Cluster-Replikationsszenarien festlegen, die über die Berechtigungen zum Erstellen, Ändern oder Entfernen der Replikation verfügen, ohne Mitglied der lokalen Administratorengruppe zu sein. Beispiel:

```
Grant-SRDelegation -UserName contso\tonywang
```

Das Cmdlet weist Sie darauf hin, dass der Benutzer sich beim zu verwaltenden Server ab- und erneut anmelden muss, damit die Änderungen wirksam werden. Diese Konfiguration kann mithilfe von `Get-SRDelegation` und `Revoke-SRDelegation` weiter gesteuert werden.

## <a name="what-are-my-backup-and-restore-options-for-replicated-volumes"></a><a name="FAQ13"></a>Welche Sicherungs-und Wiederherstellungsoptionen sind für replizierte Volumes verfügbar?

Das Speicherreplikatfeature unterstützt das Sichern und Wiederherstellen des Quellvolumes. Es bietet außerdem Unterstützung für das Erstellen und Wiederherstellen von Momentaufnahmen des Quellvolumes. Das Zielvolume kann nicht gesichert oder wiederhergestellt werden, während es durch das Speicherreplikatfeature geschützt ist. Es ist weder bereitgestellt, noch kann darauf zugegriffen werden. Bei Verlust des Quellvolumes in einem Notfallszenario können Sie mithilfe von `Set-SRPartnership` das vorherige Zielvolume als lesbare und beschreibbare Quelle festlegen, um dieses Volume sichern und wiederherstellen zu können. Sie können die Replikation auch mit `Remove-SRPartnership` und `Remove-SRGroup` entfernen, um das Volume als lesbares und beschreibbares Volume erneut bereitzustellen.

Für eine regelmäßige Erstellung von anwendungskonsistenten Momentaufnahmen können Sie VSSADMIN.EXE auf dem Quellserver ausführen, um Momentaufnahmen der replizierten Datenvolumes zu erstellen. Beispiel für die Replikation des Volumes F: mit dem Speicherreplikatfeature:

```
vssadmin create shadow /for=F:
```

Anschließend können Sie eine beliebige Momentaufnahme wiederherstellen, nachdem Sie die Replikationsrichtung geändert oder die Replikation entfernt haben bzw. wenn Sie weiterhin dasselbe Quellvolume verwenden. Beispiel, wenn Sie weiterhin F: verwenden:

```
vssadmin list shadows
vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
```

Mithilfe eines geplanten Tasks können Sie auch die regelmäßige Ausführung dieses Tools planen. Weitere Informationen zur Verwendung von VSS finden Sie unter [Vssadmin](../../administration/windows-commands/vssadmin.md). Das Sichern der Protokollvolumes ist nicht notwendig oder sinnvoll. Der Versuch, diesen Vorgang auszuführen, wird von VSS ignoriert.

Das Speicherreplikatfeature unterstützt die Verwendung von Windows Server-Sicherung, Microsoft Azure Backup, Microsoft DPM oder anderen Momentaufnahme-, VSS-, VM- oder dateibasierten Technologien, sofern diese auf Volume-Ebene eingesetzt werden. Das Speicherreplikatfeature bietet keine Unterstützung für blockbasierte Sicherungen und Wiederherstellungen.

## <a name="can-i-configure-replication-to-restrict-bandwidth-usage"></a><a name="FAQ14"></a>Kann ich die Replikation konfigurieren, um die Bandbreitennutzung einzuschränken?

Ja, über die SMB-Bandbreiteneinschränkung. Diese globale Einstellung gilt für den gesamten Speicherreplikatdatenverkehr und wirkt sich daher auf sämtliche Replikationsvorgänge von diesem Server aus. Dies ist üblicherweise nur bei der Einrichtung der ersten Speicherreplikatsynchronisierung erforderlich, bei der sämtliche Volumedaten übertragen werden müssen. Wenn eine solche Einschränkung nach der ersten Synchronisierung erforderlich ist, ist Ihre Netzwerkbandbreite zu gering für Ihre E/A-Workload. Reduzieren Sie E/A, oder erhöhen Sie die Bandbreite.

Diese Einstellung sollte nur bei der asynchronen Replikation verwendet werden. Hinweis: Die erste Synchronisierung erfolgt selbst dann immer asynchron, wenn Sie eine synchrone Replikation festgelegt haben.
Sie können auch die QoS-Netzwerkrichtlinien verwenden, um den Speicherreplikatdatenverkehr einzuschränken. Bei Verwendung der Speicherreplikatreplikation mit durchgeführtem Seeding mit großer Übereinstimmung wird die Bandbreitennutzung bei der ersten Synchronisierung ebenfalls erheblich reduziert.

So legen Sie die Bandbreiteneinschränkung fest:

```
Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x
```

So zeigen Sie die Bandbreiteneinschränkung an:

```
Get-SmbBandwidthLimit -Category StorageReplication
```

So entfernen Sie die Bandbreiteneinschränkung:

```
Remove-SmbBandwidthLimit -Category StorageReplication
```

## <a name="what-network-ports-does-storage-replica-require"></a><a name="FAQ15"></a>Welche Netzwerkports werden von Speicher Replikaten benötigt?

Das Speicher Replikat ist für die Replikation und Verwaltung von SMB und WSMAN abhängig. Dies bedeutet, dass die folgenden Ports erforderlich sind:

- 445 (SMB-Replikations Transportprotokoll, Cluster-RPC-Verwaltungs Protokoll)
- 5445 (IWarp SMB-nur erforderlich, wenn IWarp RDMA-Netzwerk verwendet wird)
- 5985 (wsmanhttp-Management-Protokoll für WMI/CIM/PowerShell)

> ! Nebenbei Für das Cmdlet "Test-srtopology" ist ICMPv4/ICMPv6 erforderlich, aber nicht für die Replikation oder Verwaltung.

## <a name="what-are-the-log-volume-best-practices"></a><a name="FAQ15.5"></a>Was sind die bewährten Methoden für das Protokoll Volume?

Die optimale Größe des Protokolls variiert in Abhängigkeit von der Umgebung und der Arbeitsauslastung. es hängt davon ab, wie viel Schreib-e/a die Arbeitsauslastung ausführt.

1. Ein größeres oder kleineres Protokoll führt Sie nicht schneller oder langsamer aus
2. Ein größeres oder kleineres Protokoll hat keine Auswirkungen auf ein 10-GB-Datenvolumen im Vergleich zu einem Datenvolumen von 10 TB, z.b.

Bei einem größeren Protokoll werden Schreibvorgänge für IOS einfach erfasst und beibehalten, bevor Sie verpackt werden. Dies ermöglicht eine Dienst Unterbrechung zwischen dem Quell-und Zielcomputer – z. b. einem Netzwerkausfall oder dem offline geschalteten Zielcomputer. Wenn das Protokoll 10 Stunden Schreibvorgänge enthalten kann und das Netzwerk zwei Stunden ausfällt, kann die Quelle, wenn das Netzwerk zurückgibt, einfach das Delta der nicht Synchronisierungs Änderungen wieder zum Ziel wiedergeben, und Sie werden sehr schnell geschützt. Wenn das Protokoll 10 Stunden umfasst und der Ausfall 2 Tage beträgt, muss die Quelle nun aus einem anderen Protokoll wiedergegeben werden, das als Bitmap – bezeichnet wird und wahrscheinlich langsamer ist, um synchron zu werden. Sobald die Synchronisierung durchführt, wird das Protokoll zurückgegeben.

Das Speicher Replikat basiert auf dem Protokoll für die gesamte Schreibleistung. Protokollieren Sie die Leistung für die Replikations Leistung. Sie müssen sicherstellen, dass das Protokoll Volume besser als das Datenvolumen ist, da das Protokoll alle Schreib-e/a-Vorgänge serialisieren und sequenzialisieren soll. Sie sollten immer Flash Medien wie SSD für Protokollvolumes verwenden. Sie dürfen niemals zulassen, dass alle anderen Arbeits Auslastungen auf dem Protokoll Volume ausgeführt werden, und zwar auf dieselbe Weise, wie Sie niemals zulassen, dass andere Workloads auf Protokoll Volumes der SQL-Datenbank ausgeführt werden.

Auch hier: Microsoft empfiehlt dringend, dass der Protokoll Speicher schneller ist als der Datenspeicher, und dass Protokollvolumes nie für andere Workloads verwendet werden müssen.

Sie können die Empfehlungen für die Protokoll Größe durch Ausführen des Tools Test-srtopology erhalten. Alternativ können Sie Leistungsindikatoren auf vorhandenen Servern verwenden, um ein Urteil zur Protokoll Größe zu erstellen. Die Formel ist einfach: Überwachen Sie den Datenträger Durchsatz (durchschnittliche geschriebene Bytes/Sek.) unter der Arbeitsauslastung, und verwenden Sie ihn, um die Zeitspanne zu berechnen, die zum Auffüllen des Protokolls mit unterschiedlichen Größen benötigt wird. Beispielsweise bewirkt der Datenträger Durchsatz von 50 MB/s, dass das Protokoll mit 120 GB in 120GB/50 MB Sekunden oder 2400 Sekunden oder 40 Minuten eingeschlossen wird. Daher ist die Zeitspanne, in der der Zielserver nicht erreichbar sein kann, bevor das umschließen des Protokolls 40 Minuten beträgt. Wenn das Protokoll umbrochen wird, das Ziel jedoch wieder erreichbar ist, würde die Quelle Blöcke über das Bitmap-Protokoll anstelle des Haupt Protokolls wiedergeben. Die Größe des Protokolls hat keine Auswirkung auf die Leistung.

Nur der Datenträger aus dem Quell Cluster muss gesichert werden. Die Protokoll Datenträger für Speicher Replikate sollten nicht gesichert werden, da eine Sicherung mit Speicher Replikat Vorgängen in Konflikt steht

## <a name="why-would-you-choose-a-stretch-cluster-versus-cluster-to-cluster-versus-server-to-server-topology"></a><a name="FAQ16"></a>Warum sollten Sie einen Stretch-Cluster und eine Cluster-zu-Server-Topologie oder eine Server-zu-Server-Topologie auswählen?

Das Speicher Replikat ist in drei Haupt Konfigurationen verfügbar: Stretch Cluster, Cluster-zu-Cluster und Server-zu-Server. Es gibt unterschiedliche Vorteile.

Die Stretch-Cluster Topologie eignet sich ideal für Workloads, für die ein automatisches Failover mit Orchestrierung erforderlich ist, z. b. Hyper-V-Private Cloud Cluster und SQL Server FCI. Es verfügt außerdem über eine integrierte grafische Oberfläche, die Failovercluster-Manager verwendet. Dabei wird die Architektur des klassischen asymmetrischen Cluster Speichers von Speicherplätzen, San, iSCSI und RAID über eine persistente Reservierung verwendet. Dies kann mit nur zwei Knoten ausgeführt werden.

Die Cluster-zu-Cluster-Topologie verwendet zwei separate Cluster und eignet sich ideal für Administratoren, die ein manuelles Failover wünschen, insbesondere wenn der zweite Standort für die Notfall Wiederherstellung und nicht für die tägliche Nutzung bereitgestellt wird. Die Orchestrierung ist manuell. Im Gegensatz zu Stretch-Clustern können direkte Speicherplätze in dieser Konfiguration verwendet werden (mit Einschränkungen). Weitere Informationen finden Sie in den FAQ zu Storage-Replikaten und der Cluster-zu-Cluster-Dokumentation. Dies kann mit nur vier Knoten ausgeführt werden.

Die Server-zu-Server-Topologie eignet sich ideal für Kunden, die Hardware ausführen, die nicht gruppiert werden kann. Hierfür sind manuelles Failover und Orchestrierung erforderlich. Sie eignet sich ideal für kostengünstige bereit Stellungen zwischen Zweigstellen und zentralen Rechenzentren, insbesondere bei Verwendung der asynchronen Replikation. Diese Konfiguration kann häufig Instanzen von DFSR-geschützten Dateiservern ersetzen, die für Notfall Wiederherstellungs Szenarien mit einem einzelnen Master verwendet werden.

In allen Fällen unterstützen die Topologien sowohl die Ausführung auf physischer Hardware als auch auf virtuellen Computern. Bei virtuellen Computern benötigt der zugrunde liegende Hypervisor keine Hyper-V. Dabei kann es sich um VMware, KVM, xen usw. handeln.

Das Speicher Replikat verfügt auch über einen Server-zu-selbst-Modus, in dem Sie die Replikation auf zwei verschiedene Volumes auf demselben Computer verweisen.

## <a name="is-data-deduplication-supported-with-storage-replica"></a><a name="FAQ18"></a>Wird die Datendeduplizierung mit dem Speicher Replikat unterstützt?

Ja, die Datendeduplizierung wird mit dem Speicher Replikat unterstützt. Aktivieren Sie die Datendeduplizierung auf einem Volume auf dem Quell Server. während der Replikation erhält der Zielserver eine deduplizierte Kopie des Volumes.

Obwohl Sie die Datendeduplizierung sowohl auf dem Quell-als auch auf dem Zielserver *Installieren* sollten (siehe [Installieren und Aktivieren der Datendeduplizierung](../data-deduplication/install-enable.md)), ist es wichtig, die Datendeduplizierung auf dem Zielserver nicht zu *aktivieren* . Speicher Replikate erlauben Schreibvorgänge nur auf dem Quell Server. Da die Datendeduplizierung Schreibvorgänge auf dem Volume durchführt, sollte Sie nur auf dem Quell Server ausgeführt werden.

## <a name="can-i-replicate-between-windows-server-2019-and-windows-server-2016"></a><a name="FAQ19"></a>Kann ich zwischen Windows Server 2019 und Windows Server 2016 replizieren?

Leider wird das Erstellen einer *neuen* Partnerschaft zwischen Windows Server 2019 und Windows Server 2016 nicht unterstützt. Sie können einen Server oder Cluster, auf dem Windows Server 2016 ausgeführt wird, sicher auf Windows Server 2019 aktualisieren, und alle *vorhandenen* Partnerschaften werden weiterhin funktionieren.

Um jedoch die verbesserte Replikations Leistung von Windows Server 2019 zu erzielen, müssen alle Mitglieder der Partnerschaft Windows Server 2019 ausführen, und Sie müssen vorhandene Partnerschaften und zugehörige Replikations Gruppen löschen und anschließend mit Seeding Daten neu erstellen (entweder bei der Erstellung der Partnerschaft im Windows Admin Center oder mit dem Cmdlet New-srpartnership).

## <a name="how-do-i-report-an-issue-with-storage-replica-or-this-guide"></a><a name="FAQ17"></a>Gewusst wie melden Sie ein Problem mit dem Speicher Replikat oder diesem Handbuch?

Technische Unterstützung beim Speicher Replikat finden Sie in den [Microsoft-Foren](https://docs.microsoft.com/answers/index.html). Sie können in srfeed@microsoft.com dieser Dokumentation auch eine e-Mail mit Fragen zu Speicher Replikaten oder Problemen senden. Die [Allgemeine Windows Server-Feedback-Website](https://windowsserver.uservoice.com/forums/295047-general-feedback) wird für Entwurfs Änderungsanforderungen bevorzugt, da Sie Ihren Kollegen die Möglichkeit bietet, Support und Feedback für Ihre Ideen bereitzustellen.

## <a name="can-storage-replica-be-configured-to-replicate-in-both-directions"></a><a name="FAQ18"></a>Kann das Speicher Replikat für die Replikation in beide Richtungen konfiguriert werden?

Speicher Replikat ist eine unidirektionale Replikations Technologie.  Die Replikation erfolgt pro Volume nur von der Quelle zum Ziel.  Diese Richtung kann jederzeit rückgängig gemacht werden, ist jedoch immer noch in eine Richtung.  Dies bedeutet jedoch nicht, dass eine Gruppe von Volumes (Quelle und Ziel) nicht in einer Richtung repliziert werden kann und dass eine andere Gruppe von Laufwerken (Quelle und Ziel) in umgekehrter Richtung repliziert wird.  Beispielsweise möchten Sie, dass die Server-zu-Server-Replikation konfiguriert ist.  Server1 und Server2 verfügen jeweils über die Laufwerk Buchstaben L:, M:, N: und O: und Sie möchten Laufwerk M: von Server1 in Server2, aber Laufwerk O: Replizieren von server2 auf Server1 replizieren.  Dies ist möglich, solange die Protokoll Laufwerke für jede Gruppe getrennt werden. Das heißt,

- Server1 Source Laufwerk m: mit Quell Protokoll Laufwerk l: Replikation auf Server2 Ziellaufwerk m: mit Ziel Protokoll Laufwerk l:
- Server2 Source Laufwerk o: mit Quell Protokoll Laufwerk n: Replikation auf Server1 Ziellaufwerk o: mit Ziel Protokoll Laufwerk n:

## <a name="related-topics"></a>Verwandte Themen
- [Übersicht über Speicherreplikate](storage-replica-overview.md)
- [Stretch-Cluster Replikation mit frei gegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)
- [Replikation von Server zu Server Speicher](server-to-server-storage-replication.md)
- [Cluster-zu-Cluster Speicher Replikation](cluster-to-cluster-storage-replication.md)
- [Speicher Replikat: bekannte Probleme](storage-replica-known-issues.md)

## <a name="see-also"></a>Weitere Informationen
- [Speicherübersicht](../storage.yml)
- [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)
