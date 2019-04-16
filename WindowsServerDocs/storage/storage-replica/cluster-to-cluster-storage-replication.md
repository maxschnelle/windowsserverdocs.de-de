---
title: Cluster-zu-Cluster-Speicherreplikation
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 10/11/2016
description: Verwendung von Speicherreplikaten zum Replizieren von Volumes von einem Cluster auf einen anderen Cluster in der Windows Server2016 Datacenter Edition.
ms.openlocfilehash: 0681f6495390fda9b0c4564bf5516a48652b2c71
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-to-cluster-storage-replication"></a>Cluster-zu-Cluster-Speicherreplikation

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die Cluster-zu-Cluster-Replikation ist jetzt in Windows Server 2016 Datacenter Edition verfügbar, einschließlich der Replikation von Clustern mithilfe von „Direkte Speicherplätze“ (d.h. direkt angeschlossenem Shared-Nothing-Speicher). Die Verwaltung und Konfiguration ähnelt derjenigen der Server-zu-Server-Replikation.  

Sie konfigurieren diese Computer und Speicherkomponenten in einer Cluster-zu-Cluster-Konfiguration, bei der ein Cluster seinen eigenen Speicher mit einem anderen Cluster und dessen Speicher repliziert. Diese Knoten und der zugehörige Speicher sollten sich an unterschiedlichen physischen Standorten befinden. Dies ist jedoch keine Voraussetzung.  

In Windows Server 2016 Datacenter Edition gibt es keine grafischen Tools, die die Speicherreplikation für die Cluster-zu-Cluster-Replikation konfigurieren können, wobei Azure Site Recovery dieses Szenario zukünftig konfigurieren kann.

> [!IMPORTANT]
> Die vier Server in diesem Test sind ein Beispiel. Sie können eine beliebige Anzahl von Servern verwenden, die von Microsoft in jedem Cluster unterstützt werden. Diese Anzahl liegt momentan bei 16 für einen Direkte Speicherplätze-Cluster und bei 64 für einen Cluster von freigegebenem Speicher.  
>   
> In diesem Handbuch wird das Konfigurieren von „Direkte Speicherplätze“ nicht behandelt. Weitere Informationen zum Konfigurieren von „Direkte Speicherplätze“ finden Sie unter [Storage Spaces Direct in Windows Server 2016 (Direkte Speicherplätze in Windows Server 2016)](../storage-spaces/storage-spaces-direct-overview.md).  

Für diese exemplarische Vorgehensweise wird die folgende Beispielumgebung verwendet:  

-   Zwei Mitgliedsserver mit den Namen **SR-SRV01** und **SR-SRV02**, die später einem Cluster mit dem Namen **SR-SRVCLUSA** bilden werden.  

-   Zwei Mitgliedsserver mit den Namen **SR-SRV03** und **SR-SRV04**, die später einem Cluster mit dem Namen **SR-SRVCLUSB** bilden werden.  

-   Ein Paar aus logischen „Standorten“, die für zwei unterschiedliche Rechenzentren stehen: **Redmond** und **Bellevue**  

![Diagramm, das eine Beispielumgebung mit einer Replikation zwischen einem Cluster am Standort Redmond und einem Cluster am Standort Bellevue anzeigt](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)  

**ABBILDUNG 1: Cluster-zu-Cluster-Replikation**  

## <a name="prerequisites"></a>Voraussetzungen  

* Active Directory Domain Services-Gesamtstruktur (in dieser Gesamtstruktur muss nicht Windows Server 2016 ausgeführt werden).  
* Mindestens vier Server (zwei Server in zwei Clustern), auf denen Windows Server 2016 Datacenter Edition installiert ist. Unterstützt bis zu zwei Cluster mit 64 Knoten.  
* Zwei Gruppen von Speicher, die SAS-JBODs, Fibre Channel-SAN, freigegebene VHDX, Direkte Speicherplätze oder iSCSI-Ziel verwenden. Der Speicher sollte eine Kombination aus HDD- und SSD-Medien umfassen. Die einzelnen Speichergruppen werden nur für jeweils einen Cluster bereitgestellt, ein gemeinsamer Zugriff zwischen Clustern wird nicht konfiguriert.  
* Jede Speichergruppe muss das Erstellen von mindestens zwei virtuellen Datenträgern ermöglichen, einen Datenträger für replizierte Daten und einen Datenträger für Protokolle. Der physische Speicher muss auf allen Datenträgern für Daten dieselben Sektorgrößen aufweisen. Der physische Speicher muss auf allen Datenträgern für Protokolle dieselben Sektorgrößen aufweisen.  
* Mindestens eine Ethernet/TCP-Verbindung auf jedem Server für die synchrone Replikation (vorzugsweise RDMA).   
* Geeignete Firewall- und Routerregeln, um bidirektionalen ICMP-, SMB- (Port445 sowie 5445 für SMB Direct) und WS-MAN-Datenverkehr (Port5985) zwischen allen Knoten zu ermöglichen.  
* Ein Netzwerk zwischen den Servern mit ausreichender Bandbreite für Ihre E/A-Schreibworkload sowie durchschnittlich 5ms Roundtriplatenz für die synchrone Replikation. Für die asynchrone Replikation gilt keine Empfehlung bezüglich der Latenz.  
* Der replizierte Speicher darf sich nicht auf dem Laufwerk mit dem Ordner des Windows-Betriebssystems befinden.

