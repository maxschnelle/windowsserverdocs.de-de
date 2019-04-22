---
title: Server-zu-Server-Speicherreplikation
description: Informationen zum Einrichten und Verwenden der Funktion "Speicherreplikat" für die Replikation von Server-zu-Server unter Windows Server, einschließlich Windows Admin Center und PowerShell.
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 06/04/2018
ms.assetid: 61881b52-ee6a-4c8e-85d3-702ab8a2bd8c
ms.openlocfilehash: 620d339a505da77649d65537abc92f301760d40d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821291"
---
# <a name="server-to-server-storage-replication-with-storage-replica"></a>Server-zu-Server-Speicherreplikation mit Speicherreplikaten

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mithilfe der Speicherreplikation können Sie zwei Server konfigurieren, um die Daten zu synchronisieren, sodass jeder Server über eine identische Kopie des gleichen Volumes verfügt. Dieses Thema enthält Hintergrundinformationen zu dieser Konfiguration einer Server-zu-Server-Replikation sowie zum Einrichten und Verwalten der Umgebung.

Zum Verwalten des Speicherreplikats können [Windows Admin Center](../../manage/windows-admin-center/overview.md) oder PowerShell.

Hier ist eine Übersicht übersichtsvideo unter Verwendung von Speicherreplikaten in Windows Admin Center.
> [!video https://www.microsoft.com/videoplayer/embed/3aa09fd4-867b-45e9-953e-064008468c4b?autoplay=false]


## <a name="prerequisites"></a>Vorraussetzungen  

* Active Directory-Domänendienste-Gesamtstruktur (muss nicht Windows Server 2016 ausgeführt).  
* Zwei Server, auf denen Windows Server 2016 Datacenter Edition installiert ist.  
* Zwei Speichergruppen, die SAS-JBODs, Fibre Channel-SANs, iSCSI-Ziele oder lokalen SCSI/SATA-Speicher verwenden. Der Speicher sollte eine Kombination aus HDD- und SSD-Medien umfassen. Die einzelnen Speichergruppen werden nur für jeweils einen Server bereitgestellt, ein gemeinsamer Zugriff wird nicht konfiguriert.  
* Jede Speichergruppe muss das Erstellen von mindestens zwei virtuellen Datenträgern ermöglichen, einen Datenträger für replizierte Daten und einen Datenträger für Protokolle. Der physische Speicher muss auf allen Datenträgern für Daten dieselben Sektorgrößen aufweisen. Der physische Speicher muss auf allen Datenträgern für Protokolle dieselben Sektorgrößen aufweisen.  
* Mindestens eine Ethernet/TCP-Verbindung auf jedem Server für die synchrone Replikation (vorzugsweise RDMA).   
* Geeignete Firewall- und Routerregeln, um bidirektionalen ICMP-Datenverkehr, SMB-Datenverkehr (Port445 sowie 5445 für SMB Direct) und WS-MAN-Datenverkehr (Port5985) zwischen allen Knoten zu ermöglichen.  
* Ein Netzwerk zwischen den Servern mit ausreichender Bandbreite für Ihre E/A-Schreibworkload sowie durchschnittlich 5 ms Roundtriplatenz für die synchrone Replikation. Asynchroner Replikation keine Empfehlung bezüglich der Latenz.<br>
Wenn Sie zwischen lokalen Servern und Azure-VMs replizieren, müssen Sie eine Netzwerkverbindung zwischen dem lokalen Server und die Azure-VMs erstellen. Zu diesem Zweck verwenden [Expressroute](#add-azure-vm-expressroute), [Standort-zu-Standort-VPN-gatewayverbindung](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal), oder installieren Sie die VPN-Software in Ihrer Azure-VMs, die sie mit Ihrem lokalen Netzwerk zu verbinden.
* Der replizierte Speicher darf sich nicht auf dem Laufwerk mit dem Ordner des Windows-Betriebssystems befinden.

> [!IMPORTANT]
>  In diesem Szenario sollte sich jeder Server an einem anderen physischen oder logischen Standort befinden. Die Server müssen über das Netzwerk miteinander kommunizieren können.  


Viele dieser Voraussetzungen lassen sich mit dem `Test-SRTopology cmdlet` ermitteln. Sie erhalten Zugang zu diesem Tool, wenn Sie das Speicherreplikatfeature oder die Speicherreplikat-Verwaltungstools auf mindestens einem Server installieren. Das Speicherreplikatfeature muss nicht konfiguriert werden, um dieses Tool verwenden zu können. Es wird lediglich zur Installation des Cmdlets benötigt. Weitere Informationen finden Sie in den nachfolgend beschriebenen Schritten.  

## <a name="windows-admin-center-requirements"></a>Anforderungen für Windows Admin Center

Um die Funktion "Speicherreplikat" und Windows Admin Center zusammen verwenden, benötigen Sie Folgendes:

| System                        | Betriebssystem                                            | Erforderlich für     |
|-------------------------------|-------------------------------------------------------------|------------------|
| Zwei Server <br>(eine beliebige Kombination von lokalen Hardware, VMs und Cloud-VMs, einschließlich virtuellen Azure-Computern)| Datacenter-Edition von Windows Server (Halbjährlicher Kanal) oder Windows Server 2016 | Speicherreplikat  |
| Einen PC                     | Windows 10                                                  | Windows Admin Center |

> [!NOTE]
> Zurzeit Sie nicht Windows Admin Center auf einem Server zum Verwalten des Speicherreplikats verwenden.

## <a name="terms"></a>Benennungen  
Für diese exemplarische Vorgehensweise wird die folgende Beispielumgebung verwendet:  

-   Zwei Server: **SR-SRV05** und **SR-SRV06**  

-   Ein Paar aus logischen „Standorten“, die für zwei unterschiedliche Rechenzentren stehen: **Redmond** und **Bellevue**.  

![Diagramm, das einen Server in Gebäude 5 zeigt, der mit einem Server in Gebäude 9 repliziert wird](media/Server-to-Server-Storage-Replication/Storage_SR_ServertoServer.png)  

**Abbildung 1: Server in Server-Replikation**  

## <a name="step-1-install-and-configure-windows-admin-center-on-your-pc"></a>Schritt 1: Installieren und Konfigurieren von Windows Admin Center auf Ihren PC

Wenn Sie Windows Admin Center zum Verwalten der Funktion "Speicherreplikat" verwenden, verwenden Sie die folgenden Schritte aus, für die Vorbereitung von Ihrem PC zum Verwalten der Funktion "Speicherreplikat".
1. Herunterladen und installieren [Windows Admin Center](../../manage/windows-admin-center/overview.md).
2. Herunterladen und Installieren der [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520).
    - Installieren Sie bei Verwendung von Windows 10, Version 1809 oder höher, die "Remoteserver-Verwaltungstools: Storage-Replikat-Modul für Windows PowerShell"aus der Features bei Bedarf.
3. Öffnen Sie dazu eine PowerShell-Sitzung als Administrator die **starten** Schaltfläche eingeben **PowerShell**der rechten Maustaste auf **Windows PowerShell,** auswählen und dann  **Als Administrator ausführen**.
4. Geben Sie den folgenden Befehl zum Aktivieren des WS-Management-Protokolls auf dem lokalen Computer, und richten Sie die Standardkonfiguration für die Remoteverwaltung auf dem Client.

    ```PowerShell
    winrm quickconfig
    ```

5. Typ **Y** WinRM-Dienste aktiviert, und aktivieren WinRM-Firewall-Ausnahme.

## <a name="provision-os"></a>Schritt 2: Bereitstellen von Betriebssystem, Features, Rollen, Speicher und Netzwerk

1.  Installieren Sie Windows Server 2016 auf beiden Serverknoten mit dem Installationstyp Windows Server 2016 Datacenter **(Desktopdarstellung)**. Wählen Sie Standard Edition nicht, sofern diese verfügbar ist, wie sie die Funktion "Speicherreplikat" nicht enthält.
 
    Um eine Azure-VM, die mit Ihrem Netzwerk über eine expressroute-Verbindung verbunden verwenden zu können, finden Sie unter [Hinzufügen einer Azure-VM mit Ihrem Netzwerk über ExpressRoute verbunden](#add-azure-vm-expressroute).

3.  Fügen Sie Netzwerkinformationen hinzu, einbinden Sie der Server in derselben Domäne wie die Verwaltung Ihrer Windows 10 PCs (Wenn Sie eine verwenden), und klicken Sie dann die starten Sie Server erneut.  

    > [!NOTE]
    > Melden Sie sich ab jetzt stets als Domänenbenutzer an, der Mitglied der integrierten Administratorengruppe auf allen Servern ist. Denken Sie von nun an immer daran, erhöhte Rechte für Ihre PowerShell- und Eingabeaufforderungen festzulegen, wenn Sie die Features auf einer graphischen Serverinstallation oder auf einem Windows10-Computer ausführen.  

3.  Verbindung mit dem Server am Standort den ersten Satz von JBOD-Speicherserver, iSCSI-Ziel, FC-SAN oder einer lokalen Festplatte (DAS) Speichergruppe **Redmond**.  

4.  Verbindung mit dem Server am Standort der zweiten Menge des Speichers **Bellevue**.  

5.  Installieren Sie gegebenenfalls aktuelle Speicher- und Gehäusefirmware, HBA-Treiber, BIOS/UEFI-Firmware, Netzwerktreiber und Hauptplatinenchipsatz-Treiber der jeweiligen Hersteller auf beiden Knoten. Starten Sie die Knoten gegebenenfalls neu.  

    > [!NOTE]
    > Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.  

6.  Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z. B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die energieverwaltung in Windows Server auf eine hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus.  

7.  Konfigurieren Sie folgende Rollen:  

    -   **Windows Admin Center-Methode**
        1. Klicken Sie in Windows Admin Center navigieren Sie zu Server-Manager, und wählen Sie dann einen der Server.
        2. Navigieren Sie zu **Rollen und Features**.
        3. Wählen Sie **Features** > **Funktion "Speicherreplikat"**, und klicken Sie dann auf **installieren**.
        4. Wiederholen Sie die auf dem anderen Server.
    -   **Server-Manager-Methode**  

        1.  Führen Sie **ServerManager.exe** aus, und erstellen Sie eine Servergruppe, der Sie alle Serverknoten hinzufügen.  

        2.  Installieren Sie die Rollen und Features **Dateiserver** und **Speicherreplikat** auf allen Knoten, und starten Sie die Knoten neu.  

    -   **Windows PowerShell-Methode**  

        Führen Sie auf SR-SRV06 oder einem Remoteverwaltungscomputer den folgenden Befehl in einer Windows PowerShell-Konsole aus, um die erforderlichen Features und Rollen zu installieren und den Knoten neu zu starten:  

        ```powershell  
        $Servers = 'SR-SRV05','SR-SRV06'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        Weitere Informationen zu diesen Schritten finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](http://technet.microsoft.co/library/hh831809.aspx).  

8.  Konfigurieren Sie den Speicher wie folgt:  

    > [!IMPORTANT]  
    > -   In jedem Speicherserver müssen zwei Volumes erstellt werden: ein Volume für Daten und ein Volume für Protokolle.  
    > -   Die Datenträger für Protokolle und Daten müssen als GPT (nicht MBR) initialisiert werden.  
    > -   Die beiden Datenvolumes müssen dieselbe Größe aufweisen.  
    > -   Die beiden Protokollvolumes sollten dieselbe Größe aufweisen.  
    > -   Alle Datenträger für replizierte Daten müssen dieselben Sektorgrößen aufweisen.  
    > -   Alle Datenträger für Protokolle müssen dieselben Sektorgrößen aufweisen.  
    > -   Die Protokollvolumes sollten Flash-basierten Speicher verwenden (z. B. SSD). Microsoft empfiehlt, dass die Protokollspeicherung schneller als die Datenspeicherung durchgeführt wird. Protokollvolumes dürfen niemals für andere Workloads verwendet werden.
    > -   Die Datenträger für Daten können HDD, SSD oder eine mehrstufige Kombination verwenden. Außerdem kann gespiegelter Speicherplatz oder Paritätsspeicherplatz bzw. RAID 1, RAID 10, RAID 5 oder RAID 50 verwendet werden.  
    > -   Das Protokollvolume muss standardmäßig eine Größe von mindestens 9 GB aufweisen und kann basierend auf Protokollanforderungen möglicherweise größer oder kleiner sein.  
    > -   Die Rolle „Dateiserver“ ist nur für Test-SRTopology erforderlich, um die erforderlichen Firewallports für die Tests zu öffnen.
    
    - **Für JBOD-Speicherserver:**  

        1.  Stellen Sie sicher, dass jedem Server nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die SAS-Verbindungen ordnungsgemäß konfiguriert sind.  

        2.  Stellen Sie den Speicher mithilfe von Speicherplätzen bereit. Führen Sie dazu die unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](../storage-spaces/deploy-standalone-storage-spaces.md) beschriebenen **Schritte 1-3** mithilfe von Windows PowerShell oder über den Server-Manager aus.  

    - **Für iSCSI-Speicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden. Bei Verwendung von iSCSI sollten mehrere Netzwerkkarten verwendet werden.    

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen. Bei Verwendung von Windows-basierten iSCSI-Zielen finden Sie unter [iSCSI-Zielblockspeicher: So wird's gemacht](https://technet.microsoft.com/library/hh848268.aspx) weitere Informationen.  

    - **Für FC-SAN-Speicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die Zonen für die Hosts ordnungsgemäß festgelegt wurden.   

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen.  

    - **Für den Speicher des lokalen Datenträger mit fester Größe:**  

        -   Stellen Sie sicher, der Speicher nicht enthalten, ein Systemvolume, die Auslagerungsdatei und keine Abbilddateien.  

        -   Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen.  

9. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets **Test-SRTopology**, ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind. Für einen schnellen Test können Sie das Cmdlet in einem Modus zur ausschließlichen Überprüfung der Anforderungen ausführen, oder Sie wählen einen Modus mit langer Ausführungsdauer, um die Leistung auszuwerten.  

    Beispiel: So überprüfen Sie, ob die Knoten jeweils über ein Volume **F:** und **G:** verfügen (die Ausführungszeit des Tests beträgt 30 Minuten):  
        
    ```PowerShell
    MD c:\temp  

    Test-SRTopology -SourceComputerName SR-SRV05 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV06 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp  
    ```

    > [!IMPORTANT]
      > Bei Verwendung eines Testservers ohne Schreib-E/A-Last auf dem angegebenen Quellvolume während des Auswertungszeitraums sollten Sie gegebenenfalls eine Workload hinzufügen, um einen nützlichen Bericht zu erhalten. Um reale Zahlen und empfohlene Protokollgrößen zu erhalten, sollte der Test mit produktionsähnlichen Workloads ausgeführt werden. Alternativ können Sie ganz einfach während des Tests Dateien auf das Quellvolume kopieren oder [DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) herunterladen und ausführen, um Schreib-E/A zu generieren. Beispiel mit geringer E/A-Workload innerhalb eines Zeitraums von 5 Minuten auf dem Volume D:  
      >
      > `Diskspd.exe -c1g -d600 -W5 -C5 -b8k -t2 -o2 -r -w5 -i100 d:\test` 

10. Überprüfen Sie die **TestSrTopologyReport.html** Bericht, die in Abbildung 2 dargestellt werden, um sicherzustellen, dass Sie die Funktion "Speicherreplikat" erfüllen.  

    ![Bildschirm mit Topologiebericht](media/Server-to-Server-Storage-Replication/SRTestSRTopologyReport.png)

    **Abbildung 2: Storage-Replikation topologiebericht**

## <a name="step-3-set-up-server-to-server-replication"></a>Schritt 3: Einrichten der Replikation von Server-zu-server
### <a name="using-windows-admin-center"></a>Mithilfe von Windows Admin Center

1. Fügen Sie den Quellserver hinzu.
    1. Wählen Sie die **hinzufügen** Schaltfläche.
    2. Wählen Sie **Serververbindung hinzufügen**.
    3. Geben Sie den Namen des Servers ein, und wählen Sie dann **senden**.
2. Auf der **alle Verbindungen** Seite, wählen Sie den Quellserver.
3. Wählen Sie **Funktion "Speicherreplikat"** aus dem Bereich "Tools".
4. Wählen Sie **neu** um eine neue Partnerschaft zu erstellen.
5. Geben Sie die Details der Partnerschaft, und wählen Sie dann **erstellen**. <br>
![Der neue Partnerschaft-Bildschirm mit Details der Partnerschaft, z. B. eine Protokollgröße von 8 GB.](media\Storage-Replica-UI\Honolulu_SR_Create_Partnership.png)

    **Abbildung 3: Erstellen eine neue Partnerschaft**

> [!NOTE]
> Die Partnerschaft Entfernen von Funktion "Speicherreplikat" in Windows Admin Center nicht die Replikationsgruppe Namens.

### <a name="using-windows-powershell"></a>Verwenden von Windows PowerShell

Als nächsten Schritt konfigurieren Sie die Server-zu-Server-Replikation mit Windows PowerShell. Die unten beschriebenen Schritte müssen unmittelbar auf den Knoten oder direkt über einen Remoteverwaltungscomputer ausgeführt werden, auf dem die RSAT-Verwaltungstools von Windows Server 2016 installiert sind.  

1. Stellen Sie sicher, dass Sie eine PowerShell-Konsole mit erhöhten Rechten als Administrator verwenden.  
2. Konfigurieren Sie die Server-zu-Server-Replikation, und geben Sie dabei die Quell- und Zieldatenträger, die Quell- und Zielprotokolle, die Quell- und Zielknoten sowie die Protokollgröße an.  

    ```PowerShell  
    New-SRPartnership -SourceComputerName sr-srv05 -SourceRGName rg01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName sr-srv06 -DestinationRGName rg02 -DestinationVolumeName f: -DestinationLogVolumeName g:  
    ```  

   Ausgabe:
   ```PowerShell
   DestinationComputerName : SR-SRV06
   DestinationRGName       : rg02
   SourceComputerName      : SR-SRV05
   PSComputerName          :
   ```

    > [!IMPORTANT]
    > Die standardmäßige Protokollgröße beträgt 8GB. Abhängig von den Ergebnissen des Cmdlets `Test-SRTopology` können Sie -LogSizeInBytes mit einem höheren oder niedrigeren Wert verwenden.  

2.  Verwenden Sie `Get-SRGroup` und `Get-SRPartnership` wie folgt, um den Quell- und Zielzustand der Replikation abzurufen:  

    ```PowerShell  
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```
    Ausgabe:

    ```PowerShell
    CurrentLsn             : 0
    DataVolume             : F:\
    LastInSyncTime         :
    LastKnownPrimaryLsn    : 1
    LastOutOfSyncTime      :
    NumOfBytesRecovered    : 37731958784
    NumOfBytesRemaining    : 30851203072
    PartitionId            : c3999f10-dbc9-4a8e-8f9c-dd2ee6ef3e9f
    PartitionSize          : 68583161856
    ReplicationMode        : synchronous
    ReplicationStatus      : InitialBlockCopy
    PSComputerName         :
    ```

3.  Bestimmen Sie den Fortschritt der Replikation wie folgt:  

    1.  Führen Sie auf dem Quellserver den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5015, 5002, 5004, 1237, 5001 und 2200:  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20  
        ```  

    2.  Führen Sie auf dem Zielserver den folgenden Befehl aus, um die Speicherreplikatereignisse anzuzeigen, die das Erstellen der Partnerschaft belegen. Dieses Ereignis gibt die Anzahl der kopierten Bytes sowie die dafür benötigte Zeit an. Beispiel:  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  
        ```
        Ausgabebeispiel:
        ```
        TimeCreated  : 4/8/2016 4:12:37 PM  
        ProviderName : Microsoft-Windows-StorageReplica  
        Id           : 1215  
        Message      : Block copy completed for replica.  

        ReplicationGroupName: rg02  
        ReplicationGroupId: {616F1E00-5A68-4447-830F-B0B0EFBD359C}  
        ReplicaName: f:\  
        ReplicaId: {00000000-0000-0000-0000-000000000000}  
        End LSN in bitmap:   
        LogGeneration: {00000000-0000-0000-0000-000000000000}  
        LogFileId: 0  
        CLSFLsn: 0xFFFFFFFF  
        Number of Bytes Recovered: 68583161856  
        Elapsed Time (ms): 117  
        ```  

        > [!NOTE]
        > Das Speicherreplikatfeature hebt die Bereitstellung der Zielvolumes sowie der zugehörigen Laufwerkbuchstaben oder Bereitstellungspunkte auf. Dies ist entwurfsbedingt.  

    3.  Alternativ gibt die Zielservergruppe für das Replikat jederzeit die Anzahl der noch zu kopierenden Bytes an. Dieser Wert kann auch über PowerShell abgefragt werden. Zum Beispiel:  

        ```PowerShell  
        (Get-SRGroup).Replicas | Select-Object numofbytesremaining  
        ```  

        Beispiel für den Fortschritt (das nicht beendet wird):  

        ```PowerShell  
        while($true) {  

         $v = (Get-SRGroup -Name "RG02").replicas | Select-Object numofbytesremaining  
         [System.Console]::Write("Number of bytes remaining: {0}`r", $v.numofbytesremaining)  
         Start-Sleep -s 5  
        }  
        ```  

    4.  Führen Sie auf dem Zielserver den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5009, 1237, 5001, 5015, 5005 und 2200, um Informationen zum Verarbeitungsfortschritt zu erhalten. Diese Abfolge sollte keine Warnungen oder Fehler enthalten. Es werden eine Vielzahl von Ereignissen des Typs 1237 angezeigt, die für den Fortschritt stehen.  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

## <a name="step-4-manage-replication"></a>Schritt 4: Verwalten der Replikation

Nachfolgend sind die Schritte zur Verwaltung Ihrer Server-zu-Server-Replikationsinfrastruktur beschrieben. Die unten beschriebenen Schritte können unmittelbar auf den Knoten oder über einen Remoteverwaltungscomputer ausgeführt werden, auf dem die RSAT-Verwaltungstools von Windows Server 2016 installiert sind.  

1.  Verwenden Sie `Get-SRPartnership` und `Get-SRGroup`, um die aktuelle Quelle und das aktuelle Ziel der Replikation sowie den zugehörigen Status zu ermitteln.  

2.  Zum Ermitteln der Replikationsleistung verwenden Sie das Cmdlet `Get-Counter` sowohl auf dem Quell- als auch auf dem Zielknoten. Es werden folgende Leistungsindikatoren verwendet:  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Häufigkeit, mit der die Leerung angehalten wurde  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl ausstehender Leerungs-E/As  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anforderungen für letzten Schreibvorgang im Protokoll  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschn. Länge der Warteschlange zum Leeren  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Aktuelle Länge der Warteschlange zum Leeren  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anwendungsschreibanforderungen  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschn. Anzahl von Anforderungen pro Protokollschreibvorgang  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschn. Wartezeit für App-Schreibvorgang  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Durchschn. Wartezeit für App-Lesevorgang  

    -   \Speicherreplikatstatistik(*)\Ziel-RPO  

    -   \Speicherreplikatstatistik(*)\Aktuelle RPO  

    -   \Speicherreplikatstatistik(*)\Durchschn. Länge der Protokollwarteschlange  

    -   \Speicherreplikatstatistik(*)\Aktuelle Länge der Protokollwarteschlange  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl empfangener Bytes  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl gesendeter Bytes  

    -   \Speicherreplikatstatistik(*)\Durchschn. Wartezeit beim Senden über das Netzwerk  

    -   \Speicherreplikatstatistik(*)\Replikationszustand  

    -   \Speicherreplikatstatistik(*)\Durchschn. Wartezeit bei Nachrichtenroundtrip  

    -   \Speicherreplikatstatistik(*)\Verstrichene Zeit bei letzter Wiederherstellung  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Max. Protokollfolgenummer  

    -   \Speicherreplikatstatistik(*)\Anzahl empfangener Nachrichten  

    -   \Speicherreplikatstatistik(*)\Anzahl gesendeter Nachrichten  

    Weitere Informationen zu Leistungsindikatoren in Windows PowerShell finden Sie unter [Get-Counter](https://technet.microsoft.com/library/hh849685.aspx).  

3.  Zum Ändern der Replikationsrichtung eines Standorts verwenden Sie das Cmdlet `Set-SRPartnership`.  

    ```PowerShell  
    Set-SRPartnership -NewSourceComputerName sr-srv06 -SourceRGName rg02 -DestinationComputerName sr-srv05 -DestinationRGName rg01  
    ```  

    > [!WARNING]  
    > Windows Server 2016 verhindert einen Rollenwechsel während der ersten Synchronisierung. Es kann zu Datenverlust führen, wenn Sie vor Abschluss der ersten Replikation versuchen, einen Wechsel vorzunehmen. Erzwungen Sie Switch-Anweisungen nicht werden, bis die erste Synchronisierung abgeschlossen ist.  

    Überprüfen Sie die Ereignisprotokolle auf eine Richtungsänderung bei der Replikation und einen Wiederherstellungsmodus, und bringen Sie die Konfiguration in Einklang. Schreib-E/As können anschließend in den Speicher schreiben, der sich im Besitz des neuen Quellservers befindet. Durch das Ändern der Replikationsrichtung werden Schreib-E/As auf dem vorherigen Quellcomputer verhindert.  

4.  Zum Entfernen der Replikation verwenden Sie `Get-SRGroup`, `Get-SRPartnership`, `Remove-SRGroup` und `Remove-SRPartnership` auf jedem Knoten. Führen Sie das Cmdlet `Remove-SRPartnership` keinesfalls auf dem Zielserver, sondern lediglich auf der aktuellen Replikationsquelle aus. Führen Sie `Remove-Group` auf beiden Servern aus. So entfernen Sie die Replikation z. B. vollständig von zwei Servern:  

    ```powershell
    Get-SRPartnership  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

## <a name="replacing-dfs-replication-with-storage-replica"></a>Ersetzen der DFS-Replikation durch Speicherreplikate  
Viele Microsoft-Kunden stellen die DFS-Replikation als Notfallwiederherstellungslösung für unstrukturierte Benutzerdaten wie Basisordner und Abteilungsfreigaben bereit. DFS-Replikation wurde in Windows Server 2003 R2 und allen späteren Betriebssystemen bereitgestellt und kann in Netzwerken mit geringer Bandbreite eingesetzt werden. Daher eignet sich diese Replikation für Umgebungen mit einer Vielzahl von Knoten, die durch eine hohe Latenz und wenige Änderungen gekennzeichnet sind. DFS-Replikation hat jedoch deutliche Einschränkungen als Lösung zur Replikation von Daten:  
* Er replizieren nicht verwendet werden oder geöffnete Dateien.  
* Er replizieren nicht synchron.  
* Bei der asynchronen Replikation kann eine Wartezeit von mehreren Minuten, Stunden oder sogar Tagen auftreten.  
* DFSR ist von einer Datenbank abhängig, für die nach einer Unterbrechung der Stromversorgung lange Konsistenzprüfungen erforderlich sein können.  
* Es ist in der Regel als Multimaster konfiguriert, die Änderungen in beide Richtungen übertragen werden kann, wobei neuere Daten überschrieben.  

Bei Speicherreplikaten gelten keine dieser Einschränkungen. Allerdings müssen auch hier eine Reihe von Einschränkungen berücksichtigt werden, aufgrund derer sich diese Art der Replikation für einige Umgebungen weniger gut eignet:  

* Lediglich eine 1:1-Replikation zwischen Volumes ist möglich. Es ist möglich, verschiedene Volumes zwischen mehreren Server repliziert.  
* Während eine asynchrone Replikation unterstützt, ist es nicht für mit niedriger Bandbreite und Netzwerke mit hoher Latenz ausgelegt.  
* Es können Benutzerzugriff auf die geschützten Daten auf dem Zielserver nicht zulassen, während der Replikation ist  

Wenn diese Faktoren nicht entscheidend sind, kann das Speicherreplikatfeature eingesetzt werden, um DFS-Replikatserver durch diese neuere Technologie zu ersetzen.   
Nachfolgend finden Sie einen groben Überblick über die erforderlichen Schritte:  

1.  Installieren Sie Windows Server 2016 auf zwei Servern, und konfigurieren Sie Ihren Speicher. Sie können entweder zwei vorhandene Server upgraden oder eine Neuinstallation durchführen.  
2.  Stellen Sie sicher, dass die Daten, die repliziert werden sollen, sich auf mindestens einem Datenvolume und nicht Laufwerk C: befinden.   
a.  Sie können auch ein Seeding für die Daten auf dem anderen Server durchführen, um den Zeitaufwand zu reduzieren. Dabei werden eine Sicherung oder Dateikopien verwendet. Außerdem ist eine schlanke Speicherzuweisung möglich. Im Gegensatz zu DFS-Replikation ist eine exakte Übereinstimmung mit der metadatenähnlichen Sicherheit nicht erforderlich.  
3.  Teilen Sie die Daten auf dem Quellserver, und legen Sie sie über einen DFS-Namespace zugegriffen werden. Dies ist wichtig, um sicherzustellen, dass Benutzer weiterhin auf die Daten zugreifen können, wenn der Servername in einen Namen an einem Notfallstandort geändert wird.  
a.  Sie können übereinstimmende Freigaben auf dem Zielserver erstellen, die im normalen Betrieb nicht verfügbar sind   
b.  Nicht dem DFS-Namespace mit den Zielserver hinzugefügt, oder wenn Sie dies tun, stellen Sie sicher, dass sämtliche Ordnerziele deaktiviert sind.  
4.  Aktivieren Sie die Speicherreplikatreplikation, und führen Sie die erste Synchronisierung durch. Die Replikation kann synchron oder asynchron durchgeführt werden.   
a.  Um E/A-Datenkonsistenz auf dem Zielserver sicherzustellen, wird jedoch eine synchrone Replikation empfohlen.   
b.  Es wird dringend empfohlen, Volumeschattenkopien zu aktivieren und regelmäßig Momentaufnahmen mit VSSADMIN oder einem anderen Tool Ihrer Wahl zu erstellen. Dadurch wird sichergestellt, dass Anwendungen ihre Daten konsistent auf den Datenträgern speichern. Bei einem Notfall können Sie Dateien anhand von Momentaufnahmen auf dem Zielserver wiederherstellen, die möglicherweise teilweise asynchron repliziert wurden. Momentaufnahmen werden gemeinsam mit den Dateien repliziert.  
5.  Nehmen Sie den normalen Betrieb auf, bis eine Notfallsituation eintritt.  
6.  Ändern Sie den Zielserver in den neuen Quellserver, sodass die replizierten Volumes für die Benutzer angezeigt werden.  
7.  Bei Verwendung der synchronen Replikation ist nur dann eine Datenwiederherstellung erforderlich, wenn der Benutzer eine Anwendung verwendet hat, die beim Ausfall des Quellservers Daten ohne Transaktionsschutz (unabhängig von der Replikation) geschrieben hat. Bei Verwendung der asynchronen Replikation sollte eine VSS-Momentaufnahmenbereitstellung verwendet werden. Sie sollten die Verwendung von VSS jedoch in allen Situationen in Betracht ziehen, um anwendungskonsistente Momentaufnahmen bereitzustellen.  
8.  Fügen Sie den Server und seine Freigaben als DFS-Namespaces Ordnerziel hinzu.   
9.  Die Benutzer können anschließend auf ihre Daten zugreifen.  

 > [!NOTE]
 > Die Notfallwiederherstellungsplanung ist ein komplexes Thema, das mit größter Sorgfalt behandelt werden muss. Es wird dringend empfohlen, Runbooks zu erstellen und jährliche Livefailoverdrills durchzuführen. Wenn tatsächlich eine Notfallsituation eintritt, können die Abläufe chaotisch sein, und erfahrene Mitarbeiter sind möglicherweise nicht verfügbar.  

## <a name="add-azure-vm-expressroute"></a>Hinzufügen einer Azure-VM mit Ihrem Netzwerk über ExpressRoute verbunden

1. [Erstellen Sie eine expressroute-Verbindung im Azure-Portal](https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager).<br>Nachdem die ExpressRoute eine Ressourcengruppe wird die Abonnement - hinzugefügt genehmigt wurde, navigieren Sie zu **Ressourcengruppen** dieser neuen Gruppe anzeigen. Notieren Sie sich der Name des virtuellen Netzwerks.
![Azure-Portal mit der Ressourcengruppe, die mit ExpressRoute hinzugefügt](media/Server-to-Server-Storage-Replication/express-route-resource-group.png)
    
    **Abbildung 4: Notieren Sie sich Name des virtuellen Netzwerks mit einer ExpressRoute - verbundenen Ressourcen**
1. [Erstellen Sie eine neue Ressourcengruppe](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).
1. [Hinzufügen eine Netzwerksicherheitsgruppe](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal). Wenn Sie es erstellen, wählen Sie die Abonnement-ID verknüpft ist, mit der ExpressRoute, die Sie erstellt haben, und wählen Sie die Ressourcengruppe aus, die Sie gerade ebenfalls erstellt haben.
<br><br>Fügen Sie eingehende und ausgehende Sicherheitsregeln, die Sie benötigen die Netzwerksicherheitsgruppe hinzu. Beispielsweise empfiehlt es sich um Remotedesktop auf dem virtuellen Computer zu ermöglichen.
1. [Erstellen einer Azure-VM](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal) mit den folgenden Einstellungen (siehe Abbildung 5):
    - **Öffentliche IP-Adresse**: Keine
    - **Virtuelles Netzwerk**: Wählen Sie das virtuelle Netzwerk, das Sie sich aus der Ressourcengruppe, die mit ExpressRoute hinzugefügt haben.
    - **Netzwerksicherheitsgruppe (Firewall)**: Wählen Sie die Netzwerksicherheitsgruppe, die Sie zuvor erstellt haben.
    ![Erstellen Sie mit der ExpressRoute-Netzwerkeinstellungen VM](media/Server-to-Server-Storage-Replication/azure-vm-express-route.png)
    **Abbildung 5: Erstellen eines virtuellen Computers beim Auswählen von Netzwerkeinstellungen für ExpressRoute**
1. Nachdem der virtuelle Computer erstellt wurde, finden Sie unter [Schritt2: Bereitstellen von Betriebssystem, Features, Rollen, Speicher und Netzwerk](#provision-os).


## <a name="related-topics"></a>Verwandte Themen  
- [Übersicht über Speicherreplikate](storage-replica-overview.md)  
- [Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Cluster-zu-Cluster-Speicherreplikation](cluster-to-cluster-storage-replication.md)
- [Funktion "Speicherreplikat": Bekannte Probleme](storage-replica-known-issues.md)  
- [Funktion "Speicherreplikat": Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)
- ["Direkte Speicherplätze" unter WindowsServer 2016](../storage-spaces/storage-spaces-direct-overview.md)  
