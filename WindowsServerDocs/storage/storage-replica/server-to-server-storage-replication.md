---
title: Server-zu-Server-Speicher Replikation
description: Einrichten und Verwenden von Speicher Replikaten für die Server-zu-Server-Replikation in Windows Server, einschließlich Windows Admin Center und PowerShell.
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 03/26/2020
ms.assetid: 61881b52-ee6a-4c8e-85d3-702ab8a2bd8c
ms.openlocfilehash: b49c626bd5b8630d375c2984eac96a32b703cd2c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964102"
---
# <a name="server-to-server-storage-replication-with-storage-replica"></a>Server-zu-Server-Speicher Replikation mit Speicher Replikat

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

Mithilfe der Speicherreplikation können Sie zwei Server konfigurieren, um die Daten zu synchronisieren, sodass jeder Server über eine identische Kopie des gleichen Volumes verfügt. Dieses Thema enthält Hintergrundinformationen zu dieser Konfiguration einer Server-zu-Server-Replikation sowie zum Einrichten und Verwalten der Umgebung.

Zum Verwalten des Speicher Replikats können Sie [Windows Admin Center](../../manage/windows-admin-center/overview.md) oder PowerShell verwenden.

Im folgenden finden Sie ein Übersichts Video zur Verwendung des Speicher Replikats im Windows Admin Center.
> [!video https://www.microsoft.com/videoplayer/embed/3aa09fd4-867b-45e9-953e-064008468c4b?autoplay=false]


## <a name="prerequisites"></a>Voraussetzungen  

* Active Directory Domain Services Gesamtstruktur (Windows Server 2016 muss nicht ausgeführt werden).  
* Zwei Server, auf denen Windows Server 2019 oder Windows Server 2016, Datacenter Edition ausgeführt wird. Wenn Sie Windows Server 2019 ausführen, können Sie stattdessen die Standard Edition verwenden, wenn Sie nur ein einzelnes Volume mit einer Größe von bis zu 2 TB replizieren möchten.  
* Zwei Speichergruppen, die SAS-JBODs, Fibre Channel-SANs, iSCSI-Ziele oder lokalen SCSI/SATA-Speicher verwenden. Der Speicher sollte eine Kombination aus HDD- und SSD-Medien umfassen. Die einzelnen Speichergruppen werden nur für jeweils einen Server bereitgestellt, ein gemeinsamer Zugriff wird nicht konfiguriert.  
* Jede Speichergruppe muss das Erstellen von mindestens zwei virtuellen Datenträgern ermöglichen, einen Datenträger für replizierte Daten und einen Datenträger für Protokolle. Der physische Speicher muss auf allen Datenträgern für Daten dieselben Sektorgrößen aufweisen. Der physische Speicher muss auf allen Datenträgern für Protokolle dieselben Sektorgrößen aufweisen.  
* Mindestens eine Ethernet/TCP-Verbindung auf jedem Server für die synchrone Replikation (vorzugsweise RDMA).   
* Geeignete Firewall- und Routerregeln, um bidirektionalen ICMP-Datenverkehr, SMB-Datenverkehr (Port 445 sowie 5445 für SMB Direct) und WS-MAN-Datenverkehr (Port 5985) zwischen allen Knoten zu ermöglichen.  
* Ein Netzwerk zwischen den Servern mit ausreichender Bandbreite für Ihre E/A-Schreibworkload sowie durchschnittlich 5 ms Roundtriplatenz für die synchrone Replikation. Bei der asynchronen Replikation ist keine Latenz Empfehlung vorhanden.<br>
Wenn Sie zwischen lokalen Servern und virtuellen Azure-Computern replizieren, müssen Sie eine Netzwerkverbindung zwischen den lokalen Servern und den Azure-VMS erstellen. Verwenden Sie hierzu [Express Route](#add-azure-vm-expressroute), eine [Standort-zu-Standort-VPN-Gatewayverbindung](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal), oder installieren Sie VPN-Software auf Ihren virtuellen Azure-Computern, um Sie mit Ihrem lokalen Netzwerk zu verbinden.
* Der replizierte Speicher darf sich nicht auf dem Laufwerk mit dem Ordner des Windows-Betriebssystems befinden.

> [!IMPORTANT]
>  In diesem Szenario sollte sich jeder Server an einem anderen physischen oder logischen Standort befinden. Die Server müssen über das Netzwerk miteinander kommunizieren können.  


Viele dieser Voraussetzungen lassen sich mit dem `Test-SRTopology cmdlet` ermitteln. Sie erhalten Zugang zu diesem Tool, wenn Sie das Speicherreplikatfeature oder die Speicherreplikat-Verwaltungstools auf mindestens einem Server installieren. Das Speicherreplikatfeature muss nicht konfiguriert werden, um dieses Tool verwenden zu können. Es wird lediglich zur Installation des Cmdlets benötigt. Weitere Informationen finden Sie in den nachfolgend beschriebenen Schritten.  

## <a name="windows-admin-center-requirements"></a>Windows Admin Center-Anforderungen

Zum gemeinsamen Verwenden von Speicher Replikat und Windows Admin Center benötigen Sie Folgendes:

| System                        | Betriebssystem                                            | Erforderlich für     |
|-------------------------------|-------------------------------------------------------------|------------------|
| Zwei Server <br>(eine Kombination aus lokaler Hardware, VMS und virtuellen Cloud-Computern einschließlich Azure-VMS)| Windows Server 2019, Windows Server 2016 oder Windows Server (halbjährlicher Kanal) | Speicherreplikat  |
| Ein PC                     | Windows 10                                                  | Windows Admin Center |

> [!NOTE]
> Zurzeit können Sie Windows Admin Center nicht auf einem Server zum Verwalten des Speicher Replikats verwenden.

## <a name="terms"></a>Bestimmungen  
Für diese exemplarische Vorgehensweise wird die folgende Beispielumgebung verwendet:  

-   Zwei Server: **SR-SRV05** und **SR-SRV06**  

-   Ein Paar aus logischen „Standorten“, die für zwei unterschiedliche Rechenzentren stehen: **Redmond** und **Bellevue**.  

![Diagramm, das einen Server in Gebäude 5 zeigt, der mit einem Server in Gebäude 9 repliziert wird](media/Server-to-Server-Storage-Replication/Storage_SR_ServertoServer.png)  

**Abbildung 1: Server-zu-Server-Replikation**  

## <a name="step-1-install-and-configure-windows-admin-center-on-your-pc"></a>Schritt 1: Installieren und Konfigurieren des Windows Admin Centers auf dem PC

Wenn Sie das Speicher Replikat mithilfe des Windows Admin Centers verwalten, führen Sie die folgenden Schritte aus, um Ihren PC für die Verwaltung des Speicher Replikats vorzubereiten.
1. Laden Sie [Windows Admin Center](../../manage/windows-admin-center/overview.md)herunter, und installieren Sie es.
2. Laden Sie den [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520)herunter und installieren Sie ihn.
    - Wenn Sie Windows 10, Version 1809 oder höher, verwenden, installieren Sie das "RSAT: Storage Replica Module for Windows PowerShell" von Features bei Bedarf.
3. Öffnen Sie eine PowerShell-Sitzung als Administrator, indem Sie die Schaltfläche **Start** auswählen, **PowerShell**eingeben, mit der rechten Maustaste auf **Windows PowerShell** klicken und dann **als Administrator ausführen**auswählen.
4. Geben Sie den folgenden Befehl ein, um das WS-Verwaltungs Protokoll auf dem lokalen Computer zu aktivieren, und richten Sie die Standardkonfiguration für die Remote Verwaltung auf dem Client ein.

    ```PowerShell
    winrm quickconfig
    ```

5. Geben Sie **Y** ein, um WinRM-Dienste zu aktivieren und die WinRM-Firewallausnahme

## <a name="step-2-provision-operating-system-features-roles-storage-and-network"></a><a name="provision-os"></a>Schritt 2: Bereitstellen von Betriebssystem, Features, Rollen, Speicher und Netzwerk

1.  Installieren Sie Windows Server auf beiden Server Knoten mit dem Installationstyp Windows Server **(Desktop Darstellung)**. 
 
    Informationen zum Verwenden einer Azure-VM, die mit Ihrem Netzwerk über eine expressroute-Verbindung verbunden ist, finden Sie unter [Hinzufügen eines virtuellen Azure-Computers über expressroute](#add-azure-vm-expressroute).
    
    > [!NOTE]
    > Ab Version 1910 des Windows Admin Centers können Sie einen Zielserver in Azure automatisch konfigurieren. Wenn Sie diese Option auswählen, installieren Sie Windows Server auf dem Quell Server, und fahren Sie dann mit [Schritt 3: Einrichten der Server-zu-Server-Replikation fort](#step-3-set-up-server-to-server-replication). 

3.  Fügen Sie Netzwerkinformationen hinzu, verknüpfen Sie die Server mit der Domäne Ihres Windows 10-Verwaltungs-PCs (falls Sie eine solche verwenden), und starten Sie die Server dann neu.  

    > [!NOTE]
    > Melden Sie sich anschließend stets als Domänenbenutzer an, der Mitglied der integrierten Administratorengruppe auf allen Servern ist. Denken Sie anschließend immer daran, erhöhte Rechte für Ihre PowerShell- und Eingabeaufforderungen festzulegen, wenn Sie die Features auf einer graphischen Serverinstallation oder auf einem Windows 10-Computer ausführen.  

3.  Verbinden Sie den ersten Satz von JBOD-Speicher Gehäuse, iSCSI-Ziel, FC-SAN oder lokalem Festplattenspeicher mit dem Server an Standort **Redmond**.  

4.  Verbinden Sie die zweite Speicher Gruppe mit dem Server an Standort **Bellevue**.  

5.  Installieren Sie gegebenenfalls aktuelle Speicher- und Gehäusefirmware, HBA-Treiber, BIOS/UEFI-Firmware, Netzwerktreiber und Hauptplatinenchipsatz-Treiber der jeweiligen Hersteller auf beiden Knoten. Starten Sie die Knoten gegebenenfalls neu.  

    > [!NOTE]
    > Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.  

6.  Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z.B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die Energie Verwaltung in Windows Server auf hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus.  

7.  Konfigurieren Sie folgende Rollen:  

    -   **Windows Admin Center-Methode**
        1. Navigieren Sie im Windows Admin Center zu Server-Manager, und wählen Sie dann einen der Server aus.
        2. Navigieren Sie zu **Rollen & Features**.
        3. Wählen Sie **Features**  >  **Speicher Replikat**, und klicken Sie dann auf **Installieren**.
        4. Wiederholen Sie den Vorgang auf dem anderen Server.
    -   **Server-Manager-Methode**  

        1.  Führen Sie **ServerManager.exe** aus, und erstellen Sie eine Server Gruppe, die alle Server Knoten hinzufügt.  

        2.  Installieren Sie die Rollen und Features **Dateiserver** und **Speicherreplikat** auf allen Knoten, und starten Sie die Knoten neu.  

    -   **Windows PowerShell-Methode**  

        Führen Sie auf SR-SRV06 oder einem Remoteverwaltungscomputer den folgenden Befehl in einer Windows PowerShell-Konsole aus, um die erforderlichen Features und Rollen zu installieren und den Knoten neu zu starten:  

        ```powershell  
        $Servers = 'SR-SRV05','SR-SRV06'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        Weitere Informationen zu diesen Schritten finden Sie unter [installieren oder Deinstallieren von Rollen, Rollen Diensten oder Features](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) .  

8.  Konfigurieren Sie den Speicher wie folgt:  

    > [!IMPORTANT]  
    > -   In jedem Speicherserver müssen zwei Volumes erstellt werden: ein Volume für Daten und ein Volume für Protokolle.  
    > -   Die Datenträger für Protokolle und Daten müssen als GPT (nicht MBR) initialisiert werden.  
    > -   Die beiden Datenvolumes müssen dieselbe Größe aufweisen.  
    > -   Die beiden Protokollvolumes sollten dieselbe Größe aufweisen.  
    > -   Alle Datenträger für replizierte Daten müssen dieselben Sektorgrößen aufweisen.  
    > -   Alle Datenträger für Protokolle müssen dieselben Sektorgrößen aufweisen.  
    > -   Die Protokollvolumes sollten Flash-basierten Speicher verwenden (z. B. SSD). Microsoft empfiehlt, dass der Protokoll Speicher schneller als der Datenspeicher ist. Protokollvolumes dürfen nie für andere Arbeits Auslastungen verwendet werden.
    > -   Die Datenträger für Daten können HDD, SSD oder eine mehrstufige Kombination verwenden. Außerdem kann gespiegelter Speicherplatz oder Paritätsspeicherplatz bzw. RAID 1, RAID 10, RAID 5 oder RAID 50 verwendet werden.  
    > -   Das Protokollvolume muss standardmäßig eine Größe von mindestens 9 GB aufweisen und kann basierend auf Protokollanforderungen möglicherweise größer oder kleiner sein.  
    > -   Die Rolle „Dateiserver“ ist nur für Test-SRTopology erforderlich, um die erforderlichen Firewallports für die Tests zu öffnen.
    
    - **Für JBOD-Gehäuse:**  

        1.  Stellen Sie sicher, dass jedem Server nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die SAS-Verbindungen ordnungsgemäß konfiguriert sind.  

        2.  Stellen Sie den Speicher mithilfe von Speicherplätzen bereit. Führen Sie dazu die unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](../storage-spaces/deploy-standalone-storage-spaces.md) beschriebenen **Schritte 1-3** mithilfe von Windows PowerShell oder über den Server-Manager aus.  

    - **Für iSCSI-Speicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden. Bei Verwendung von iSCSI sollten mehrere Netzwerkkarten verwendet werden.    

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen. Bei Verwendung von Windows-basierten iSCSI-Zielen finden Sie unter [iSCSI-Zielblockspeicher: So wird's gemacht](../iscsi/iscsi-target-server.md) weitere Informationen.  

    - **Für FC-SAN-Speicher:**  

        1.  Stellen Sie sicher, dass jedem Cluster nur die Speichergehäuse des jeweiligen Standorts angezeigt werden und die Zonen für die Hosts ordnungsgemäß festgelegt wurden.   

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen.  

    - **Für lokalen Festplattenspeicher:**  

        -   Stellen Sie sicher, dass der Speicher keine System Volume-, Auslagerungs Datei-oder Dumpdateien enthält.  

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
      > `Diskspd.exe -c1g -d600 -W5 -C5 -b8k -t2 -o2 -r -w5 -i100 -j100 d:\test` 

10. Überprüfen Sie den in Abbildung 2 gezeigten **TestSrTopologyReport.html** -Bericht, um sicherzustellen, dass Sie die Speicher Replikat Anforderungen erfüllen.  

    ![Bildschirm mit Topologiebericht](media/Server-to-Server-Storage-Replication/SRTestSRTopologyReport.png)

    **Abbildung 2: Bericht zur Speicher Replikations Topologie**

## <a name="step-3-set-up-server-to-server-replication"></a>Schritt 3: Einrichten der Server-zu-Server-Replikation
### <a name="using-windows-admin-center"></a>Verwenden des Windows Admin Centers

1. Fügen Sie den Quell Server hinzu.
    1. Wählen Sie die Schaltfläche **Hinzufügen** aus.
    2. Wählen Sie **Server Verbindung hinzufügen**aus.
    3. Geben Sie den Namen des Servers ein, und wählen Sie dann **senden**aus.
2. Wählen Sie auf der Seite **alle Verbindungen** den Quell Server aus.
3. Wählen Sie im Werkzeug Panel **Speicher Replikat** aus.
4. Wählen Sie **neu** aus, um eine neue Partnerschaft zu erstellen. So erstellen Sie einen neuen virtuellen Azure-Computer, der als Ziel für die Partnerschaft verwendet wird:
   
    1. Wählen Sie unter **Replikation mit einem anderen Server** **neuen virtuellen Azure** -Computer verwenden aus, und klicken Sie auf **weiter**. Wenn diese Option nicht angezeigt wird, stellen Sie sicher, dass Sie Windows Admin Center, Version 1910, oder eine höhere Version verwenden.
    2. Geben Sie die Quell Server Informationen und den Replikations Gruppennamen an, und klicken Sie dann auf **weiter**.<br><br>Dadurch wird ein Prozess gestartet, bei dem automatisch ein virtueller Azure-Computer unter Windows Server 2019 oder Windows Server 2016 als Ziel für die Migrations Quelle ausgewählt wird. Storage Migration Service empfiehlt VM-Größen, die ihrer Quelle entsprechen. Sie können dies jedoch überschreiben, indem Sie **alle Größen**anzeigen auswählen. Inventur Daten werden verwendet, um Ihre verwalteten Datenträger und Ihre Dateisysteme automatisch zu konfigurieren und ihre neue Azure-VM mit Ihrer Active Directory Domäne zu verknüpfen.
    3. Nachdem das Windows Admin Center die Azure-VM erstellt hat, geben Sie einen Replikations Gruppennamen an, und wählen Sie dann **Erstellen** Das Windows Admin Center beginnt dann mit der erst Synchronisierung des normalen Speicher Replikats, um die Daten zu schützen.
    
    Im folgenden Video wird gezeigt, wie Sie das Speicher Replikat für die Migration zu Azure-VMS verwenden.

    > [!VIDEO https://www.youtube-nocookie.com/embed/_VqD7HjTewQ] 

5. Geben Sie die Details der Partnerschaft an, und wählen Sie dann **Erstellen** aus (wie in Abbildung 3 dargestellt). <br>
   ![Der Bildschirm "neue Partnerschaft" zeigt Partnerschafts Details an, z. b. eine Protokoll Größe von 8 GB.](media/Storage-Replica-UI/Honolulu_SR_Create_Partnership.png)

    **Abbildung 3: Erstellen einer neuen Partnerschaft**

> [!NOTE]
> Beim Entfernen der Partnerschaft aus dem Speicher Replikat im Windows Admin Center wird der Replikations Gruppenname nicht entfernt.

### <a name="using-windows-powershell"></a>Verwenden von Windows PowerShell

Als nächsten Schritt konfigurieren Sie die Server-zu-Server-Replikation mit Windows PowerShell. Sie müssen alle Schritte unten auf den Knoten direkt oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

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
    > Die standardmäßige Protokollgröße beträgt 8 GB. Abhängig von den Ergebnissen des Cmdlets `Test-SRTopology` können Sie -LogSizeInBytes mit einem höheren oder niedrigeren Wert verwenden.  

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
        Hier ist eine Beispielausgabe angegeben:
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
        > Das Speicherreplikatfeature hebt die Bereitstellung der Zielvolumes sowie der zugehörigen Laufwerkbuchstaben oder Bereitstellungspunkte auf. Dies ist beabsichtigt.  

    3.  Alternativ gibt die Zielservergruppe für das Replikat jederzeit die Anzahl der noch zu kopierenden Bytes an. Dieser Wert kann auch über PowerShell abgefragt werden. Beispiel:  

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

Nachfolgend sind die Schritte zur Verwaltung Ihrer Server-zu-Server-Replikationsinfrastruktur beschrieben. Sie können alle nachfolgenden Schritte direkt auf den Knoten oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

1.  Verwenden Sie `Get-SRPartnership` und `Get-SRGroup`, um die aktuelle Quelle und das aktuelle Ziel der Replikation sowie den zugehörigen Status zu ermitteln.  

2.  Zum Ermitteln der Replikationsleistung verwenden Sie das Cmdlet `Get-Counter` sowohl auf dem Quell- als auch auf dem Zielknoten. Es werden folgende Leistungsindikatoren verwendet:  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Häufigkeit, mit der die Leerung angehalten wurde  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl ausstehender Leerungs-E/As  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anforderungen für letzten Schreibvorgang im Protokoll  

    -   \Speicherreplikatspartitions-e/a-Statistik (*) \Durchschnittl. Länge der Warteschlange  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Aktuelle Länge der Warteschlange zum Leeren  

    -   \Statistik zur Partitions-E/A des Speicherreplikats(*)\Anzahl von Anwendungsschreibanforderungen  

    -   \E/a-Statistiken für die Speicher Replikat Partition (*) \Durchschnittl. Anzahl der Anforderungen pro Protokoll Schreibvorgang  

    -   \E/a-Statistiken für die Speicher Replikat Partition (*) \avg. app-Schreib Latenz  

    -   \E/a-Statistiken für die Speicher Replikat Partition (*) \avg. app-Lese Latenz  

    -   \Speicherreplikatstatistik(*)\Ziel-RPO  

    -   \Speicherreplikatstatistik(*)\Aktuelle RPO  

    -   \Speicherreplikatstatistik (*) \Durchschnittl. Länge der Protokoll Warteschlange  

    -   \Speicherreplikatstatistik(*)\Aktuelle Länge der Protokollwarteschlange  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl empfangener Bytes  

    -   \Speicherreplikatstatistik(*)\Gesamtanzahl gesendeter Bytes  

    -   \Speicherreplikatstatistik (*) \Durchschnittl. Netzwerk-Sende Latenz  

    -   \Speicherreplikatstatistik(*)\Replikationszustand  

    -   \Speicherreplikatstatistik (*) \Durchschnittl. Nachrichten Roundtrip-Latenz  

    -   \Speicherreplikatstatistik(*)\Verstrichene Zeit bei letzter Wiederherstellung  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Wiederherstellungstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl geleerter Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Anzahl von Replikationstransaktionen  

    -   \Speicherreplikatstatistik(*)\Max. Protokollfolgenummer  

    -   \Speicherreplikatstatistik(*)\Anzahl empfangener Nachrichten  

    -   \Speicherreplikatstatistik(*)\Anzahl gesendeter Nachrichten  

    Weitere Informationen zu Leistungsindikatoren in Windows PowerShell finden Sie unter [Get-Counter](/powershell/module/microsoft.powershell.diagnostics/get-counter).  

3.  Zum Ändern der Replikationsrichtung eines Standorts verwenden Sie das Cmdlet `Set-SRPartnership`.  

    ```PowerShell  
    Set-SRPartnership -NewSourceComputerName sr-srv06 -SourceRGName rg02 -DestinationComputerName sr-srv05 -DestinationRGName rg01  
    ```  

    > [!WARNING]  
    > Windows Server verhindert den Rollenwechsel, wenn die erste Synchronisierung ausgeführt wird, da dies zu Datenverlusten führen kann, wenn Sie versuchen, den Vorgang zu beenden, bevor die erste Replikation abgeschlossen werden kann. Erzwingen Sie die switchrichtung erst, wenn die erste Synchronisierung beendet ist.  

    Überprüfen Sie die Ereignisprotokolle auf eine Richtungsänderung bei der Replikation und einen Wiederherstellungsmodus, und bringen Sie die Konfiguration in Einklang. Schreib-E/As können anschließend in den Speicher schreiben, der sich im Besitz des neuen Quellservers befindet. Durch das Ändern der Replikationsrichtung werden Schreib-E/As auf dem vorherigen Quellcomputer verhindert.  

4.  Zum Entfernen der Replikation verwenden Sie `Get-SRGroup`, `Get-SRPartnership`, `Remove-SRGroup` und `Remove-SRPartnership` auf jedem Knoten. Führen Sie das Cmdlet `Remove-SRPartnership` keinesfalls auf dem Zielserver, sondern lediglich auf der aktuellen Replikationsquelle aus. Führen Sie `Remove-Group` auf beiden Servern aus. So entfernen Sie die Replikation z. B. vollständig von zwei Servern:  

    ```powershell
    Get-SRPartnership  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

## <a name="replacing-dfs-replication-with-storage-replica"></a>Ersetzen der DFS-Replikation durch Speicherreplikate  
Viele Microsoft-Kunden stellen die DFS-Replikation als Notfallwiederherstellungslösung für unstrukturierte Benutzerdaten wie Basisordner und Abteilungsfreigaben bereit. DFS-Replikation wurde in Windows Server 2003 R2 und allen späteren Betriebssystemen bereitgestellt und kann in Netzwerken mit geringer Bandbreite eingesetzt werden. Daher eignet sich diese Replikation für Umgebungen mit einer Vielzahl von Knoten, die durch eine hohe Latenz und wenige Änderungen gekennzeichnet sind. DFS-Replikation hat jedoch deutliche Einschränkungen als Lösung zur Replikation von Daten:  
* Sie repliziert keine verwendeten oder geöffneten Dateien.  
* Sie wird nicht synchron repliziert.  
* Bei der asynchronen Replikation kann eine Wartezeit von mehreren Minuten, Stunden oder sogar Tagen auftreten.  
* DFSR ist von einer Datenbank abhängig, für die nach einer Unterbrechung der Stromversorgung lange Konsistenzprüfungen erforderlich sein können.  
* Sie ist im Allgemeinen als multimasterkonfiguration konfiguriert, sodass Änderungen in beide Richtungen übertragen werden können, was möglicherweise neuere Daten überschreibt.  

Bei Speicherreplikaten gelten keine dieser Einschränkungen. Allerdings müssen auch hier eine Reihe von Einschränkungen berücksichtigt werden, aufgrund derer sich diese Art der Replikation für einige Umgebungen weniger gut eignet:  

* Lediglich eine 1:1-Replikation zwischen Volumes ist möglich. Es ist möglich, verschiedene Volumes zwischen mehreren Servern zu replizieren.  
* Obwohl die asynchrone Replikation unterstützt wird, ist Sie nicht für Netzwerke mit geringer Bandbreite und hoher Latenz konzipiert.  
* Der Benutzer kann nicht auf die geschützten Daten auf dem Ziel zugreifen, während die Replikation durchgeführt wird.  

Wenn diese Faktoren nicht entscheidend sind, kann das Speicherreplikatfeature eingesetzt werden, um DFS-Replikatserver durch diese neuere Technologie zu ersetzen.   
Nachfolgend finden Sie einen groben Überblick über die erforderlichen Schritte:  

1. Installieren Sie Windows Server auf zwei Servern, und konfigurieren Sie Ihren Speicher. Sie können entweder zwei vorhandene Server upgraden oder eine Neuinstallation durchführen.  
2. Stellen Sie sicher, dass die Daten, die repliziert werden sollen, sich auf mindestens einem Datenvolume und nicht Laufwerk C: befinden.   
   a)  Sie können auch ein Seeding für die Daten auf dem anderen Server durchführen, um den Zeitaufwand zu reduzieren. Dabei werden eine Sicherung oder Dateikopien verwendet. Außerdem ist eine schlanke Speicherzuweisung möglich. Im Gegensatz zu DFS-Replikation ist eine exakte Übereinstimmung mit der metadatenähnlichen Sicherheit nicht erforderlich.  
3. Teilen Sie die Daten auf dem Quell Server, und machen Sie Sie über einen DFS-Namespace zugänglich. Dies ist wichtig, um sicherzustellen, dass Benutzer weiterhin auf die Daten zugreifen können, wenn der Servername in einen Namen an einem Notfallstandort geändert wird.  
   a)  Sie können übereinstimmende Freigaben auf dem Zielserver erstellen, die im normalen Betrieb nicht verfügbar sind   
   b)  Fügen Sie den Zielserver nicht zum DFS-Namespaces-Namespace hinzu. Wenn Sie dies tun, stellen Sie sicher, dass alle zugehörigen Ordner Ziele deaktiviert sind.  
4. Aktivieren Sie die Speicher Replikat Replikation, und schließen Sie die Die Replikation kann entweder synchron oder asynchron sein.   
   a)  Um E/A-Datenkonsistenz auf dem Zielserver sicherzustellen, wird jedoch eine synchrone Replikation empfohlen.   
   b)  Es wird dringend empfohlen, Volumeschattenkopien zu aktivieren und regelmäßig Momentaufnahmen mit VSSADMIN oder einem anderen Tool Ihrer Wahl zu erstellen. Dadurch wird sichergestellt, dass Anwendungen ihre Daten konsistent auf den Datenträgern speichern. Bei einem Notfall können Sie Dateien anhand von Momentaufnahmen auf dem Zielserver wiederherstellen, die möglicherweise teilweise asynchron repliziert wurden. Momentaufnahmen werden gemeinsam mit den Dateien repliziert.  