Das Vorliegen vieler dieser Voraussetzungen lässt sich mit dem `Test-SRTopology`-Cmdlet ermitteln. Sie erhalten Zugang zu diesem Tool, wenn Sie das Speicherreplikatfeature oder die Speicherreplikat-Verwaltungstools auf mindestens einem Server installieren. Das Speicherreplikatfeature muss nicht konfiguriert werden, um dieses Tool verwenden zu können. Es wird lediglich zur Installation des Cmdlets benötigt. Weitere Informationen finden Sie in den nachfolgend beschriebenen Schritten.  

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>Schritt1: Bereitstellen von Betriebssystem, Features, Rollen, Speicher und Netzwerk

1.  Installieren Sie Windows Server 2016 auf allen vier Serverknoten mit dem Installationstyp Windows Server 2016 Datacenter **(Desktopdarstellung)**. Wählen Sie nicht „Standard Edition“, falls diese Option verfügbar ist, da diese Edition das Speicherreplikatfeature nicht beinhaltet.  

2.  Fügen Sie Netzwerkinformationen hinzu, konfigurieren Sie den Domänenbeitritt, und starten Sie die Serverknoten neu.  

    > [!IMPORTANT]  
    > Melden Sie sich anschließend stets als Domänenbenutzer an, der Mitglied der integrierten Administratorengruppe auf allen Servern ist. Denken Sie anschließend immer daran, erhöhte Rechte für Ihre Windows PowerShell- und CMD-Eingabeaufforderungen festzulegen, wenn Sie die Features auf einer graphischen Serverinstallation oder auf einem Windows10-Computer ausführen.  

3.  Verbinden Sie die erste Gruppe aus JBOD-Speichergehäusen, iSCSI-Zielen, FC-SAN- oder lokalem DAS-Speicher mit dem Server am Standort **Redmond**.  

4.  Verbinden Sie die zweite Speichergruppe mit dem Server am Standort **Bellevue**.  

5.  Installieren Sie gegebenenfalls aktuelle Speicher- und Speicherserverfirmware, HBA-Treiber, BIOS/UEFI-Firmware, Netzwerktreiber und Hauptplatinenchipsatz-Treiber der jeweiligen Hersteller auf allen vier Knoten. Starten Sie die Knoten gegebenenfalls neu.  

    > [!NOTE]  
    > Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.  

6.  Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z.B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die Energieverwaltung in Windows Server auf eine hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus.  

