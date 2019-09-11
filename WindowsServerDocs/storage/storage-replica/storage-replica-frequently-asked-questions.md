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
ms.openlocfilehash: 89676ba821b99d44865bc6f45c34c05edb771d9d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865259"
---
# <a name="frequently-asked-questions-about-storage-replica"></a>Häufig gestellte Fragen zu Speicherreplikaten

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

In diesem Thema erhalten Sie Antworten auf häufig gestellte Fragen (FAQs) zu Speicherreplikaten.

## <a name="FAQ1"></a>Wird das Speicher Replikat in Azure unterstützt?
Ja. Sie können die folgenden Szenarien mit Azure verwenden:

1. Server-zu-Server-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in einer oder zwei Rechenzentrums Fehler Domänen oder asynchron zwischen zwei separaten Regionen)
2. Asynchrone Server-zu-Server-Replikation zwischen Azure und lokal (über VPN oder Azure expressroute)
3. Cluster-zu-Cluster-Replikation in Azure (synchron oder asynchron zwischen IaaS-VMs in einer oder zwei Rechenzentrums Fehler Domänen oder asynchron zwischen zwei separaten Regionen)
4. Asynchrone Cluster-zu-Cluster-Replikation zwischen Azure und lokal (über VPN oder Azure expressroute)

