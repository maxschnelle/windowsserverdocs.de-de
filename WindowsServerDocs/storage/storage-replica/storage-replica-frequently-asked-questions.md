---
title: "Häufig gestellte Fragen zu Speicherreplikaten"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 07/20/2017
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: f29ca24a39e00f5142fe700e6abb09d1673acf7b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="frequently-asked-questions-about-storage-replica"></a>Häufig gestellte Fragen zu Speicherreplikaten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema erhalten Sie Antworten auf häufig gestellte Fragen (FAQs) zu Speicherreplikaten.

## <a name="FAQ1"></a> Werden Speicherreplikate auf Nano Server unterstützt?  
Ja.  

> [!NOTE]
> Sie müssen bei der Einrichtung das Nano Server-Paket **Storage** verwenden. Weitere Informationen zur Bereitstellung von Nano Server finden Sie unter [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx) (Erste Schritte mit Nano Server).  

Nutzen Sie das PowerShell-Remoting wie folgt, um das Speicherreplikatfeature auf Nano Server zu installieren:  

1. Fügen Sie den Nano Server Ihrer Clientvertrauensliste hinzu.  
   > [!NOTE]
   > Dieser Schritt muss nur ausgeführt werden, wenn der Computer kein Mitglied einer Active Directory Domain Services-Gesamtstruktur ist oder sich in einer nicht vertrauenswürdigen Gesamtstruktur befindet. Über diesen Schritt wird NTLM-Unterstützung zum PSSession-Remoting hinzugefügt (dies ist aus Sicherheitsgründen standardmäßig deaktiviert). Weitere Informationen finden Sie unter [Sicherheitsaspekte von PowerShell-Remoting](https://msdn.microsoft.com/powershell/scriptiwinrmsecurity).  

   ```  
       Set-Item WSMan:\localhost\Client\TrustedHosts "<computer name of Nano Server>"  
   ```  
2.  Um das Speicherreplikatfeature zu installieren, führen Sie das folgende Cmdlet von einem Verwaltungscomputer aus:  

    ```  
    Install-windowsfeature -Name storage-replica,RSAT-Storage-Replica -ComputerName <nano server> -Restart -IncludeManagementTools  
    ```  

    Zur Verwendung des Cmdlets `Test-SRTopology` mit Nano Server in Windows Server 2016 muss ein Remoteskript mit CredSSP aufgerufen werden. Im Gegensatz zu anderen Speicherreplikat-Cmdlets muss `Test-SRTopology` lokal auf dem Quellserver ausgeführt werden.   
Auf dem Nano Server (über eine Remote-PSSession) :  

    >[!NOTE]
    >CREDSSP ist für Kerberos-Double-Hop-Unterstützung im Cmdlet `Test-SRTopology` erforderlich und wird von anderen Speicherreplikat-Cmdlets nicht benötigt, die verteilte Systemanmeldeinformationen automatisch verarbeiten. In typischen Szenarien wird die Verwendung von CREDSSP nicht empfohlen. Eine Alternative zu CREDSSP finden Sie im folgenden Blogbeitrag von Microsoft: „PowerShell Remoting Kerberos Double Hop Solved Securely (PowerShell Remoting Kerberos Double Hop sicher gelöst)“ - https://blogs.technet.microsoft.com/ashleymcglone/2016/08/30/powershell-remoting-kerberos-double-hop-solved-securely/ 

        Enable-WSManCredSSP -role server       

    Auf dem Verwaltungscomputer:  

         Enable-WSManCredSSP Client -DelegateComputer <remote server name>  

         $CustomCred = Get-Credential  

         Invoke-Command -ComputerName sr-srv01 -ScriptBlock { Test-SRTopology <commands> } -Authentication Credssp -Credential $CustomCred  

       Kopieren Sie die Ergebnisse anschließend auf Ihren Verwaltungscomputer, oder geben Sie den Pfad frei. Da Nano nicht über die erforderlichen grafischen Bibliotheken verfügt, können Sie Test-SRTopology verwenden, um die Ergebnisse zu verarbeiten und eine Berichtdatei mit Diagrammen zu erhalten. Beispiel:  

        Test-SRTopology -GenerateReport -DataPath \\sr-srv05\c$\temp  


## <a name="FAQ2"></a> Wie kann ich den Fortschritt der Replikation bei der ersten Synchronisierung anzeigen?  
Die auf dem Zielserver im Ereignisprotokoll für die Speicherreplikatverwaltung angezeigte Ereignismeldung1237 zeigt alle 10Sekunden die Anzahl der kopierten Bytes sowie die Anzahl von verbleibenden Bytes an. Sie können auch den Speicherreplikat-Leistungsindikator auf dem Ziel verwenden, der **\Speicherreplikatstatistik\Gesamtzahl empfangener Bytes** für mindestens ein repliziertes Volume anzeigt. Die Replikationsgruppe kann auch mithilfe von Windows PowerShell abgefragt werden. Über diesen Beispielbefehl wird z.B. der Name der Gruppen auf dem Ziel abgerufen und die Gruppe **Replication 2** alle 10Sekunden abgefragt, um den Fortschritt anzuzeigen:  

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

## <a name="FAQ4"></a> Kann ich eine 1:n-Replikation oder transitive Replikation (A zu B zu C) konfigurieren?  
Nicht in Windows Server 2016. Dieses Release unterstützt lediglich die 1:1-Replikation von Servern, Clustern oder Stretched Cluster-Knoten. In einem späteren Release kann sich dies ändern. Sie können natürlich eine Replikation zwischen verschiedenen Servern eines bestimmten Volume-Paars in beide Richtungen konfigurieren. Beispielsweise kann Server 1 sein D-Volume an Server 2, und sein E-Volume von Server 3 replizieren.

## <a name="FAQ5"></a> Kann ich replizierte Volumes, die mithilfe des Speicherreplikatfeatures repliziert wurden, vergrößern oder verkleinern?  
Sie können Volumes vergrößern (erweitern), aber nicht verkleinern. Speicherreplikate verhindern standardmäßig, dass Administratoren replizierte Volumes erweitern. Verwenden Sie die Option `Set-SRGroup -AllowVolumeResize $TRUE` in der Quellgruppe vor dem Ändern der Größe. Beispiel:

1. Verwenden für den Quellcomputer: `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. Vergrößern Sie das Volume mithilfe des bevorzugten Verfahrens
3. Verwenden für den Quellcomputer: `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>Kann ich ein Zielvolume ausschließlich für den schreibgeschützten Zugriff online schalten?  
Nicht in Windows Server2016-RTM, d. h. oder der sogenannten "RS1"-Version. Das Speicherreplikat hebt das Zielvolumes bei Beginn der Replikation auf. 

Allerdings ist jetzt in der Version 1709 von Windows Server die Option zum Bereitstellen des Zielspeichers möglich – dieses Feature wird "Test-Failover" genannt. Dazu benötigen Sie ein nicht verwendetes NTFS oder ReFS-formatiertes Volume, das derzeit nicht auf dem Zielserver repliziert wird. Sie können dann eine Momentaufnahme des replizierten Speichers vorübergehend zu Test- und Sicherungszwecken bereitstellen. 

Geben Sie beispielsweise Folgendes ein, um ein Test-Failover zu erstellen, in dem Sie ein Volume "D:" in der Replikationsgruppe "RG2" auf dem Zielserver "SRV2" replizieren und das Laufwerk "T:" auf dem Computern SRV2 haben, das nicht repliziert wird:

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
Das replizierte Volume "D:" ist jetzt auf den Computern SRV2 verfügbar. Sie können haben ganz normalen Schreib- und Lesezugriff, können Dateien daraus kopieren, oder eine Online-Sicherung durchführen, die Sie an einer anderen Stelle zur sicheren Verwahrung speichern.

So entfernen Sie den Test-Failover-Snapshot und Verwerfen die Änderungen:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
Sie sollten die Funktion zum Testen des Failovers nur für kurzfristige temporäre Vorgänge verwenden. Sie ist nicht für die langfristige Verwendung vorgesehen. Bei der Durchführung läuft die Replikation auf dem tatsächlichen Zielvolume. 

## <a name="FAQ7"></a>Kann ich einen Dateiserver mit horizontaler Skalierung in einem Stretched Cluster konfigurieren?  
Auch wenn es technisch möglich ist, ist dies keine empfohlene Konfiguration in Windows Server 2016. Der Grund dafür sind die nicht vorhandenen Standortinformationen in den Computeknoten, die SOFS kontaktieren. Bei Verwendung von Campusnetzwerken, in denen Wartezeiten typischerweise im Bereich unter Millisekunden liegen, funktioniert diese Konfiguration normalerweise ohne Probleme.   

Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature bei der Replikation zwischen zwei Clustern volle Unterstützung für Dateiserver mit horizontaler Skalierung (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ8"></a>Kann ich direkte Speicherplätze in einem Stretched Cluster mit Speicherreplikaten konfigurieren?  
Diese Konfiguration wird in Windows Server 2016 nicht unterstützt.  In einem späteren Release kann sich dies ändern. Bei der Konfiguration einer Cluster-zu-Cluster-Replikation bietet das Speicherreplikatfeature volle Unterstützung für Dateiserver mit horizontaler Skalierung und Hyper-V-Server (einschließlich Verwendung von direkten Speicherplätzen).  

## <a name="FAQ9"></a>Wie konfiguriere ich die asynchrone Replikation?  

Geben Sie `New-SRPartnership -ReplicationMode` und das Argument **Asynchronous** an. Standardmäßig wird jede Replikation im Speicherreplikatfeature synchron ausgeführt. Sie können den Modus auch mit `Set-SRPartnership -ReplicationMode` ändern.  

## <a name="FAQ10"></a>Wie verhindere ich das automatische Failover eines Stretched Clusters?  
Um ein automatisches Failover zu verhindern, können Sie `Get-ClusterNode -Name "NodeName").NodeWeight=0` mithilfe von PowerShell konfigurieren. Dadurch wird die Abstimmung auf den einzelnen Knoten am Notfallwiederherstellungsstandort entfernt. Anschließend können Sie `Start-ClusterNode -PreventQuorum` auf Knoten am primären Standort und `Start-ClusterNode -ForceQuorum` auf Knoten am Notfallstandort verwenden, um ein Failover zu erzwingen. Es ist keine grafische Option verfügbar, um ein automatisches Failover zu verhindern, und das Verhindern des automatischen Failovers wird nicht empfohlen.  

## <a name="FAQ11"></a>Wie deaktiviere ich VM-Resilienz?  
Um die Ausführung des neuen Hyper-V-VM-Resilienzfeatures zu verhindern und virtuelle Computer anzuhalten anstatt ein Failover auf den Notfallwiederherstellungsstandort durchzuführen, führen Sie folgenden Befehl aus: `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> Wie kann ich den Zeitaufwand für die erste Synchronisierung verkürzen?  

Eine Möglichkeit, die Dauer der ersten Synchronisierung zu verkürzen, bietet die schlanke Speicherzuweisung. Das Speicherreplikatfeature führt eine Abfrage nach Speicher mit schlanker Zuweisung durch und verwendet diesen Speicher automatisch (einschließlich nicht gruppierter Speicherplätze, dynamischer Hyper-V-Datenträger und SAN-LUNs).  

Sie können auch ein Seeding für Datenvolumes durchführen, um die Nutzung von Breitband und manchmal Zeit zu verringern, indem Sie sicherstellen, dass das Zielvolume über eine Untermenge an Daten des primären Standorts verfügt (über eine wiederhergestellte Sicherung, eine alte Momentaufnahme, eine vorherige Replikation, kopierte Dateien usw.). Anschließend verwenden Sie die Option für ein ausgeführtes Seeding im Failovercluster-Manager oder `New-SRPartnership`. Wenn das Volume überwiegend leer ist, kann mit einer Seeding-Synchronisierung die Nutzung von Zeit und Bandbreite reduziert werden.

## <a name="FAQ13"></a> Kann ich Benutzer für die Replikationsverwaltung delegieren?  

Sie können das Cmdlet `Grant-SRDelegation` in Windows Server 2016 verwenden. Mit diesem Cmdlet können Sie bestimmte Benutzer in Server-zu-Server-, Cluster-zu-Cluster- und Stretched Cluster-Replikationsszenarien festlegen, die über die Berechtigungen zum Erstellen, Ändern oder Entfernen der Replikation verfügen, ohne Mitglied der lokalen Administratorengruppe zu sein. Beispiel:  

    Grant-SRDelegation -UserName contso\tonywang  

Das Cmdlet weist Sie darauf hin, dass der Benutzer sich beim zu verwaltenden Server ab- und erneut anmelden muss, damit die Änderungen wirksam werden. Diese Konfiguration kann mithilfe von `Get-SRDelegation` und `Revoke-SRDelegation` weiter gesteuert werden.  

## <a name="FAQ13"></a> Welche Sicherungs- und Wiederherstellungsoptionen sind für replizierte Volumes verfügbar?
Das Speicherreplikatfeature unterstützt das Sichern und Wiederherstellen des Quellvolumes. Es bietet außerdem Unterstützung für das Erstellen und Wiederherstellen von Momentaufnahmen des Quellvolumes. Das Zielvolume kann nicht gesichert oder wiederhergestellt werden, während es durch das Speicherreplikatfeature geschützt ist. Es ist weder bereitgestellt, noch kann darauf zugegriffen werden. Bei Verlust des Quellvolumes in einem Notfallszenario können Sie mithilfe von `Set-SRPartnership` das vorherige Zielvolume als lesbare und beschreibbare Quelle festlegen, um dieses Volume sichern und wiederherstellen zu können. Sie können die Replikation auch mit `Remove-SRPartnership` und `Remove-SRGroup` entfernen, um das Volume als lesbares und beschreibbares Volume erneut bereitzustellen.
Für eine regelmäßige Erstellung von anwendungskonsistenten Momentaufnahmen können Sie VSSADMIN.EXE auf dem Quellserver ausführen, um Momentaufnahmen der replizierten Datenvolumes zu erstellen. Beispiel für die Replikation des Volumes F: mit dem Speicherreplikatfeature:

    vssadmin create shadow /for=F:
Anschließend können Sie eine beliebige Momentaufnahme wiederherstellen, nachdem Sie die Replikationsrichtung geändert oder die Replikation entfernt haben bzw. wenn Sie weiterhin dasselbe Quellvolume verwenden. Beispiel, wenn Sie weiterhin F: verwenden:

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
Mithilfe eines geplanten Tasks können Sie auch die regelmäßige Ausführung dieses Tools planen. Weitere Informationen zur Verwendung von VSS finden Sie unter [Vssadmin](https://technet.microsoft.com/library/cc754968.aspx). Das Sichern der Protokollvolumes ist nicht notwendig oder sinnvoll. Der Versuch, diesen Vorgang auszuführen, wird von VSS ignoriert.
Das Speicherreplikatfeature unterstützt die Verwendung von Windows Server-Sicherung, Microsoft Azure Backup, Microsoft DPM oder anderen Momentaufnahme-, VSS-, VM- oder dateibasierten Technologien, sofern diese auf Volume-Ebene eingesetzt werden. Das Speicherreplikatfeature bietet keine Unterstützung für blockbasierte Sicherungen und Wiederherstellungen.

## <a name="FAQ14"></a> Kann ich die Replikation für eine eingeschränkte Bandbreitennutzung konfigurieren?
Ja, über die SMB-Bandbreiteneinschränkung. Diese globale Einstellung gilt für den gesamten Speicherreplikatdatenverkehr und wirkt sich daher auf sämtliche Replikationsvorgänge von diesem Server aus. Dies ist üblicherweise nur bei der Einrichtung der ersten Speicherreplikatsynchronisierung erforderlich, bei der sämtliche Volumedaten übertragen werden müssen. Wenn eine solche Einschränkung nach der ersten Synchronisierung erforderlich ist, ist Ihre Netzwerkbandbreite zu gering für Ihre E/A-Workload. Reduzieren Sie E/A, oder erhöhen Sie die Bandbreite.

Diese Einstellung sollte nur bei der asynchronen Replikation verwendet werden. Hinweis: Die erste Synchronisierung erfolgt selbst dann immer asynchron, wenn Sie eine synchrone Replikation festgelegt haben.
Sie können auch die QoS-Netzwerkrichtlinien verwenden, um den Speicherreplikatdatenverkehr einzuschränken. Bei Verwendung der Speicherreplikatreplikation mit durchgeführtem Seeding mit großer Übereinstimmung wird die Bandbreitennutzung bei der ersten Synchronisierung ebenfalls erheblich reduziert.


So legen Sie die Bandbreiteneinschränkung fest:

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

So zeigen Sie die Bandbreiteneinschränkung an:

    Get-SmbBandwidthLimit -Category StorageReplication

So entfernen Sie die Bandbreiteneinschränkung:

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>Welche Netzwerkports sind für Speicherreplikate erforderlich?
Speicherreplikate verwenden SMB und WSMAN für die Replikation und Verwaltung. Dies bedeutet, dass die folgenden Ports erforderlich sind:

   445 (SMB – Transportprotokoll für die Replikation) 5445 (iWARP SMB – nur bei Verwendung von iWARP RDMA-Netzwerken erforderlich) 5895 (WSManHTTP – Verwaltungsprotokoll für WMI/CIM/PowerShell)

Hinweis: Das Cmdlet Test-SRTopology erfordert ICMPv4/ICMPv6, jedoch nicht für die Replikation oder Verwaltung.

## <a name="FAQ15"></a>Was sind die bewährten Methoden für das Protokollvolume?
Die optimale Größe des Ereignisprotokolls variiert je nach Umgebung und Arbeitsauslastung und wird dadurch bestimmt, wie viel Schreib-E/A-Auslastung ausgeführt wird. 

1.  Ein kleineres oder größeres Protokoll bestimmt nicht die Schnelligkeit
2.  Ein kleineres oder größeres Protokoll wirkt sich beispielsweise nicht auf das Datenvolume von 10GB im Gegensatz zu 10TB aus.

Ein größeres Protokoll sammelt und bewahrt nur mehr Schreib-E/A-Auslastung auf, bevor es umschlossen wird. Dadurch wird die Unterbrechung des Diensts zwischen dem Quell- und Zielcomputer – z.B. ein Netzwerkausfall oder wenn der Zielcomputer offline ist - verlängert. Wenn das Protokoll 10 Stunden an Schreibvorgängen enthalten kann, und das Netzwerk für 2 Stunden ausfällt, kann der Quellcomputer nach erneutem Verbinden mit dem Netzwerk einfach das Delta der nicht synchronisierten Änderungen schnell zum Ziel zurückgeben, und Sie sind erneut sehr schnell geschützt. Wenn das Protokoll 10 Stunden enthält und der Ausfall 2Tage beträgt, muss der Quellcomputer Daten aus einem anderen Protokoll zurückgeben, das Bitmap genannt wird – was wahrscheinlich langsamer ist, um zum Synchronisieren zurückzukehren. Wenn die Synchronisierung abgeschlossen ist, wird das Protokoll erneut verwendet.

SR-Leistungsindikatoren geben die Verarbeitungsrate des Protokolls an und ermöglichen Ihnen, sich ein Urteil zu verschaffen. Das Cmdlet „Test-SRTopology” ermöglicht dies ebenfalls. Im Grunde sehen Sie die Schreib-E/A einer vorhandenen Arbeitslast, um zu entscheiden, wie viel E/A vom Protokoll pro Minute, Stunde oder Tag verarbeitet werden soll.

Das Speicherreplikat nutzt das Protokoll für die gesamte Schreibleistung. Die Protokollleistung ist für die Replikationsleistung von entscheidender Bedeutung. Sie müssen sicherstellen, dass die Leistung des Protokollvolumens besser als die des Datenvolumens ist, da das Protokoll alle Schreib-E/A-Lasten serialisiert und sequenzialisiert. Sie sollten auf Protokollvolumes immer Flashmedien verwenden, z.B. SSD. Sie dürfen niemals zulassen, dass andere Workloads auf dem Protokollvolume ausgeführt werden, so wie Sie auch niemals zulassen würden, dass andere Workloads auf SQL-Datenbank-Protokollvolumes ausgeführt werden. 

Noch einmal: Microsoft empfiehlt dringend, dass die Protokollspeicherung schneller als die Datenspeicherung durchgeführt wird und dass die Protokolldateien nie für andere Auslastungen verwendet werden.

## <a name="FAQ16"></a> Warum würden Sie einen Stretched Cluster im Vergleich zu einem Cluster-zu-Cluster im Vergleich zu einer Server-zu-Server-Topologie wählen?  
Das Speicherreplikat ist in drei wichtigen Konfigurationen verfügbar: Stretched Cluster , Cluster-zu-Cluster und Server-zu-Server. Jede bietet verschiedene Vorteile.

Die Stretched Cluster-Topologie ist ideal für Auslastungen, die automatisches Failover mit Orchestrierung wie z.B. private Hyper-V-Cloud-Cluster und SQLServer-Failoverclusterinstanzen erfordern. Es verfügt außerdem über eine integrierte Benutzeroberfläche, die den Failovercluster-Manager verwendet. Sie verwendet die klassische asymmetrische gemeinsam genutzte Cluster Speicherarchitektur von Speicherplätzen, SAN, iSCSI und RAID-Reservierungssemantik. Sie können dies mit nur 2 Knoten ausführen.

Die Cluster-zu-Cluster-Topologie verwendet zwei separate Cluster und eignet sich besonders für Administratoren, die manuelles Failover möchten, insbesondere, wenn der zweite Speicherort für die Notfallwiederherstellung und nicht die alltägliche Verwendung konfiguriert ist. Die Orchestrierung erfolgt manuell. Im Gegensatz zu Stretched Cluster können direkte Speicherplätze in dieser Konfiguration verwendet werden. Sie können dies mit nur 4 Knoten ausführen. 

Die Server-zu-Server-Topologie ist ideal für Kunden mit Hardware, die nicht als Clustern gruppiert werden kann. Sie erfordert manuelles Failover und Orchestrierung. Sie ist ideal für kostengünstige Bereitstellungen zwischen Zweigstellen und zentralen Rechenzentren, insbesondere bei der Verwendung von asynchroner Replikation. Diese Konfiguration ersetzt häufig Instanzen von DFSR-geschützten Dateiservern, die für die Single Master Notfallwiederherstellungszenarien verwendet werden.

In allen Fällen kann die Topologie sowohl auf physischer Hardware als auch auf virtuellen Computern ausgeführt werden. In virtuellen Computern erfordert der zugrunde liegenden Hypervisor nicht Hyper-V und kann anstatt VMware, KVM, Xen verwenden.

Das Speicherreplikatfeature verfügt außerdem über einen Server-to-Self-Modus, in dem die Replikation auf zwei Volumes auf demselben Computer verweist.

## <a name="FAQ17"></a> Wie melde ich ein Problem mit Speicherreplikaten oder diesem Leitfaden?  
Falls Sie technische Unterstützung für Speicherreplikate benötigen, können Sie Ihre Fragen in den [Microsoft TechNet-Foren](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview) stellen. Sie können uns auch eine E-Mail an srfeed@microsoft.com senden, wenn Sie Fragen zu Speicherreplikaten oder dieser Dokumentation haben. Die Website „https://windowsserver.uservoice.com“ sollte hauptsächlich für Änderungsvorschläge zum Design genutzt werden, da hier auch andere Kunden Unterstützung und Feedback zu Ihren Ideen geben können.



## <a name="related-topics"></a>Verwandte Themen  
- [Übersicht über Speicherreplikate](storage-replica-overview.md) 
- [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Server-zu-Server-Speicherreplikation](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster-Speicherreplikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikate: Bekannte Probleme](storage-replica-known-issues.md)  

## <a name="see-also"></a>Weitere Informationen  
- [Übersicht über das erweiterte Speichern](../storage.md)  
- [Storage Spaces Direct in Windows Server 2016 (Direkte Speicherplätze in Windows Server 2016)](../storage-spaces/storage-spaces-direct-overview.md)  