7.  Konfigurieren Sie folgende Rollen:  

    -   **Grafische Methode**  

        1.  Führen Sie **ServerManager.exe** aus, und erstellen Sie eine Servergruppe, der Sie alle Serverknoten hinzufügen.  

        2.  Installieren Sie die Rollen und Features **Dateiserver** und **Speicherreplikat** auf allen Knoten, und starten Sie die Knoten neu.  

    -   **Windows PowerShell-Methode**  

        Führen Sie auf SR-SRV04 oder einem Remoteverwaltungscomputer den folgenden Befehl in einer Windows PowerShell-Konsole aus, um die erforderlichen Features und Rollen für einen Stretched Cluster auf den vier Knoten zu installieren und sie neu zu starten:  

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        Weitere Informationen zu diesen Schritten finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](http://technet.microsoft.com/library/hh831809.aspx).  

9. Konfigurieren Sie den Speicher wie folgt:  

    > [!IMPORTANT]  
    > -   In jedem Speicherserver müssen zwei Volumes erstellt werden: ein Volume für Daten und ein Volume für Protokolle.  
    > -   Die Datenträger für Protokolle und Daten müssen als **GPT** (nicht **MBR**) initialisiert werden.  
    > -   Die beiden Datenvolumes müssen dieselbe Größe aufweisen.  
    > -   Die beiden Protokollvolumes sollten dieselbe Größe aufweisen.  
    > -   Alle Datenträger für replizierte Daten müssen dieselben Sektorgrößen aufweisen.  
    > -   Alle Datenträger für Protokolle müssen dieselben Sektorgrößen aufweisen.  
    > -   Die Protokollvolumes sollten Flash-basierten Speicher verwenden (z.B. SSD).  Microsoft empfiehlt, dass die Protokollspeicherung schneller als die Datenspeicherung durchgeführt wird. Protokollvolumes dürfen niemals für andere Workloads verwendet werden.
    > -   Die Datenträger für Daten können HDD, SSD oder eine mehrstufige Kombination verwenden. Außerdem kann gespiegelter Speicherplatz oder Paritätsspeicherplatz bzw. RAID 1, RAID 10, RAID 5 oder RAID 50 verwendet werden.  
    > -   Das Protokollvolume muss standardmäßig eine Größe von mindestens 9 GB aufweisen und kann basierend auf Protokollanforderungen möglicherweise größer oder kleiner sein.  

    -   **Für JBOD-Gehäuse:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die SAS-Verbindungen ordnungsgemäß konfiguriert sind.  

        2.  Stellen Sie den Speicher mithilfe von Speicherplätzen bereit. Führen Sie dazu die unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](http://technet.microsoft.com/library/jj822938.aspx) beschriebenen **Schritte 1-3** mithilfe von Windows PowerShell oder über den Server-Manager aus.  

    -   **Für iSCSI-Zielspeicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden. Bei Verwendung von iSCSI sollten mehrere Netzwerkkarten verwendet werden.  

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen. Bei Verwendung von Windows-basierten iSCSI-Zielen finden Sie unter [iSCSI-Zielblockspeicher: So wird's gemacht](http://technet.microsoft.com/library/hh848268.aspx) weitere Informationen.  

    -   **Für FC-SAN-Speicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die Zonen für die Hosts ordnungsgemäß festgelegt wurden.  

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen.  

    -   **Für direkte Speicherplätze:**  

        1.  Stellen Sie sicher, dass jeder Cluster nur die Speicherserver des jeweiligen Standorts erkennen kann, indem direkte Speicherplätze bereitgestellt werden. (https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) 

        2.  Stellen Sie sicher, dass die SR-Protokollvolumes sich immer auf dem schnellsten Flash-Speicher und die Datenvolumes sich in einem langsameren Speicher mit hoher Kapazität befinden.

10. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets `Test-SRTopology`, ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Für einen schnellen Test können Sie das Cmdlet in einem Modus zur ausschließlichen Überprüfung der Anforderungen ausführen, oder Sie wählen einen Modus mit langer Ausführungsdauer, um die Leistung auszuwerten.  
Beispiel:  

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp        
   ```

      > [!IMPORTANT]
      > Bei Verwendung eines Testservers ohne Schreib-E/A-Last auf dem angegebenen Quellvolume während des Auswertungszeitraums sollten Sie gegebenenfalls eine Workload hinzufügen, um einen nützlichen Bericht zu erhalten. Um reale Zahlen und empfohlene Protokollgrößen zu erhalten, sollte der Test mit produktionsähnlichen Workloads ausgeführt werden. Alternativ können Sie ganz einfach während des Tests Dateien auf das Quellvolume kopieren oder [DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) herunterladen und ausführen, um Schreib-E/A zu generieren. Beispiel mit geringer E/A-Workload innerhalb eines Zeitraums von 5Minuten auf dem Volume D:  
      > `Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`  

11. Stellen Sie anhand des Berichts **TestSrTopologyReport.html** sicher, dass Sie die Anforderungen für das Speicherreplikatfeature erfüllen.  

    ![Bildschirm, der die Replikationstopologie der Berichtsergebnisse darstellt](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)      

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>Schritt2: Konfigurieren von zwei Failoverclustern mit horizontaler Skalierung  
Im Folgenden erstellen Sie zwei normale Failovercluster. Nach der Konfiguration, der Überprüfung und dem Testen replizieren Sie diese mithilfe des Speicherreplikatfeatures. Die unten beschriebenen Schritte können unmittelbar auf den Clusterknoten oder über einen Remoteverwaltungscomputer ausgeführt werden, auf dem die RSAT-Verwaltungstools von Windows Server 2016 installiert sind.  

### <a name="graphical-method"></a>Grafische Methode  

1.  Führen Sie **cluadmin.msc** für einen Knoten an jedem Standort aus.  

2.  Überprüfen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können. Im Beispiel unten sind es **SR-SRVCLUSA** und **SR-SRVCLUSB**.  

3.  Erstellen Sie die zwei Cluster. Stellen Sie sicher, dass die Clusternamen maximal 15 Zeichen lang sind.  

4.  Konfigurieren Sie einen Dateifreigabe- oder Cloudzeugen.  

    > [!NOTE]  
    > Windows Server 2016 enthält nun eine Option für einen (Azure-basierten) Cloudzeugen. Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.  

    > [!WARNING]  
    > Weitere Informationen zur Quorumkonfiguration finden Sie im Abschnitt **Zeugenkonfiguration** unter [Konfigurieren und Verwalten des Quorums in einem Windows Server2012-Failovercluster](http://technet.microsoft.com/library/jj612870.aspx). Weitere Informationen zum Cmdlet `Set-ClusterQuorum` finden Sie unter [Set-ClusterQuorum](http://technet.microsoft.com/library/hh847275.aspx).  

5.  Fügen Sie am Standort **Redmond** den freigegebenen Clustervolumes einen Datenträger hinzu. Zu diesem Zweck klicken Sie im Bereich **Speicher** mit der rechten Maustaste auf den Knoten **Datenträger** und klicken dann auf **Zu freigegebenen Clustervolumes hinzufügen**.  

6.  Erstellen Sie die gruppierten Dateiserver mit horizontaler Skalierung in beiden Clustern mithilfe der Anweisungen in [Konfigurieren des Dateiservers mit horizontaler Skalierung](http://technet.microsoft.com/library/hh831718.aspx).  

### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  

1.  Testen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können:  

    ```PowerShell
    Test-Cluster SR-SRV01,SR-SRV02  
    Test-Cluster SR-SRV03,SR-SRV04  
    ```  

2.  Erstellen Sie die Cluster (Sie müssen eine eigene statische IP-Adressen für den Cluster angeben). Stellen Sie sicher, dass jeder Clustername maximal 15 Zeichen lang ist:  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUSA -Node SR-SRV01,SR-SRV02 -StaticAddress <your IP here>  
    New-Cluster -Name SR-SRVCLUSB -Node SR-SRV03,SR-SRV04 -StaticAddress <your IP here>  
    ```  

3.  Konfigurieren Sie in jedem Cluster einen Dateifreigabe- oder Cloudzeugen (Azure), der auf eine Freigabe verweist, die auf dem Domänencontroller oder auf einem anderen unabhängigen Server gehostet ist. Beispiel:  

    ```PowerShell  
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
    ```  

    > [!NOTE]  
    > Windows Server 2016 enthält nun eine Option für einen (Azure-basierten) Cloudzeugen. Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.  

    > [!WARNING]  
    > Weitere Informationen zur Quorumkonfiguration finden Sie im Abschnitt **Zeugenkonfiguration** unter [Konfigurieren und Verwalten des Quorums in einem Windows Server2012-Failovercluster](http://technet.microsoft.com/library/jj612870.aspx). Weitere Informationen zum Cmdlet `Set-ClusterQuorum` finden Sie unter [Set-ClusterQuorum](http://technet.microsoft.com/library/hh847275.aspx).  

4.  Erstellen Sie die gruppierten Dateiserver mit horizontaler Skalierung in beiden Clustern mithilfe der Anweisungen in [Konfigurieren des Dateiservers mit horizontaler Skalierung](https://technet.microsoft.com/library/hh831718.aspx).  

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>Schritt3: Konfigurieren der Cluster-zu-Cluster-Replikation mit Windows PowerShell  
Jetzt richten Sie die Cluster-zu-Cluster-Replikation mit Windows PowerShell ein. Die unten beschriebenen Schritte können unmittelbar auf den Knoten oder über einen Remoteverwaltungscomputer ausgeführt werden, auf dem die RSAT-Verwaltungstools von Windows Server 2016 installiert sind.  

1.  Gewähren Sie dem ersten Cluster Vollzugriff auf die anderen Cluster, indem Sie das Cmdlet **Grant-ClusterAccess** auf einem beliebigen Knoten im ersten Cluster oder remote ausführen.  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB  
    ```  

2.  Gewähren Sie dem zweiten Cluster Vollzugriff auf die anderen Cluster, indem Sie das Cmdlet **Grant-ClusterAccess** auf einem beliebigen Knoten im zweiten Cluster oder remote ausführen.  

    ```PowerShell
    Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA  
    ```  

3.  Konfigurieren Sie die Cluster-zu-Cluster-Replikation, und geben Sie dabei die Quell- und Zieldatenträger, die Quell- und Zielprotokolle, die Quell- und Zielclusternamen sowie die Protokollgröße an. Sie können diesen Befehl lokal auf dem Server oder unter Verwendung eines Remoteverwaltungscomputers ausführen.  

    ```powershell  
    New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:  
    ```  

    > [!WARNING]  
    > Die standardmäßige Protokollgröße beträgt 8GB. Abhängig von den Ergebnissen des Cmdlets **Test-SRTopology** können Sie **-LogSizeInBytes** mit einem höheren oder niedrigeren Wert verwenden.  

4.  Verwenden Sie **Get-SRGroup** und **Get-SRPartnership**wie folgt, um den Quell- und Zielzustand der Replikation abzurufen:  

    ```powershell
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

5.  Bestimmen Sie den Fortschritt der Replikation wie folgt:  

    1.  Führen Sie auf dem Quellserver den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5015, 5002, 5004, 1237, 5001 und 2200:
        
        ```PowerShell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
        ```
    2.  Führen Sie auf dem Zielserver den folgenden Befehl aus, um die Speicherreplikatereignisse anzuzeigen, die das Erstellen der Partnerschaft belegen. Dieses Ereignis gibt die Anzahl der kopierten Bytes sowie die dafür benötigte Zeit an. Beispiel:  
        
        ```powershell
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
        ```
        Hier ist ein Beispiel für die Ausgabe angegeben:
        
        ```
        TimeCreated  : 4/8/2016 4:12:37 PM  
        ProviderName : Microsoft-Windows-StorageReplica  
        Id           : 1215  
        Message      : Block copy completed for replica.  
            ReplicationGroupName: rg02  
            ReplicationGroupId:  
            {616F1E00-5A68-4447-830F-B0B0EFBD359C}  
            ReplicaName: f:\  
            ReplicaId: {00000000-0000-0000-0000-000000000000}  
            End LSN in bitmap:  
            LogGeneration: {00000000-0000-0000-0000-000000000000}  
            LogFileId: 0  
            CLSFLsn: 0xFFFFFFFF  
            Number of Bytes Recovered: 68583161856  
            Elapsed Time (seconds): 117  
        ```
    3. Alternativ gibt die Zielservergruppe für das Replikat jederzeit die Anzahl der noch zu kopierenden Bytes an. Dieser Wert kann auch über PowerShell abgefragt werden. Beispiel:

       ```PowerShell
       (Get-SRGroup).Replicas | Select-Object numofbytesremaining
       ```

       Beispiel für den Fortschritt (das nicht beendet wird):  

       ```PowerShell
         while($true) {  
         $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }
        ```

6. Führen Sie auf dem Zielserver im Zielcluster den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5009, 1237, 5001, 5015, 5005 und 2200, um Informationen zum Verarbeitungsfortschritt zu erhalten. Diese Abfolge sollte keine Warnungen oder Fehler enthalten. Es werden eine Vielzahl von Ereignissen des Typs 1237 angezeigt, die für den Fortschritt stehen.  
    
   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
   ```
   > [!NOTE]  
        > Der Zielcluster-Datenträger wird bei der Replikation immer als **Online (kein Zugriff)** angezeigt.  

## <a name="step-4-manage-replication"></a>Schritt4: Verwalten der Replikation

Jetzt können Sie Ihre Cluster-zu-Cluster-Replikation verwalten und betreiben. Die unten beschriebenen Schritte können unmittelbar auf den Clusterknoten oder über einen Remoteverwaltungscomputer ausgeführt werden, auf dem die RSAT-Verwaltungstools von Windows Server 2016 installiert sind.  

1.  Verwenden Sie **Get-ClusterGroup** oder den **Failovercluster-Manager**, um die aktuelle Quelle und das aktuelle Ziel der Replikation sowie den zugehörigen Status zu ermitteln.  

2.  Zum Ermitteln der Replikationsleistung verwenden Sie das Cmdlet **Get-Counter** sowohl auf dem Quell- als auch auf dem Zielknoten. Es werden folgende Leistungsindikatoren verwendet:  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Häufigkeit, mit der die Leerung angehalten wurde  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl ausstehender Leerungs-E/As  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anforderungen für letzten Schreibvorgang im Protokoll  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschnittl. Länge der Warteschlange zum Leeren  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Aktuelle Länge der Warteschlange zum Leeren  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anwendungsschreibanforderungen  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl Durchschnittl. Anforderungen pro Schreibvorgang im Protokoll  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschnittl. Wartezeit für App-Schreibvorgang  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschnittl. Wartezeit für App-Lesevorgang  

    -   \Speicherreplikatstatistik(*)\Ziel-RPO  

    -   \Speicherreplikatstatistik(*)\Aktuelle RPO  

    -   \Speicherreplikatstatistik(*)\Durchschnittl. Länge der Protokollwarteschlange  

    -   \Speicherreplikatstatistik(*)\Aktuelle Länge der Protokollwarteschlange  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl empfangener Bytes  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl gesendeter Bytes  

    -   \Speicherreplikatstatistik (*) \Durchschnittl. Wartezeit beim Senden über das Netzwerk  

    -   \Speicherreplikatstatistik(*)\Replikationszustand  

    -   \Speicherreplikatstatistik (*) \Durchschnittl. Wartezeit bei Nachrichtenroundtrip  

    -   \Speicherreplikatstatistik(*)\Verstrichene Zeit bei letzter Wiederherstellung  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Max. Protokollfolgenummer  

    -   \Speicherreplikatstatistik(*)\Anzahl empfangener Nachrichten  

    -   \Speicherreplikatstatistik(*)\Anzahl gesendeter Nachrichten  

    Weitere Informationen zu Leistungsindikatoren in Windows PowerShell finden Sie unter [Get-Counter](https://technet.microsoft.com/library/hh849685.aspx).  

3.  Zum Ändern der Replikationsrichtung eines Standorts verwenden Sie das Cmdlet **Set-SRPartnership**.  

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01  
    ```  

    > [!NOTE]  
    > Windows Server 2016 verhindert einen Rollenwechsel während der ersten Synchronisierung, da es zu Datenverlust führen kann, wenn Sie vor Abschluss der ersten Replikation versuchen, einen Wechsel vorzunehmen. Erzwingen Sie keinen Richtungswechsel, bevor die erste Synchronisierung abgeschlossen ist.

    Überprüfen Sie die Ereignisprotokolle auf eine Richtungsänderung bei der Replikation und einen Wiederherstellungsmodus, und bringen Sie die Konfiguration in Einklang. Schreib-E/As können anschließend in den Speicher schreiben, der sich im Besitz des neuen Quellservers befindet. Durch das Ändern der Replikationsrichtung werden Schreib-E/As auf dem vorherigen Quellcomputer verhindert.  

    > [!NOTE]  
    > Der Zielcluster-Datenträger wird bei der Replikation immer als **Online (kein Zugriff)** angezeigt.  

4.  Zum Ändern des Standardwerts der Protokollgröße von 8 GB in Windows Server 2016 verwenden Sie **Set-SRGroup** für die Quell- und Ziel-Speicherreplikatgruppen.  

    > [!IMPORTANT]  
    > Die standardmäßige Protokollgröße beträgt 8GB. Abhängig von den Ergebnissen des Cmdlets **Test-SRTopology** können Sie „-LogSizeInBytes“ mit einem höheren oder niedrigeren Wert verwenden.  

5.  Verwenden Sie zum Entfernen der Replikation **Get-SRGroup**, **Get-SRPartnership**, **Remove-SRGroup** und **Remove-SRPartnership** auf jedem Cluster.  

    ```powershell
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]  
    > Das Speicherreplikatfeature hebt die Bereitstellung der Zielvolumes auf. Dies ist entwurfsbedingt.

## <a name="see-also"></a>Weitere Informationen:

-   [Übersicht über Speicherreplikate](storage-replica-overview.md) 
-   [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
-   [Server-zu-Server-Speicherreplikation](server-to-server-storage-replication.md)  
-   [Speicherreplikate: Bekannte Probleme](storage-replica-known-issues.md)  
-   [Speicherreplikate: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)  
-   [Storage Spaces Direct in Windows Server 2016 (Direkte Speicherplätze in Windows Server 2016)](../storage-spaces/storage-spaces-direct-overview.md)  