Weitere Hinweise zum Gastclustering in Azure finden Sie unter: Bereitstellen von [IaaS-VM-Gast Clustern in Microsoft Azure](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

Wichtige Hinweise:

1. Azure unterstützt keine freigegebenen vhdx-Gastclustering. Daher müssen virtuelle Windows-Failovercluster-Computer iSCSI-Ziele für permanente Datenträger-Reservierungs Clustering oder direkte Speicherplätze für den klassischen freigegebenen Speicher verwenden.
2. Zum [Erstellen eines direkte Speicherplätze sofs-Clusters mit Speicher Replikat für die Notfall Wiederherstellung in Azure-Regionen](https://aka.ms/azure-storage-replica-cluster)gibt es Azure Resource Manager Vorlagen für direkte Speicherplätze-basiertes Speicher Replikat Cluster.  
3. Cluster-zu-Cluster-RPC-Kommunikation in Azure (erforderlich für die Cluster-APIs zum Gewähren von Zugriff zwischen Clustern) erfordert das Konfigurieren des Netzwerk Zugriffs für das CNO. Sie müssen den TCP-Port 135 und den dynamischen Bereich oberhalb des TCP-Ports 49152 zulassen. Referenz [zum Erstellen eines Windows Server-Failoverclusters auf Azure IaaS-VM – Teil 2 Netzwerk und Erstellung](https://blogs.technet.microsoft.com/askcore/2015/06/24/building-windows-server-failover-cluster-on-azure-iaas-vm-part-2-network-and-creation/).  
4. Es ist möglich, Gast Cluster mit zwei Knoten zu verwenden, bei denen jeder Knoten Loopback-iSCSI für einen vom Speicher Replikat replizierten asymmetrischen Cluster verwendet. Dies hat jedoch wahrscheinlich eine sehr schlechte Leistung und sollte nur für sehr begrenzte Workloads oder Tests verwendet werden.  

## <a name="FAQ2"></a>Gewusst wie den Fortschritt der Replikation während der ersten Synchronisierung anzeigen?  
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

## <a name="FAQ3"></a>Kann ich bestimmte Netzwerkschnittstellen angeben, die für die Replikation verwendet werden sollen?  

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

    Set-SRNetworkConstraint -SourceComputerName sr-cluster01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-cluster02 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"

## <a name="FAQ4"></a>Kann ich die 1: n-Replikation oder transitiv Replikation (A zu B zu C) konfigurieren?  
Nein, das Speicher Replikat unterstützt nur eine Replikation eines Servers, Clusters oder eines Stretch-Cluster Knotens. In einem späteren Release kann sich dies ändern. Sie können natürlich eine Replikation zwischen verschiedenen Servern eines bestimmten Volume-Paars in beide Richtungen konfigurieren. Beispielsweise kann Server 1 sein D-Volume an Server 2, und sein E-Volume von Server 3 replizieren.

## <a name="FAQ5"></a>Kann ich replizierte Volumes vergrößern oder verkleinern, die vom Speicher Replikat repliziert werden  
Sie können Volumes vergrößern (erweitern), aber nicht verkleinern. Speicherreplikate verhindern standardmäßig, dass Administratoren replizierte Volumes erweitern. Verwenden Sie die Option `Set-SRGroup -AllowVolumeResize $TRUE` in der Quellgruppe vor dem Ändern der Größe. Zum Beispiel:

1. Verwendung für den Quellcomputer:`Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. Vergrößern Sie das Volume mithilfe des bevorzugten Verfahrens
3. Verwendung für den Quellcomputer:`Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>Kann ich ein Zielvolume für den schreibgeschützten Zugriff online schalten?  
Nicht in Windows Server 2016. Das Speicherreplikat hebt das Zielvolumes bei Beginn der Replikation auf. 

In Windows Server 2019 und dem halbjährlichen Channel von Windows Server ab Version 1709 ist die Option zum Einbinden des Ziel Speichers nun jedoch möglich. diese Funktion wird als "Test Failover" bezeichnet. Dazu benötigen Sie ein nicht verwendetes NTFS oder ReFS-formatiertes Volume, das derzeit nicht auf dem Zielserver repliziert wird. Sie können dann eine Momentaufnahme des replizierten Speichers vorübergehend zu Test- und Sicherungszwecken bereitstellen. 

Geben Sie beispielsweise Folgendes ein, um ein Test-Failover zu erstellen, in dem Sie ein Volume "D:" in der Replikationsgruppe "RG2" auf dem Zielserver "SRV2" replizieren und das Laufwerk "T:" auf dem Computern SRV2 haben, das nicht repliziert wird:

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
Das replizierte Volume "D:" ist jetzt auf den Computern SRV2 verfügbar. Sie können in diesem Fall Lese-und Schreibvorgänge ausführen, Dateien aus dem Verzeichnis kopieren oder eine Online Sicherung ausführen, die Sie an anderer Stelle für die Aufbewahrung speichern (unter dem Pfad "D:"). Das Volume "T:" enthält nur Protokolldaten.

So entfernen Sie den Test-Failover-Snapshot und Verwerfen die Änderungen:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
Sie sollten die Funktion zum Testen des Failovers nur für kurzfristige temporäre Vorgänge verwenden. Sie ist nicht für die langfristige Verwendung vorgesehen. Bei der Durchführung läuft die Replikation auf dem tatsächlichen Zielvolume. 

## <a name="FAQ7"></a>Kann ich einen Datei Server mit horizontaler Skalierung (sofs) in einem Stretch-Cluster konfigurieren?  
Obwohl es technisch möglich ist, ist dies keine empfohlene Konfiguration, weil die Computeknoten, die mit dem sofs kontaktiert werden, nicht über die Standortinformationen verfügen. Bei Verwendung von Campus-Entfernungs Netzwerken, bei denen Wartezeiten in der Regel unter Millisekunden liegen, funktioniert diese Konfiguration in der Regel ohne Probleme.   

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ7.5"></a>Muss CSV in einem Stretch-Cluster oder zwischen Clustern repliziert werden?  
Nein. Sie können eine Replikation mit einer CSV-oder persistenten Datenträger Reservierung (PDR) im Besitz einer Cluster Ressource (z. b. einer Datei Server Rolle) durch 

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ8"></a>Kann ich direkte Speicherplätze in einem Stretch-Cluster mit Speicher Replikat konfigurieren?  
Dies ist keine unterstützte Konfiguration in Windows Server. In einem späteren Release kann sich dies ändern. Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature volle Unterstützung für Dateiserver mit horizontaler Skalierung und Hyper-V-Server (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ9"></a>Gewusst wie konfigurieren Sie die asynchrone Replikation?  

Geben Sie `New-SRPartnership -ReplicationMode` und das Argument **Asynchronous** an. Standardmäßig wird jede Replikation im Speicherreplikatfeature synchron ausgeführt. Sie können den Modus auch mit `Set-SRPartnership -ReplicationMode` ändern.  

## <a name="FAQ10"></a>Gewusst wie verhindern des automatischen Failovers eines Stretch-Clusters?  
Um ein automatisches Failover zu verhindern, können Sie `Get-ClusterNode -Name "NodeName").NodeWeight=0` mithilfe von PowerShell konfigurieren. Dadurch wird die Abstimmung auf den einzelnen Knoten am Notfallwiederherstellungsstandort entfernt. Anschließend können Sie `Start-ClusterNode -PreventQuorum` auf Knoten am primären Standort und `Start-ClusterNode -ForceQuorum` auf Knoten am Notfallstandort verwenden, um ein Failover zu erzwingen. Es ist keine grafische Option verfügbar, um ein automatisches Failover zu verhindern, und das Verhindern des automatischen Failovers wird nicht empfohlen.  

## <a name="FAQ11"></a>Gewusst wie die Resilienz virtueller Computer deaktivieren?
Führen Sie aus, um zu verhindern, dass die neue resilienzfunktion der virtuellen Hyper-V-Computer ausgeführt wird und daher virtuelle Computer angehalten werden, anstatt Sie an den Notfall Wiederherstellungs Standort zu übergeben.`(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a>Wie kann ich die Zeit für die anfängliche Synchronisierung verkürzen?

Eine Möglichkeit, die Dauer der ersten Synchronisierung zu verkürzen, bietet die schlanke Speicherzuweisung. Das Speicherreplikatfeature führt eine Abfrage nach Speicher mit schlanker Zuweisung durch und verwendet diesen Speicher automatisch (einschließlich nicht gruppierter Speicherplätze, dynamischer Hyper-V-Datenträger und SAN-LUNs).  

Sie können auch Datenvolumes mit Seeding verwenden, um die Bandbreitennutzung zu reduzieren, und gelegentlich Zeit, indem Sie sicherstellen, dass das Ziel Volume über eine Teilmenge der Daten vom primären Replikat verfügt, und die Option Seeding in Failovercluster-Manager oder `New-SRPartnership`verwenden. Wenn das Volume überwiegend leer ist, kann mit einer Seeding-Synchronisierung die Nutzung von Zeit und Bandbreite reduziert werden. Es gibt mehrere Möglichkeiten zum Seed von Daten mit unterschiedlichen Wirkungsgraden:

1. Vorherige Replikation: durch Replizieren der normalen anfänglichen Synchronisierung zwischen Knoten mit den Datenträgern und Volumes, Entfernen der Replikation, Versenden der Ziel Datenträger an andere Orte und anschließendes Hinzufügen der Replikation mit der Option Seeding Dies ist die effektivste Methode, da das Speicher Replikat eine Block Kopier Spiegelung garantiert und nur Delta Blöcke repliziert werden müssen.
2. Wiederhergestellte Momentaufnahme oder wiederhergestellte Momentaufnahme basierte Sicherung: indem Sie eine volumebasierte Momentaufnahme auf dem Ziel Volume wiederherstellen, sollte das Block Layout minimal unterschieden werden. Dies ist die nächst effektivste Methode, da Blöcke wahrscheinlich aufgrund von volumemomentaufnahmen mit Spiegelungs Bildern identisch sind.
3. Kopierte Dateien: durch Erstellen eines neuen Volumes auf dem Ziel, das noch nie verwendet wurde, und Durchführen einer vollständigen Robocopy/mir Tree-Kopie der Daten, sind wahrscheinlich Block Übereinstimmungen vorhanden. Wenn Sie den Windows-Datei-Explorer verwenden oder einen Teil der Struktur kopieren, werden nicht viele Block Übereinstimmungen erstellt. Das manuelle Kopieren von Dateien ist die am wenigsten effektive Methode für das Seeding.

## <a name="FAQ13"></a>Kann ich Benutzer zur Verwaltung der Replikation delegieren?  

Sie können das `Grant-SRDelegation` Cmdlet verwenden. Mit diesem Cmdlet können Sie bestimmte Benutzer in Server-zu-Server-, Cluster-zu-Cluster- und Stretched Cluster-Replikationsszenarien festlegen, die über die Berechtigungen zum Erstellen, Ändern oder Entfernen der Replikation verfügen, ohne Mitglied der lokalen Administratorengruppe zu sein. Zum Beispiel:  

    Grant-SRDelegation -UserName contso\tonywang  

Das Cmdlet weist Sie darauf hin, dass der Benutzer sich beim zu verwaltenden Server ab- und erneut anmelden muss, damit die Änderungen wirksam werden. Diese Konfiguration kann mithilfe von `Get-SRDelegation` und `Revoke-SRDelegation` weiter gesteuert werden.  

## <a name="FAQ13"></a>Welche Sicherungs-und Wiederherstellungsoptionen sind für replizierte Volumes verfügbar?
Das Speicherreplikatfeature unterstützt das Sichern und Wiederherstellen des Quellvolumes. Es bietet außerdem Unterstützung für das Erstellen und Wiederherstellen von Momentaufnahmen des Quellvolumes. Das Zielvolume kann nicht gesichert oder wiederhergestellt werden, während es durch das Speicherreplikatfeature geschützt ist. Es ist weder bereitgestellt, noch kann darauf zugegriffen werden. Bei Verlust des Quellvolumes in einem Notfallszenario können Sie mithilfe von `Set-SRPartnership` das vorherige Zielvolume als lesbare und beschreibbare Quelle festlegen, um dieses Volume sichern und wiederherstellen zu können. Sie können die Replikation auch mit `Remove-SRPartnership` und `Remove-SRGroup` entfernen, um das Volume als lesbares und beschreibbares Volume erneut bereitzustellen.
Für eine regelmäßige Erstellung von anwendungskonsistenten Momentaufnahmen können Sie VSSADMIN.EXE auf dem Quellserver ausführen, um Momentaufnahmen der replizierten Datenvolumes zu erstellen. Beispiel für die Replikation des Volumes F: mit dem Speicherreplikatfeature:

    vssadmin create shadow /for=F:
Anschließend können Sie eine beliebige Momentaufnahme wiederherstellen, nachdem Sie die Replikationsrichtung geändert oder die Replikation entfernt haben bzw. wenn Sie weiterhin dasselbe Quellvolume verwenden. Beispiel, wenn Sie weiterhin F: verwenden:

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
Mithilfe eines geplanten Tasks können Sie auch die regelmäßige Ausführung dieses Tools planen. Weitere Informationen zur Verwendung von VSS finden Sie unter [Vssadmin](../../administration/windows-commands/vssadmin.md). Das Sichern der Protokollvolumes ist nicht notwendig oder sinnvoll. Der Versuch, diesen Vorgang auszuführen, wird von VSS ignoriert.
Das Speicherreplikatfeature unterstützt die Verwendung von Windows Server-Sicherung, Microsoft Azure Backup, Microsoft DPM oder anderen Momentaufnahme-, VSS-, VM- oder dateibasierten Technologien, sofern diese auf Volume-Ebene eingesetzt werden. Das Speicherreplikatfeature bietet keine Unterstützung für blockbasierte Sicherungen und Wiederherstellungen.

## <a name="FAQ14"></a>Kann ich die Replikation konfigurieren, um die Bandbreitennutzung einzuschränken?
Ja, über die SMB-Bandbreiteneinschränkung. Diese globale Einstellung gilt für den gesamten Speicherreplikatdatenverkehr und wirkt sich daher auf sämtliche Replikationsvorgänge von diesem Server aus. Dies ist üblicherweise nur bei der Einrichtung der ersten Speicherreplikatsynchronisierung erforderlich, bei der sämtliche Volumedaten übertragen werden müssen. Wenn eine solche Einschränkung nach der ersten Synchronisierung erforderlich ist, ist Ihre Netzwerkbandbreite zu gering für Ihre E/A-Workload. Reduzieren Sie E/A, oder erhöhen Sie die Bandbreite.

Diese Einstellung sollte nur bei der asynchronen Replikation verwendet werden. Hinweis: Die erste Synchronisierung erfolgt selbst dann immer asynchron, wenn Sie eine synchrone Replikation festgelegt haben.
Sie können auch die QoS-Netzwerkrichtlinien verwenden, um den Speicherreplikatdatenverkehr einzuschränken. Bei Verwendung der Speicherreplikatreplikation mit durchgeführtem Seeding mit großer Übereinstimmung wird die Bandbreitennutzung bei der ersten Synchronisierung ebenfalls erheblich reduziert.


So legen Sie die Bandbreiteneinschränkung fest:

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

So zeigen Sie die Bandbreiteneinschränkung an:

    Get-SmbBandwidthLimit -Category StorageReplication

So entfernen Sie die Bandbreiteneinschränkung:

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>Welche Netzwerkports werden von Speicher Replikaten benötigt?
Speicherreplikate verwenden SMB und WSMAN für die Replikation und Verwaltung. Dies bedeutet, dass die folgenden Ports erforderlich sind:

 445 (SMB-Replication Transport Protocol, Cluster RPC Management Protocol) 5445 (IWarp SMB-nur bei Verwendung von IWarp RDMA-Netzwerk erforderlich) 5985 (wsmanhttp-Management-Protokoll für WMI/CIM/PowerShell)

Hinweis: Für das Cmdlet "Test-srtopology" ist ICMPv4/ICMPv6 erforderlich, aber nicht für die Replikation oder Verwaltung.

## <a name="FAQ15.5"></a>Was sind die bewährten Methoden für das Protokoll Volume?
Die optimale Größe des Protokolls variiert in Abhängigkeit von der Umgebung und der Arbeitsauslastung. es hängt davon ab, wie viel Schreib-e/a die Arbeitsauslastung ausführt. 

1.  Ein größeres oder kleineres Protokoll führt Sie nicht schneller oder langsamer aus
2.  Ein größeres oder kleineres Protokoll hat keine Auswirkungen auf ein 10-GB-Datenvolumen im Vergleich zu einem Datenvolumen von 10 TB, z.b.

Ein größeres Protokoll sammelt und bewahrt nur mehr Schreib-E/A-Auslastung auf, bevor es umschlossen wird. Dadurch wird die Unterbrechung des Diensts zwischen dem Quell- und Zielcomputer – z. B. ein Netzwerkausfall oder wenn der Zielcomputer offline ist - verlängert. Wenn das Protokoll 10 Stunden an Schreibvorgängen enthalten kann, und das Netzwerk für 2 Stunden ausfällt, kann der Quellcomputer nach erneutem Verbinden mit dem Netzwerk einfach das Delta der nicht synchronisierten Änderungen schnell zum Ziel zurückgeben, und Sie sind erneut sehr schnell geschützt. Wenn das Protokoll 10 Stunden enthält und der Ausfall 2 Tage beträgt, muss der Quellcomputer Daten aus einem anderen Protokoll zurückgeben, das Bitmap genannt wird – was wahrscheinlich langsamer ist, um zum Synchronisieren zurückzukehren. Wenn die Synchronisierung abgeschlossen ist, wird das Protokoll erneut verwendet.

Das Speicherreplikat nutzt das Protokoll für die gesamte Schreibleistung. Die Protokollleistung ist für die Replikationsleistung von entscheidender Bedeutung. Sie müssen sicherstellen, dass die Leistung des Protokollvolumens besser als die des Datenvolumens ist, da das Protokoll alle Schreib-E/A-Lasten serialisiert und sequenzialisiert. Sie sollten auf Protokollvolumes immer Flashmedien verwenden, z. B. SSD. Sie dürfen niemals zulassen, dass andere Workloads auf dem Protokollvolume ausgeführt werden, so wie Sie auch niemals zulassen würden, dass andere Workloads auf SQL-Datenbank-Protokollvolumes ausgeführt werden. 

Erneut Microsoft empfiehlt dringend, dass der Protokoll Speicher schneller ist als der Datenspeicher, und dass Protokollvolumes niemals für andere Arbeits Auslastungen verwendet werden müssen.

Sie können die Empfehlungen für die Protokoll Größe durch Ausführen des Tools Test-srtopology erhalten. Alternativ können Sie Leistungsindikatoren auf vorhandenen Servern verwenden, um ein Urteil zur Protokoll Größe zu erstellen. Die Formel ist einfach: Überwachen Sie den Datenträger Durchsatz (durchschnittliche geschriebene Bytes/Sek.) unter der Arbeitsauslastung, und verwenden Sie ihn, um die Zeitspanne zu berechnen, die zum Auffüllen des Protokolls mit unterschiedlichen Größen benötigt wird. Beispielsweise bewirkt der Datenträger Durchsatz von 50 MB/s, dass das Protokoll mit 120 GB in 120GB/50 MB Sekunden oder 2400 Sekunden oder 40 Minuten eingeschlossen wird. Daher ist die Zeitspanne, in der der Zielserver nicht erreichbar sein kann, bevor das umschließen des Protokolls 40 Minuten beträgt. Wenn das Protokoll umbrochen wird, das Ziel jedoch wieder erreichbar ist, würde die Quelle Blöcke über das Bitmap-Protokoll anstelle des Haupt Protokolls wiedergeben. Die Größe des Protokolls hat keine Auswirkung auf die Leistung.

Nur der Datenträger aus dem Quell Cluster muss gesichert werden. Die Protokoll Datenträger für Speicher Replikate sollten nicht gesichert werden, da eine Sicherung mit Speicher Replikat Vorgängen in Konflikt steht

## <a name="FAQ16"></a>Warum sollten Sie einen Stretch-Cluster und eine Cluster-zu-Server-Topologie oder eine Server-zu-Server-Topologie auswählen?  
Das Speicher Replikat ist in drei Haupt Konfigurationen verfügbar: Stretch Cluster, Cluster-zu-Cluster und Server-zu-Server. Jede bietet verschiedene Vorteile.

Die Stretched Cluster-Topologie ist ideal für Auslastungen, die automatisches Failover mit Orchestrierung wie z. B. private Hyper-V-Cloud-Cluster und SQL Server-Failoverclusterinstanzen erfordern. Es verfügt außerdem über eine integrierte Benutzeroberfläche, die den Failovercluster-Manager verwendet. Sie verwendet die klassische asymmetrische gemeinsam genutzte Cluster Speicherarchitektur von Speicherplätzen, SAN, iSCSI und RAID-Reservierungssemantik. Sie können dies mit nur 2 Knoten ausführen.

Die Cluster-zu-Cluster-Topologie verwendet zwei separate Cluster und eignet sich besonders für Administratoren, die manuelles Failover möchten, insbesondere, wenn der zweite Speicherort für die Notfallwiederherstellung und nicht die alltägliche Verwendung konfiguriert ist. Die Orchestrierung erfolgt manuell. Im Gegensatz zu Stretch-Clustern können direkte Speicherplätze in dieser Konfiguration verwendet werden (mit Einschränkungen). Weitere Informationen finden Sie in den FAQ zu Storage-Replikaten und der Cluster-zu-Cluster-Dokumentation. Sie können dies mit nur 4 Knoten ausführen. 

Die Server-zu-Server-Topologie ist ideal für Kunden mit Hardware, die nicht als Clustern gruppiert werden kann. Sie erfordert manuelles Failover und Orchestrierung. Sie eignet sich ideal für kostengünstige bereit Stellungen zwischen Zweigstellen und zentralen Rechenzentren, insbesondere bei Verwendung der asynchronen Replikation. Diese Konfiguration ersetzt häufig Instanzen von DFSR-geschützten Dateiservern, die für die Single Master Notfallwiederherstellungszenarien verwendet werden.

In allen Fällen kann die Topologie sowohl auf physischer Hardware als auch auf virtuellen Computern ausgeführt werden. In virtuellen Computern erfordert der zugrunde liegenden Hypervisor nicht Hyper-V und kann anstatt VMware, KVM, Xen verwenden.

Das Speicherreplikatfeature verfügt außerdem über einen Server-to-Self-Modus, in dem die Replikation auf zwei Volumes auf demselben Computer verweist.

## <a name="FAQ18"></a>Wird die Datendeduplizierung mit dem Speicher Replikat unterstützt?

Ja, die Datendeduplizierung wird mit dem Speicher Replikat unterstützt. Aktivieren Sie die Datendeduplizierung auf einem Volume auf dem Quell Server. während der Replikation erhält der Zielserver eine deduplizierte Kopie des Volumes.

Obwohl Sie die Datendeduplizierung sowohl auf dem Quell-als auch auf dem Zielserver *Installieren* sollten (siehe [Installieren und Aktivieren der Datendeduplizierung](../data-deduplication/install-enable.md)), ist es wichtig, die Datendeduplizierung auf dem Zielserver nicht zu *aktivieren* . Speicher Replikate erlauben Schreibvorgänge nur auf dem Quell Server. Da die Datendeduplizierung Schreibvorgänge auf dem Volume durchführt, sollte Sie nur auf dem Quell Server ausgeführt werden. 

## <a name="FAQ19"></a>Kann ich zwischen Windows Server 2019 und Windows Server 2016 replizieren?

Leider wird das Erstellen einer *neuen* Partnerschaft zwischen Windows Server 2019 und Windows Server 2016 nicht unterstützt. Sie können einen Server oder Cluster, auf dem Windows Server 2016 ausgeführt wird, sicher auf Windows Server 2019 aktualisieren, und alle *vorhandenen* Partnerschaften werden weiterhin funktionieren.

Um jedoch die verbesserte Replikations Leistung von Windows Server 2019 zu erzielen, müssen alle Mitglieder der Partnerschaft Windows Server 2019 ausführen, und Sie müssen vorhandene Partnerschaften und zugehörige Replikations Gruppen löschen und anschließend mit Seeding Daten neu erstellen (entweder beim Erstellen der Partnerschaft im Windows Admin Center oder mit dem New-srpartnership-Cmdlet).

## <a name="FAQ17"></a>Gewusst wie melden Sie ein Problem mit dem Speicher Replikat oder diesem Handbuch?  
Falls Sie technische Unterstützung für Speicherreplikate benötigen, können Sie Ihre Fragen in den [Microsoft TechNet-Foren](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview) stellen. Sie können uns auch eine E-Mail an srfeed@microsoft.com senden, wenn Sie Fragen zu Speicherreplikaten oder dieser Dokumentation haben. Die <https://windowsserver.uservoice.com> Website wird für Entwurfs Änderungsanforderungen bevorzugt, da Sie Ihren Kollegen die Möglichkeit bietet, Support und Feedback für Ihre Ideen bereitzustellen.



## <a name="related-topics"></a>Verwandte Themen  
- [Speicher Replikat](storage-replica-overview.md) 
- [Stretch-Cluster Replikation mit frei gegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Replikation von Server zu Server Speicher](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster Speicher Replikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikat: Bekannte Probleme](storage-replica-known-issues.md)  

## <a name="see-also"></a>Siehe auch  
- [Übersicht über den Speicher](../storage.md)  
- [Direkte Speicherplätze](../storage-spaces/storage-spaces-direct-overview.md)  