5. Nehmen Sie den normalen Betrieb auf, bis eine Notfallsituation eintritt.  
6. Ändern Sie den Zielserver in den neuen Quellserver, sodass die replizierten Volumes für die Benutzer angezeigt werden.  
7. Bei Verwendung der synchronen Replikation ist nur dann eine Datenwiederherstellung erforderlich, wenn der Benutzer eine Anwendung verwendet hat, die beim Ausfall des Quellservers Daten ohne Transaktionsschutz (unabhängig von der Replikation) geschrieben hat. Bei Verwendung der asynchronen Replikation sollte eine VSS-Momentaufnahmenbereitstellung verwendet werden. Sie sollten die Verwendung von VSS jedoch in allen Situationen in Betracht ziehen, um anwendungskonsistente Momentaufnahmen bereitzustellen.  
8. Fügen Sie den Server und seine Freigaben als Ordner Ziel für DFS-Namespaces hinzu.   
9. Die Benutzer können anschließend auf ihre Daten zugreifen.  

   > [!NOTE]
   > Die Notfallwiederherstellungsplanung ist ein komplexes Thema, das mit größter Sorgfalt behandelt werden muss. Es wird dringend empfohlen, Runbooks zu erstellen und jährliche Livefailoverdrills durchzuführen. Wenn tatsächlich eine Notfallsituation eintritt, können die Abläufe chaotisch sein, und erfahrene Mitarbeiter sind möglicherweise nicht verfügbar.  

## <a name="adding-an-azure-vm-connected-to-your-network-via-expressroute"></a><a name="add-azure-vm-expressroute"></a>Hinzufügen einer Azure-VM, die mit Ihrem Netzwerk über expressroute verbunden ist

1. [Erstellen Sie eine expressroute-Verbindung in der Azure-Portal](/azure/expressroute/expressroute-howto-circuit-portal-resource-manager).<br>Nachdem die expressroute-Genehmigung genehmigt wurde, wird dem Abonnement eine Ressourcengruppe hinzugefügt. Navigieren Sie zu **Ressourcengruppen** , um diese neue Gruppe anzuzeigen. Notieren Sie sich den Namen des virtuellen Netzwerks.
![Azure-Portal, der die mit expressroute hinzugefügte Ressourcengruppe anzeigt](media/Server-to-Server-Storage-Replication/express-route-resource-group.png)
    
    **Abbildung 4: die einer expressroute zugeordneten Ressourcen notieren Sie sich den Namen des virtuellen Netzwerks.**
1. [Erstellen Sie eine neue Ressourcengruppe](/azure/azure-resource-manager/resource-group-portal).
1. [Fügen Sie eine Netzwerk Sicherheitsgruppe hinzu](/azure/virtual-network/virtual-networks-create-nsg-arm-pportal). Wählen Sie beim Erstellen die Abonnement-ID aus, die der von Ihnen erstellten expressroute zugeordnet ist, und wählen Sie die Ressourcengruppe aus, die Sie soeben erstellt haben.
<br><br>Fügen Sie alle eingehenden und ausgehenden Sicherheitsregeln, die Sie benötigen, der Netzwerk Sicherheitsgruppe hinzu. Beispielsweise können Sie Remotedesktop Zugriff auf den virtuellen Computer zulassen.
1. [Erstellen Sie eine Azure-VM](/azure/virtual-machines/windows/quick-create-portal) mit den folgenden Einstellungen (siehe Abbildung 5):
    - **Öffentliche IP-Adresse**: keine
    - **Virtuelles Netzwerk**: Wählen Sie das virtuelle Netzwerk aus, das Sie in der mit expressroute hinzugefügten Ressourcengruppe notiert haben.
    - **Netzwerk Sicherheitsgruppe (Firewall)**: Wählen Sie die Netzwerk Sicherheitsgruppe aus, die Sie zuvor erstellt haben.
    ![Erstellen eines virtuellen Computers mit expressroute-Netzwerkeinstellungen ](media/Server-to-Server-Storage-Replication/azure-vm-express-route.png)
     **Abbildung 5: Erstellen eines virtuellen Computers beim Auswählen von expressroute-Netzwerkeinstellungen**
1. Nachdem der virtuelle Computer erstellt wurde, finden Sie weitere Informationen unter [Schritt 2: Bereitstellen von Betriebssystemen, Features, Rollen, Speicher und Netzwerk](#provision-os).


## <a name="related-topics"></a>Verwandte Themen  
- [Übersicht über Speicherreplikate](storage-replica-overview.md)  
- [Stretch-Cluster Replikation mit frei gegebenem Speicher](stretch-cluster-replication-using-shared-storage.md)  
- [Cluster-zu-Cluster Speicher Replikation](cluster-to-cluster-storage-replication.md)
- [Speicher Replikat: bekannte Probleme](storage-replica-known-issues.md)  
- [Speicherreplikat: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)
- [Direkte Speicherplätze in Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)  
