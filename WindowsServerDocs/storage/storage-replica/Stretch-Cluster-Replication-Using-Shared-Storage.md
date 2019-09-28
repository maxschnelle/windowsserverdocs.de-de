---
title: Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher
ms.prod: windows-server
manager: eldenc
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 04/26/2019
ms.assetid: 6c5b9431-ede3-4438-8cf5-a0091a8633b0
ms.openlocfilehash: 654b4aea135c360f5fc5f59fdf85627fe8dd4cc2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402965"
---
# <a name="stretch-cluster-replication-using-shared-storage"></a>Replikation eines Stretched Clusters mithilfe von freigegebenem Speicher

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal)

In diesem Evaluierungsbeispiel konfigurieren Sie die entsprechenden Computer und den zugehörigen Speicher so, dass ein einheitlicher Stretched Cluster entsteht. Dabei nutzen zwei Knoten eine Speichergruppe gemeinsam, und zwei weitere Knoten nutzen eine andere Speichergruppe gemeinsam. Durch die Replikation werden die beiden Speichergruppen im Cluster gespiegelt, sodass ein sofortiges Failover möglich wird. Diese Knoten und der zugehörige Speicher sollten sich an unterschiedlichen physischen Standorten befinden. Dies ist jedoch keine Voraussetzung. Das Erstellen von Hyper-V-Clustern und Dateiserverclustern wird separat mit den entsprechenden Schritten anhand von Beispielszenarios erklärt.  

> [!IMPORTANT]  
> In dieser Evaluierung müssen die Server an den verschiedenen Standorten in der Lage sein, über ein Netzwerk mit anderen Servern zu kommunizieren. Sie dürfen jedoch über keine physische Verbindung mit dem gemeinsam genutzten (bzw. freigegebenen) Speicher des anderen Standorts verfügen. In diesem Szenario werden keine direkten Speicherplätze verwendet.  

## <a name="terms"></a>Benennungen  
Für diese exemplarische Vorgehensweise wird die folgende Beispielumgebung verwendet:  

-   Vier Server mit den Namen **SR-SRV01**, **SR-SRV02**, **SR-SRV03** und **SR-SRV04** bilden einen einheitlichen Cluster mit der Bezeichnung **SR-SRVCLUS**.  

-   Ein Paar aus logischen „Standorten“ steht für zwei unterschiedliche Rechenzentren. Einer dieser logischen „Standorte“ heißt **Redmond** und der andere **Bellevue**.  

> [!NOTE]  
> Alternativ können Sie sogar nur zwei Knoten verwenden. Mit anderen Worten: Sie siedeln jeweils nur einen Knoten an einem Standort an. Allerdings können Sie mit nur zwei Servern kein standortinternes Failover ausführen. Sie können bis zu 64 Knoten verwenden.

![Diagramm mit zwei Knoten in Redmond und der Replikation mit zwei Knoten desselben Clusters am Standort Bellevue](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_StretchClusterExample.png)  

**ABBILDUNG 1:  Speicher Replikation in einem Stretch-Cluster @ no__t-0  

## <a name="prerequisites"></a>Erforderliche Komponenten  
-   Active Directory Domain Services-Gesamtstruktur (in dieser Gesamtstruktur muss nicht Windows Server 2016 ausgeführt werden).  
-   2-64-Server, auf denen Windows Server 2019 oder Windows Server 2016, Datacenter Edition ausgeführt wird. Wenn Sie Windows Server 2019 ausführen, können Sie stattdessen die Standard Edition verwenden, wenn Sie nur ein einzelnes Volume mit einer Größe von bis zu 2 TB replizieren möchten. 
-   Zwei Gruppen von freigegebenem Speicher, die SAS-JBODs (z. B. mit Speicherplätzen), Fibre Channel-SAN, freigegebene VHDX oder iSCSI-Ziel verwenden. Der Speicher muss aus einer Mischung aus Festplatten- und SSD-Medien bestehen und die permanente Reservierung unterstützen. Jede Speichergruppe darf nur für zwei der Server (asymmetrisch) verfügbar gemacht werden.  
-   Jede Speichergruppe muss das Erstellen von mindestens zwei virtuellen Datenträgern ermöglichen, einen Datenträger für replizierte Daten und einen Datenträger für Protokolle. Der physische Speicher muss auf allen Datenträgern für Daten dieselben Sektorgrößen aufweisen. Der physische Speicher muss auf allen Datenträgern für Protokolle dieselben Sektorgrößen aufweisen.  
-   Mindestens eine 1-GbE-Verbindung auf jedem Server für die synchrone Replikation (vorzugsweise RDMA).   
-   Mindestens 2GB RAM und zwei Kerne pro Server. Für mehr virtuelle Computer benötigen Sie mehr Arbeitsspeicher und mehr Kerne.  
-   Geeignete Firewall- und Routerregeln, um bidirektionalen ICMP-Datenverkehr, SMB-Datenverkehr (Port445 sowie 5445 für SMB Direct) und WS-MAN-Datenverkehr (Port5985) zwischen allen Knoten zu ermöglichen.  
-   Ein Netzwerk zwischen den Servern mit ausreichender Bandbreite für Ihre E/A-Schreibworkload sowie durchschnittlich 5 ms Roundtriplatenz für die synchrone Replikation. Für die asynchrone Replikation gilt keine Empfehlung bezüglich der Latenz.  
-   Der replizierte Speicher darf sich nicht auf dem Laufwerk mit dem Ordner des Windows-Betriebssystems befinden.

Das Vorliegen vieler dieser Voraussetzungen lässt sich mit dem `Test-SRTopology`-Cmdlet ermitteln. Sie erhalten Zugang zu diesem Tool, wenn Sie das Speicherreplikatfeature oder die Speicherreplikat-Verwaltungstools auf mindestens einem Server installieren. Das Speicherreplikatfeature muss nicht konfiguriert werden, um dieses Tool verwenden zu können. Es wird lediglich zur Installation des Cmdlets benötigt. Weitere Informationen finden Sie in den folgenden Schritten.  

## <a name="provision-operating-system-features-roles-storage-and-network"></a>Bereitstellen von Betriebssystem, Features, Rollen, Speicher und Netzwerk  

1.  Installieren Sie Windows Server auf allen Server Knoten, und verwenden Sie dabei die Installationsoptionen Server Core oder Server mit Desktop Darstellung.  
    > [!IMPORTANT]
    > Melden Sie sich ab jetzt stets als Domänenbenutzer an, der Mitglied der integrierten Administratorengruppe auf allen Servern ist. Denken Sie von nun an immer daran, erhöhte Rechte für Ihre PowerShell- und Eingabeaufforderungen festzulegen, wenn Sie die Features auf einer graphischen Serverinstallation oder auf einem Windows10-Computer ausführen.

2.  Fügen Sie Netzwerkinformationen hinzu, konfigurieren Sie den Beitritt der Knoten zur Domäne, und starten Sie die Serverknoten neu.  
    > [!NOTE]
    > Ab dieser Stelle wird in der Anleitung davon ausgegangen, dass für die Verwendung im Stretched Cluster zwei Serverpaare zur Verfügung stehen. Die Server sind durch ein WAN oder ein LAN getrennt, und sie gehören zu physischen oder logischen Standorten. In der Anleitung wird davon ausgegangen, dass **SR-SRV01** und **SR-SRV02** zum Standort „Redmond“ gehören und dass **SR-SRV03** und **SR-SRV04** zum Standort **Bellevue** gehören.  

3.  Verbinden Sie die erste Gruppe aus freigegebenem JBOD-Speicherserver, freigegebener VHDX, iSCSI-Ziel oder FC-SAN mit den Servern am Standort **Redmond**.  

4.  Verbinden Sie die zweite Speichergruppe mit dem Server am Standort **Bellevue**.  

5.  Installieren Sie gegebenenfalls aktuelle Speicher- und Speicherserverfirmware, HBA-Treiber, BIOS/UEFI-Firmware, Netzwerktreiber und Hauptplatinenchipsatz-Treiber der jeweiligen Hersteller auf allen vier Knoten. Starten Sie die Knoten gegebenenfalls neu.  

    > [!NOTE]
    > Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.  

6.  Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z. B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die Energieverwaltung in Windows Server auf eine hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus.  

7.  Konfigurieren Sie folgende Rollen:  

    -   **Grafische Methode**  

        Führen Sie **ServerManager.exe** aus, und fügen Sie alle Serverknoten hinzu, indem Sie auf **Verwaltung** und dann auf **Server hinzufügen** klicken.  

        > [!IMPORTANT]
        > Installieren Sie die Rollen und Features **Failoverclustering** und **Speicherreplikat** auf allen Knoten, und starten Sie die Knoten neu. Wenn Sie später weitere Rollen wie z.B. Hyper-V, Dateiserver usw. verwenden möchten, können Sie diese ebenfalls jetzt installieren.  

    -   **Verwenden der Windows PowerShell-Methode**  

        Führen Sie auf **SR-SRV04** oder einem Remoteverwaltungscomputer den folgenden Befehl in einer Windows PowerShell-Konsole aus, um die erforderlichen Features und Rollen für einen Stretched Cluster auf den vier Knoten zu installieren und sie neu zu starten:  

        ```PowerShell  
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | foreach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  

        ```  

        Weitere Informationen zu diesen Schritten finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md).  


8. Konfigurieren Sie den Speicher wie folgt:  

    > [!IMPORTANT]  
    > -   In jedem Speicherserver müssen zwei Volumes erstellt werden: ein Volume für Daten und ein Volume für Protokolle.  
    > -   Die Datenträger für Protokolle und Daten müssen als GPT (nicht MBR) initialisiert werden.  
    > -   Die beiden Datenvolumes müssen dieselbe Größe aufweisen.  
    > -   Die beiden Protokollvolumes sollten dieselbe Größe aufweisen.  
    > -   Alle Datenträger für replizierte Daten müssen dieselben Sektorgrößen aufweisen.  
    > -   Alle Datenträger für Protokolle müssen dieselben Sektorgrößen aufweisen.  
    > -   Für die Protokollvolumes sollte Flash-basierter Speicher mit Resilienzeinstellungen für besonders hohe Leistung verwendet werden. Microsoft empfiehlt, dass die Protokollspeicherung schneller als die Datenspeicherung durchgeführt wird. Protokollvolumes dürfen niemals für andere Workloads verwendet werden. 
    > -   Die Datenträger für Daten können HDD, SSD oder eine mehrstufige Kombination verwenden. Außerdem kann gespiegelter Speicherplatz oder Paritätsspeicherplatz bzw. RAID 1, RAID 10, RAID 5 oder RAID 50 verwendet werden.  
    > -  Das Protokollvolume muss standardmäßig eine Größe von mindestens 9 GB aufweisen und kann basierend auf Protokollanforderungen möglicherweise größer oder kleiner sein.  
    > - Die Volumes müssen mit NTFS oder ReFS formatiert sein.
    > - Die Rolle „Dateiserver“ ist nur für Test-SRTopology erforderlich, um die erforderlichen Firewallports für die Tests zu öffnen.  

    -   **Für JBOD-Gehäuse:**  

        1.  Stellen Sie sicher, dass jede Gruppe von Serverpaaren nur die Speicherserver des jeweiligen Standorts erkennen kann (d.h. asymmetrischer Speicher) und dass die SAS-Verbindungen ordnungsgemäß konfiguriert sind.  

        2.  Stellen Sie den Speicher mithilfe von Speicherplätzen bereit. Führen Sie dazu die unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](../storage-spaces/deploy-standalone-storage-spaces.md) beschriebenen **Schritte 1-3** mithilfe von Windows PowerShell oder über den Server-Manager aus.  

    -   **Für iSCSI-Speicher:**  

        1.  Stellen Sie sicher, dass jede Gruppe von Serverpaaren nur die Speicherserver des jeweiligen Standorts erkennen kann (d.h. asymmetrischer Speicher). Bei Verwendung von iSCSI sollten mehrere Netzwerkkarten verwendet werden.  

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen. Bei Verwendung von Windows-basierten iSCSI-Zielen finden Sie unter [iSCSI-Zielblockspeicher: So wird's gemacht](../iscsi/iscsi-target-server.md) weitere Informationen.  

    -   **Für den FC-SAN-Speicher:**  

        1.  Stellen Sie sicher, dass jede Gruppe von Serverpaaren nur die Speicherserver des jeweiligen Standorts erkennen kann (d. h. asymmetrischer Speicher) und dass die Zonenkonfiguration für die Hosts korrekt ist.  

        2.  Befolgen Sie die Anweisungen in der Dokumentation des jeweiligen Herstellers, um den Speicher bereitzustellen.  

## <a name="configure-a-hyper-v-failover-cluster-or-a-file-server-for-a-general-use-cluster"></a>Konfigurieren eines Hyper-V-Failoverclusters oder eines Dateiservers für einen zur allgemeinen Verwendung bestimmten Cluster

Nach dem Einrichten der Serverknoten erstellen Sie im nächsten Schritt einen der folgenden Clustertypen:  
*  [Hyper-V-Failovercluster](#BKMK_HyperV)  
*  [Datei Server für den allgemeinen Anwendungs Cluster](#BKMK_FileServer)  

### <a name="BKMK_HyperV"></a>Konfigurieren eines Hyper-V-Failoverclusters  

>[!NOTE]
> Überspringen Sie diesen Abschnitt und wechseln Sie zum Abschnitt [Konfigurieren eines Dateiservers für einen zur allgemeinen Verwendung bestimmten Cluster](#BKMK_FileServer), wenn Sie statt eines Hyper-V-Clusters einen Dateiservercluster erstellen möchten.  

Im Folgenden erstellen Sie einen normalen Failovercluster. Nach der Konfiguration, der Überprüfung und dem Testen „strecken“ Sie ihn mithilfe des Speicherreplikatfeatures, d.h. Sie erstellen daraus einen Stretched Cluster. Sie können alle unten aufgeführten Schritte auf den Cluster Knoten direkt oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

#### <a name="graphical-method"></a>Grafische Methode  

1. Führen Sie **cluadmin.msc** aus.  

2. Überprüfen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können.  

   > [!NOTE]  
   > Bei der Clusterüberprüfung sind Fehler zu erwarten, weil asymmetrischer Speicher verwendet wird.  

3. Erstellen Sie den Hyper-V-Computecluster. Stellen Sie sicher, dass der Clustername maximal 15 Zeichen lang ist. Im folgenden Beispiel wird der Name „SR-SRVCLUS“ verwendet. Wenn sich die Knoten in verschiedenen Subnetzen befinden, müssen Sie für jedes Subnetz eine IP-Adresse für den Cluster Namen erstellen und die Abhängigkeit "or" verwenden.  Weitere Informationen finden Sie unter [Konfigurieren von IP-Adressen und Abhängigkeiten für multisubnetzcluster – Teil III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698).  

4. Konfigurieren Sie einen Dateifreigabezeugen oder einen Cloudzeugen, um ein Quorum für den Fall eines Standortausfalls bereitzustellen.  

   > [!NOTE]  
   > Windows Server umfasst nun eine Option für einen Cloud-basierten Zeugen (Azure). Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.  

   > [!WARNING]  
   > Weitere Informationen zur Quorumkonfiguration finden Sie unter [Konfigurieren und Verwalten des Quorums in einem Windows Server2012-Failovercluster in der Anleitung zur Zeugenkonfiguration](https://technet.microsoft.com/library/jj612870.aspx). Weitere Informationen zum Cmdlet `Set-ClusterQuorum` finden Sie unter [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

5. Lesen Sie die [Netzwerkempfehlungen für einen Hyper-V-Cluster in Windows Server 2012](https://technet.microsoft.com/library/dn550728.aspx) und stellen Sie sicher, dass das Clusternetzwerk optimal konfiguriert ist.  

6. Fügen Sie am Standort Redmond den freigegebenen Clustervolumes des Clusters einen Datenträger hinzu. Zu diesem Zweck klicken Sie im Bereich **Speicher** mit der rechten Maustaste auf den Knoten **Datenträger** und klicken dann auf **Zu freigegebenen Clustervolumes hinzufügen**.  

7. Führen Sie in der Anleitung [Bereitstellen eines Hyper-V-Clusters](https://technet.microsoft.com/library/jj863389.aspx) die Schritte 7–10 am Standort **Redmond** aus, um einen virtuellen Testcomputer zu erstellen. Mit diesem überprüfen Sie nur, ob der Cluster mit den zwei Knoten und dem gemeinsam genutzten (bzw. freigegebenen) Speicher am ersten Teststandort ordnungsgemäß funktioniert.  

8. Wenn Sie einen Stretched Cluster mit zwei Knoten erstellen, müssen Sie den gesamten Speicher hinzufügen, bevor Sie fortfahren. Zu diesem Zweck öffnen Sie auf dem Clusterknoten eine PowerShell-Sitzung mit Administratorrechten, und führen Sie den folgenden Befehl aus: `Get-ClusterAvailableDisk -All | Add-ClusterDisk`.

   Dies ist beabsichtigtes Verhalten in Windows Server 2016.

9. Starten Sie Windows PowerShell, und überprüfen Sie mithilfe des Cmdlets `Test-SRTopology`, ob alle Anforderungen für das Speicherreplikatfeature erfüllt sind.  

    Um z. B. zwei Knoten eines geplanten Stretched Clusters zu überprüfen, die jeweils über ein Volume **D:** und **E:** verfügen, führen Sie den folgenden 30-minütigen Test aus:
   1. Verschieben Sie den gesamten verfügbaren Speicher zu **SR-SRV01**.
   2. Klicken Sie im Failovercluster-Manager im Abschnitt **Rollen** auf **Leere Rolle erstellen**.
   3. Fügen Sie der leeren Rolle mit dem Namen **Neue Rolle** den Onlinespeicher hinzu.
   4. Verschieben Sie den gesamten verfügbaren Speicher zu **SR-SRV03**.
   5. Klicken Sie im Failovercluster-Manager im Abschnitt **Rollen** auf **Leere Rolle erstellen**.
   6. Verschieben Sie **Neue Rolle (2)** im leeren Zustand zu **SR-SRV03**.
   7. Fügen Sie der leeren Rolle mit dem Namen **Neue Rolle (2)** den Onlinespeicher hinzu.
   8. Nachdem Sie nun den gesamten Speicher mit Laufwerksbuchstaben eingebunden haben, können Sie den Cluster mit `Test-SRTopology` überprüfen.

       Zum Beispiel:

           MD c:\temp  

           Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName D: -SourceLogVolumeName E: -DestinationComputerName SR-SRV03 -DestinationVolumeName D: -DestinationLogVolumeName E: -DurationInMinutes 30 -ResultPath c:\temp        

      > [!IMPORTANT]
      > Bei Verwendung eines Testservers ohne Schreib-E/A-Last auf dem angegebenen Quellvolume während des Auswertungszeitraums sollten Sie am besten eine Workload hinzufügen. Andernfalls generiert Test-SRTopology keinen nützlichen Bericht. Um reale Zahlen und empfohlene Protokollgrößen zu erhalten, sollte der Test mit produktionsähnlichen Workloads ausgeführt werden. Alternativ können Sie ganz einfach während des Tests Dateien auf das Quellvolume kopieren oder DISKSPD herunterladen und ausführen, um Schreib-E/A zu generieren. Beispiel mit geringer E/A-Workload innerhalb eines Zeitraums von 5 Minuten auf dem Volume D:   
       `Diskspd.exe -c1g -d600 -W5 -C5 -b4k -t2 -o2 -r -w5 -i100 d:\test.dat`  

10. Vergewissern Sie sich anhand des Berichts **TestSrTopologyReport-< Datum >.html**, dass die Anforderungen für das Speicherreplikatfeature erfüllt sind, und beachten Sie die Prognosen für die Erstsynchronisierungszeit sowie die Protokollempfehlungen.  

      ![Bildschirm mit dem Replikationsbericht](./media/Stretch-Cluster-Replication-Using-Shared-Storage/SRTestSRTopologyReport.png)

11. Führen Sie die Datenträger wieder zum verfügbaren Speicher zurück, und entfernen Sie die temporären leeren Rollen.

12. Wenn Sie mit der Überprüfung zufrieden sind, entfernen Sie den virtuellen Testcomputer wieder. Fügen Sie einem geplanten Quellknoten beliebige echte virtuelle Testcomputer hinzu, um gegebenenfalls weitere Überprüfungen durchzuführen.  

13. Konfigurieren Sie die Standortinformationen für den Stretched Cluster so, dass sich die Server **SR-SRV01** und **SR-SRV02** am Standort **Redmond** befinden, die Server **SR-SRV03** und **SR-SRV04** dem Standort **Bellevue** zugeordnet sind und **Redmond** als bevorzugter Standort für den Knotenbesitz des Quellspeichers und der virtuellen Computer festgelegt ist:  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  
   
    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  
   
    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"
    ```

    > [!NOTE]
    > Im Failovercluster-Manager von Windows Server 2016 ist keine Option zum Konfigurieren von Standortinformationen vorhanden.  

14. **(Optional)** Konfigurieren Sie das Clusternetzwerk und Active Directory, um ein schnelleres DNS-Standortfailover zu ermöglichen. Sie können Software-Defined Networking mit Hyper-V, Stretched VLANs, Netzwerkabstraktionsgeräte, verringerte DNS-TTL und andere übliche Techniken verwenden.

    Weitere Informationen finden Sie in der Microsoft Ignite-Sitzung: [Erweitern von Failoverclustern und Verwenden des Speicher Replikats in Windows Server vNext](http://channel9.msdn.com/Events/Ignite/2015/BRK3487) und dem Blogbeitrag [Aktivieren von Änderungs Benachrichtigungen Zwischenstand Orten-wie und warum?](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)  

15. **(Optional)** Konfigurieren Sie die VM-Resilienz so, dass Gäste bei Knotenausfällen nicht für längere Zeit angehalten werden. Anstelle dessen soll innerhalb von 10Sekunden ein Failover auf den neuen Quellspeicher für die Replikation ausgeführt werden.  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]
    >  Im Failovercluster-Manager von Windows Server 2016 ist keine Option zum Konfigurieren von VM-Resilienz vorhanden.  

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  

1. Testen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können:  

   ```PowerShell  
   Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04  
   ```  

   > [!NOTE]
   >  Bei der Clusterüberprüfung sind Fehler zu erwarten, weil asymmetrischer Speicher verwendet wird.  

2. Erstellen Sie den Datei Server für die allgemeine Verwendung eines Speicher Clusters (Sie müssen eine eigene statische IP-Adresse angeben, die vom Cluster verwendet wird). Stellen Sie sicher, dass der Clustername maximal 15 Zeichen lang ist.  Wenn sich die Knoten in unterschiedlichen Subnetzen befinden, muss mithilfe der Abhängigkeit "oder" eine IP-Adresse für den zusätzlichen Standort erstellt werden. Weitere Informationen finden Sie unter [Konfigurieren von IP-Adressen und Abhängigkeiten für multisubnetzcluster – Teil III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698).
   ```PowerShell  
   New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here>  
   Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”
   Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
   ```  

3. Konfigurieren Sie im Cluster einen Dateifreigabezeugen oder einen Cloudzeugen (Azure-Zeugen), der auf eine Freigabe verweist, die auf dem Domänencontroller oder auf einem anderen unabhängigen Server gehostet ist. Zum Beispiel:  

   ```PowerShell  
   Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
   ```  

   > [!NOTE]
   > Windows Server umfasst nun eine Option für einen Cloud-basierten Zeugen (Azure). Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.  
    
   Weitere Informationen zur Quorumkonfiguration finden Sie unter [Konfigurieren und Verwalten des Quorums in einem Windows Server2012-Failovercluster in der Anleitung zur Zeugenkonfiguration](https://technet.microsoft.com/library/jj612870.aspx). Weitere Informationen zum Cmdlet `Set-ClusterQuorum` finden Sie unter [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

4. Lesen Sie die [Netzwerkempfehlungen für einen Hyper-V-Cluster in Windows Server 2012](https://technet.microsoft.com/library/dn550728.aspx) und stellen Sie sicher, dass das Clusternetzwerk optimal konfiguriert ist.  

5. Wenn Sie einen Stretched Cluster mit zwei Knoten erstellen, müssen Sie den gesamten Speicher hinzufügen, bevor Sie fortfahren. Zu diesem Zweck öffnen Sie auf dem Clusterknoten eine PowerShell-Sitzung mit Administratorrechten, und führen Sie den folgenden Befehl aus: `Get-ClusterAvailableDisk -All | Add-ClusterDisk`.

   Dies ist beabsichtigtes Verhalten in Windows Server 2016.

6. Führen Sie in der Anleitung [Bereitstellen eines Hyper-V-Clusters](https://technet.microsoft.com/library/jj863389.aspx) die Schritte 7–10 am Standort **Redmond** aus, um einen virtuellen Testcomputer zu erstellen. Mit diesem überprüfen Sie nur, ob der Cluster mit den zwei Knoten und dem gemeinsam genutzten (bzw. freigegebenen) Speicher am ersten Teststandort ordnungsgemäß funktioniert.  

7. Wenn Sie mit der Überprüfung zufrieden sind, entfernen Sie den virtuellen Testcomputer wieder. Fügen Sie einem geplanten Quellknoten beliebige echte virtuelle Testcomputer hinzu, um gegebenenfalls weitere Überprüfungen durchzuführen.  

8. Konfigurieren Sie die Standortinformationen für den Stretched Cluster so, dass sich die Server **SR-SRV01** und **SR-SRV02** am Standort **Redmond** befinden, die Server **SR-SRV03** und **SR-SRV04** dem Standort **Bellevue** zugeordnet sind und **Redmond** als bevorzugter Standort für den Knotenbesitz des Quellspeichers und der virtuellen Computer festgelegt ist:  

   ```PowerShell  
   New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

   New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

   Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
   Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
   Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

   (Get-Cluster).PreferredSite="Seattle"  
   ```  

9. **(Optional)** Konfigurieren Sie das Clusternetzwerk und Active Directory, um ein schnelleres DNS-Standortfailover zu ermöglichen. Sie können Software-Defined Networking mit Hyper-V, Stretched VLANs, Netzwerkabstraktionsgeräte, verringerte DNS-TTL und andere übliche Techniken verwenden.  

   Weitere Informationen finden Sie in der Microsoft Ignite-Sitzung: [Stretching von Failoverclustern und Verwenden des Speicher Replikats in Windows Server vNext](http://channel9.msdn.com/Events/Ignite/2015/BRK3487) und [Aktivieren von Änderungs Benachrichtigungen Zwischenstand Orten: wie und warum](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx).  

10. **(Optional)** Konfigurieren Sie die VM-Resilienz so, dass Gäste bei Knotenausfällen nicht für einen längeren Zeitraum angehalten werden. Anstelle dessen soll innerhalb von 10Sekunden ein Failover auf den neuen Quellspeicher für die Replikation ausgeführt werden.  

    ```PowerShell  
    (Get-Cluster).ResiliencyDefaultPeriod=10  
    ```  

    > [!NOTE]  
    > Im Failovercluster-Manager von Windows Server 2016 ist keine Option für VM-Resilienz vorhanden.  



### <a name="BKMK_FileServer"></a>Konfigurieren eines Dateiservers für den allgemeinen Anwendungs Cluster  

>[!NOTE]
> Überspringen Sie diesen Abschnitt, wenn Sie bereits einen Hyper-V-Failovercluster gemäß der Beschreibung unter [Konfigurieren eines Hyper-V-Failoverclusters](#BKMK_HyperV) konfiguriert haben.  

Im Folgenden erstellen Sie einen normalen Failovercluster. Nach der Konfiguration, der Überprüfung und dem Testen „strecken“ Sie ihn mithilfe des Speicherreplikatfeatures, d.h. Sie erstellen daraus einen Stretched Cluster. Sie können alle unten aufgeführten Schritte auf den Cluster Knoten direkt oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

#### <a name="graphical-method"></a>Grafische Methode  

1. Führen Sie „cluadmin.msc“ aus.  

2. Überprüfen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können.  
   >[!NOTE]
   >Bei der Clusterüberprüfung sind Fehler zu erwarten, weil asymmetrischer Speicher verwendet wird.   
3. Erstellen Sie den Dateiserver für einen zur allgemeinen Verwendung bestimmten Speichercluster. Stellen Sie sicher, dass der Clustername maximal 15 Zeichen lang ist. Im folgenden Beispiel wird der Name „SR-SRVCLUS“ verwendet.  Wenn sich die Knoten in verschiedenen Subnetzen befinden, müssen Sie für jedes Subnetz eine IP-Adresse für den Cluster Namen erstellen und die Abhängigkeit "or" verwenden.  Weitere Informationen finden Sie unter [Konfigurieren von IP-Adressen und Abhängigkeiten für multisubnetzcluster – Teil III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698).  

4. Konfigurieren Sie einen Dateifreigabezeugen oder einen Cloudzeugen, um ein Quorum für den Fall eines Standortausfalls bereitzustellen.  
   >[!NOTE]
   > Windows Server umfasst nun eine Option für einen Cloud-basierten Zeugen (Azure). Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.                                                                                                                                                                             
   >[!NOTE]
   >  Weitere Informationen zur Quorumkonfiguration finden Sie unter [Konfigurieren und Verwalten des Quorums in einem Windows Server2012-Failovercluster in der Anleitung zur Zeugenkonfiguration](https://technet.microsoft.com/library/jj612870.aspx). Weitere Informationen zum Cmdlet „Set-ClusterQuorum“ finden Sie unter [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum). 

5. Wenn Sie einen Stretched Cluster mit zwei Knoten erstellen, müssen Sie den gesamten Speicher hinzufügen, bevor Sie fortfahren. Zu diesem Zweck öffnen Sie auf dem Clusterknoten eine PowerShell-Sitzung mit Administratorrechten, und führen Sie den folgenden Befehl aus: `Get-ClusterAvailableDisk -All | Add-ClusterDisk`.

   Dies ist beabsichtigtes Verhalten in Windows Server 2016.

6. Stellen Sie sicher, dass das Clusternetzwerk optimal konfiguriert ist.  
    >[!NOTE]
    > Die Rolle „Dateiserver“ muss auf allen Knoten installiert werden, bevor Sie mit dem nächsten Schritt fortfahren.   |  

7. Klicken Sie unter **Rollen** auf **Rolle konfigurieren**. Lesen Sie die **Vorbemerkungen**, und klicken Sie auf **Weiter**.  

8. Wählen Sie **Dateiserver** aus, und klicken Sie auf **Weiter**.  

9. Lassen Sie **Dateiserver zur allgemeinen Verwendung** ausgewählt, und klicken Sie auf **Weiter**.  

10. Geben Sie einen Namen für den **Clientzugriffspunkt** ein (maximal 15 Zeichen), und klicken Sie auf **Weiter**.  

11. Wählen Sie einen Datenträger aus, der als Datenvolume verwendet werden soll, und klicken Sie auf **Weiter**.  

12. Überprüfen Sie Ihre Einstellungen, und klicken Sie auf **Weiter**. Klicken Sie auf **Fertig stellen**.  

13. Klicken Sie mit der rechten Maustaste auf die neue Dateiserverrolle, und klicken Sie auf **Dateifreigabe hinzufügen**. Führen Sie im Assistenten die Schritte zum Konfigurieren von Freigaben aus.  

14. Optional: Fügen Sie eine weitere Datei Server Rolle hinzu, die den anderen Speicher an diesem Standort verwendet.  

15. Konfigurieren Sie die Standortinformationen für den Stretched Cluster so, dass sich die Server SR-SRV01 und SR-SRV02 am Standort Redmond befinden, die Server SR-SRV03 und SR-SRV04 dem Standort Bellevue zugeordnet sind und Redmond als bevorzugter Standort für den Knotenbesitz des Quellspeichers und der virtuellen Computer festgelegt ist:  

    ```PowerShell  
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```  

      >[!NOTE]
      > Im Failovercluster-Manager von Windows Server 2016 ist keine Option zum Konfigurieren von Standortinformationen vorhanden.  

16. (Optional) Konfigurieren Sie das Clusternetzwerk und Active Directory, um ein schnelleres DNS-Standortfailover zu ermöglichen. Sie können Stretched VLANs, Netzwerkabstraktionsgeräte, verringerte DNS-TTL und andere übliche Techniken verwenden.  

Weitere Informationen finden Sie in der Microsoft Ignite-Sitzung: [Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](http://channel9.msdn.com/events/ignite/2015/brk3487) und dem Blogbeitrag [Enable Change Notifications between Sites - How and Why?](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)    

#### <a name="powershell-method"></a>PowerShell-Methode

1. Testen Sie den geplanten Cluster, und analysieren Sie die Ergebnisse, um sicherzustellen, dass Sie den Vorgang fortsetzen können:    

    ```PowerShell
    Test-Cluster SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04
    ```

    > [!NOTE]
    >  Bei der Clusterüberprüfung sind Fehler zu erwarten, weil asymmetrischer Speicher verwendet wird.   

2.  Erstellen Sie den Hyper-V-Computecluster (Sie müssen die eigene statische IP-Adresse angeben, die der Cluster verwenden soll). Stellen Sie sicher, dass der Clustername maximal 15 Zeichen lang ist.  Wenn sich die Knoten in unterschiedlichen Subnetzen befinden, muss mithilfe der Abhängigkeit "oder" eine IP-Adresse für den zusätzlichen Standort erstellt werden. Weitere Informationen finden Sie unter [Konfigurieren von IP-Adressen und Abhängigkeiten für multisubnetzcluster – Teil III](https://techcommunity.microsoft.com/t5/Failover-Clustering/Configuring-IP-Addresses-and-Dependencies-for-Multi-Subnet/ba-p/371698).  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUS -Node SR-SRV01, SR-SRV02, SR-SRV03, SR-SRV04 -StaticAddress <your IP here> 

    Add-ClusterResource -Name NewIPAddress -ResourceType “IP Address” -Group “Cluster Group”

    Set-ClusterResourceDependency -Resource “Cluster Name” -Dependency “[Cluster IP Address] or [NewIPAddress]”
    ```


3. Konfigurieren Sie im Cluster einen Dateifreigabezeugen oder einen Cloudzeugen (Azure-Zeugen), der auf eine Freigabe verweist, die auf dem Domänencontroller oder auf einem anderen unabhängigen Server gehostet ist. Zum Beispiel:  

    ```PowerShell
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare
    ```

    >[!NOTE]
    > Windows Server enthält jetzt eine Option für den cloudzeugen, der Azure verwendet. Sie können diese Quorumoption anstelle des Dateifreigabezeugen auswählen.  

   Weitere Informationen zur Quorum Konfiguration finden Sie Untergrund Legendes zu [Cluster-und Pool Quorums](../storage-spaces/understand-quorum.md). Weitere Informationen zum Cmdlet „Set-ClusterQuorum“ finden Sie unter [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).

4.  Wenn Sie einen Stretched Cluster mit zwei Knoten erstellen, müssen Sie den gesamten Speicher hinzufügen, bevor Sie fortfahren. Zu diesem Zweck öffnen Sie auf dem Clusterknoten eine PowerShell-Sitzung mit Administratorrechten, und führen Sie den folgenden Befehl aus: `Get-ClusterAvailableDisk -All | Add-ClusterDisk`.

    Dies ist beabsichtigtes Verhalten in Windows Server 2016.

5. Stellen Sie sicher, dass das Clusternetzwerk optimal konfiguriert ist.  

6.  Konfigurieren Sie eine Dateiserverrolle. Zum Beispiel:

    ```PowerShell  
    Get-ClusterResource  
    Add-ClusterFileServerRole -Name SR-CLU-FS2 -Storage "Cluster Disk 4"  

    MD e:\share01  

    New-SmbShare -Name Share01 -Path f:\share01 -ContinuouslyAvailable $false  
    ```

7. Konfigurieren Sie die Standortinformationen für den Stretched Cluster so, dass sich die Server SR-SRV01 und SR-SRV02 am Standort Redmond befinden, die Server SR-SRV03 und SR-SRV04 dem Standort Bellevue zugeordnet sind und Redmond als bevorzugter Standort für den Knotenbesitz des Quellspeichers und der virtuellen Computer festgelegt ist:  

    ```PowerShell
    New-ClusterFaultDomain -Name Seattle -Type Site -Description "Primary" -Location "Seattle Datacenter"  

    New-ClusterFaultDomain -Name Bellevue -Type Site -Description "Secondary" -Location "Bellevue Datacenter"  

    Set-ClusterFaultDomain -Name sr-srv01 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv02 -Parent Seattle  
    Set-ClusterFaultDomain -Name sr-srv03 -Parent Bellevue  
    Set-ClusterFaultDomain -Name sr-srv04 -Parent Bellevue  

    (Get-Cluster).PreferredSite="Seattle"  
    ```

8.  (Optional) Konfigurieren Sie das Clusternetzwerk und Active Directory, um ein schnelleres DNS-Standortfailover zu ermöglichen. Sie können Stretched VLANs, Netzwerkabstraktionsgeräte, verringerte DNS-TTL und andere übliche Techniken verwenden.  
    
    Weitere Informationen finden Sie in der Microsoft Ignite-Sitzung: [Stretching Failover Clusters and Using Storage Replica in Windows Server vNext](http://channel9.msdn.com/events/ignite/2015/brk3487) und dem Blogbeitrag [Enable Change Notifications between Sites - How and Why?](http://blogs.technet.com/b/qzaidi/archive/2010/09/23/enable-change-notifications-between-sites-how-and-why.aspx)

### <a name="configure-a-stretch-cluster"></a>Konfigurieren eines Stretched Clusters  
Nun konfigurieren Sie den Stretched Cluster. Dazu verwenden Sie entweder den Failovercluster-Manager oder Windows PowerShell. Sie können alle unten aufgeführten Schritte auf den Cluster Knoten direkt oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

#### <a name="failover-cluster-manager-method"></a>Methode mit dem Failovercluster-Manager  

1.  Bei Hyper-V-Workloads fügen Sie auf dem Knoten, auf dem sich die nach außen zu replizierenden Daten befinden, den Quelldatenträger aus Ihren verfügbaren Datenträgern zu den freigegebenen Clustervolumes hinzu (sofern diese Konfiguration noch nicht vorgenommen wurde). Fügen Sie nicht alle Datenträger, sondern nur einen einzelnen Datenträger hinzu. Zu diesem Zeitpunkt wird die Hälfte der Datenträger als „offline“ angezeigt, weil es sich hier um asymmetrischen Speicher handelt.  
Wenn Workloads für physische Datenträgerressourcen repliziert werden sollen, z.B. ein Dateiserver zur allgemeinen Verwendung, verfügen Sie bereits über einen Datenträger mit Rollenzuweisung, der sofort einsatzbereit ist.  

    ![Bildschirm mit dem Failovercluster-Manager](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_OnlineDisks2.png)  

2.  Klicken Sie mit der rechten Maustaste auf den Datenträger im freigegebenen Clustervolume oder auf den Datenträger mit Rollenzuweisung, und klicken Sie auf **Replikation** und dann auf **Aktivieren**.  

3.  Wählen Sie ein geeignetes Zieldatenvolume aus, und klicken Sie auf **Weiter**. Die angezeigten Zieldatenträger verfügen über ein Volume mit der gleichen Größe wie der ausgewählte Quelldatenträger. Während Sie in diesem Assistenten von Dialogfeld zu Dialogfeld wechseln, wird der verfügbare Speicher nach Bedarf im Hintergrund automatisch verschoben und online geschaltet.  

    ![Bildschirm mit der Seite „Zieldatenträger auswählen“ des Assistenten zum Konfigurieren von Speicherreplikaten](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_SelectDestinationDataDisk2.png)  

4.  Wählen Sie den entsprechenden Datenträger für das Quellprotokoll aus, und klicken Sie auf **Weiter**. Das Quellprotokollvolume sollte sich auf einem Datenträger befinden, der SSD oder ähnlich schnelle Medien nutzt, und nicht auf einer rotierenden Festplatte.  

5.  Wählen Sie ein geeignetes Zielprotokollvolume aus, und klicken Sie auf „Weiter“. Die angezeigten Zielprotokoll-Datenträger verfügen über ein Volume mit der gleichen Größe wie das ausgewählte Quellprotokoll-Datenträgervolume.  

6.  Behalten Sie für **Volume überschreiben** den Wert **Zielvolume überschreiben** bei, wenn das Zielvolume keine vorherige Kopie der Daten aus dem Quellserver enthält. Wenn das Ziel bereits ähnliche Daten aus einer neueren Datensicherung oder einer vorherigen Replikation enthält, wählen Sie **Seeding-Zieldatenträger** aus. Klicken Sie dann auf **Weiter**.  

7.  Behalten Sie für **Replikationsmodus** den Wert **Synchrone Replikation** bei, wenn Sie eine Replikation mit einem Wiederherstellungspunktziel (RPO, Recovery Point Objective) von null verwenden möchten. Ändern Sie den Wert in **Asynchrone Replikation**, wenn Sie einen Stretched Cluster einrichten möchten, der sich über Netzwerke mit höherer Latenz erstreckt, oder wenn Sie eine niedrigere E/A-Latenz auf den Knoten des primären Standorts benötigen.  
8.  Behalten Sie für **Konsistenzgruppe** den Wert **Höchste Leistung** bei, wenn Sie später bei zusätzlichen Datenträgerpaaren in der Replikationsgruppe keine Schreibreihenfolge verwenden möchten. Wenn Sie der Replikationsgruppe weitere Datenträger hinzufügen möchten und eine garantierte Schreibreihenfolge erforderlich ist, wählen Sie **Schreibreihenfolge aktivieren** aus. Klicken Sie dann auf **Weiter**.  

9.  Klicken Sie auf **Weiter**, um die Replikation und den Aufbau des Stretched Clusters zu konfigurieren.  

    ![Bildschirm mit der Seite „Bestätigung auswählen“ des Assistenten zum Konfigurieren von Speicherreplikaten](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ConfigureSR2.png)  

10. Beachten Sie auf der Seite „Zusammenfassung“ die Ergebnisse des Abschlussdialogfelds. Sie können diesen Bericht in einem Webbrowser anzeigen.  

11. Jetzt haben Sie eine Speicherreplikatpartnerschaft zwischen den beiden Hälften des Clusters konfiguriert, die Replikation selbst dauert jedoch noch an. Es gibt verschiedene Möglichkeiten, wie Sie den Status der Replikation in einem grafischen Tool anzeigen können.  

    1.  Verwenden Sie die Spalte **Replikationsrolle** und die Registerkarte **Replikation**. Nach dem Abschluss der Erstsynchronisierung haben die Quell- und Zieldatenträger den Replikationsstatus **Kontinuierliche Replikation**.   

        ![Bildschirm mit der Registerkarte „Replikation“ eines Datenträgers im Failovercluster-Manager](./media/Stretch-Cluster-Replication-Using-Shared-Storage/Storage_SR_ReplicationDetails2.png)  

    2.  Starten Sie **eventvwr.exe**.  

        1.  Navigieren Sie auf dem Quellserver zu **Anwendungen und Dienste \ Microsoft \ Windows \ StorageReplica \ Admin**, und überprüfen Sie die Ereignisse 5015, 5002, 5004, 1237, 5001 und 2200.  

        2.  Navigieren Sie auf dem Zielserver zu **Anwendungen und Dienste \ Microsoft \ Windows \ StorageReplica \ Betriebsbereit**, und warten Sie auf Ereignis 1215. Dieses Ereignis gibt die Anzahl der kopierten Bytes sowie die dafür benötigte Zeit an. Beispiel:  

            ```  
            Log Name:      Microsoft-Windows-StorageReplica/Operational  
            Source:        Microsoft-Windows-StorageReplica  
            Date:          4/6/2016 4:52:23 PM  
            Event ID:      1215  
            Task Category: (1)  
            Level:         Information  
            Keywords:      (1)  
            User:          SYSTEM  
            Computer:      SR-SRV03.Threshold.nttest.microsoft.com  
            Description:  
            Block copy completed for replica.  

            ReplicationGroupName: Replication 2  
            ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
            ReplicaName: \\?\Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}\  
            ReplicaId: {00000000-0000-0000-0000-000000000000}  
            End LSN in bitmap:   
            LogGeneration: {00000000-0000-0000-0000-000000000000}  
            LogFileId: 0  
            CLSFLsn: 0xFFFFFFFF  
            Number of Bytes Recovered: 68583161856  
            Elapsed Time (ms): 140  
            ```  

        3.  Navigieren Sie auf dem Zielserver zu **Anwendungen und Dienste \ Microsoft \ Windows \ StorageReplica \ Admin**, und überprüfen Sie die Ereignisse 5009, 1237, 5001, 5015, 5005 und 2200, um Informationen zum Verarbeitungsfortschritt zu erhalten. Diese Abfolge sollte keine Warnungen oder Fehler enthalten. Es werden eine Vielzahl von Ereignissen des Typs 1237 angezeigt, die für den Fortschritt stehen.  

            > [!WARNING]
            > Die CPU- und Speicherauslastung sind bis zum Abschluss der Erstsynchronisierung in der Regel höher als üblich.  

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  

1.  Stellen Sie sicher, dass Ihre PowerShell-Konsole mit einem Administratorkonto mit erhöhten Rechten ausgeführt wird.  
2.  Fügen Sie nur den Quelldatenspeicher als freigegebenes Clustervolume zum Cluster hinzu. Ermitteln Sie mithilfe der folgenden Befehle die Größe, die Partition und das Volumelayout der verfügbaren Datenträger:  

    ```PowerShell  
    Move-ClusterGroup -Name "available storage" -Node sr-srv01  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  

    Move-ClusterGroup -Name "available storage" -Node sr-srv03  

    $DiskResources = Get-ClusterResource | Where-Object { $_.ResourceType -eq 'Physical Disk' -and $_.State -eq 'Online' }  
    $DiskResources | foreach {  
        $resource = $_  
        $DiskGuidValue = $resource | Get-ClusterParameter DiskIdGuid  

        Get-Disk | where { $_.Guid -eq $DiskGuidValue.Value } | Get-Partition | Get-Volume |  
            Select @{N="Name"; E={$resource.Name}}, @{N="Status"; E={$resource.State}}, DriveLetter, FileSystemLabel, Size, SizeRemaining  
    } | FT -AutoSize  
    ```  

4.  Legen Sie mit folgendem Befehl den richtigen Datenträger für das freigegebene Clustervolume (engl.„Cluster Shared Volume“) fest:  

    ```PowerShell  
    Add-ClusterSharedVolume -Name "Cluster Disk 4"  
    Get-ClusterSharedVolume  
    Move-ClusterSharedVolume -Name "Cluster Disk 4" -Node sr-srv01  
    ```  

5.  Konfigurieren Sie den Stretched Cluster, und geben Sie dabei Folgendes an:  

    -   Quell- und Zielknoten (wobei sich die Quelldaten auf einem Datenträger in einem freigegebenen Clustervolume befinden, alle anderen Datenträger aber nicht)  

    -   Die Namen der Quell- und Zielreplikationsgruppen  

    -   Die Quell- und Zieldatenträger mit übereinstimmenden Partitionsgrößen  

    -   Die Protokollvolumes für Quelle und Ziel mit genügend freiem Speicherplatz für die vorgesehene Protokollgröße auf beiden Datenträgern. Als Speicher sollte SSD oder ein ähnlich schnelles Medium verwendet werden.  

    -   Die Protokollvolumes für Quelle und Ziel mit genügend freiem Speicherplatz für die vorgesehene Protokollgröße auf beiden Datenträgern. Als Speicher sollte SSD oder ein ähnlich schnelles Medium verwendet werden.  

    -   Protokollgröße  

    -   Das Quellprotokollvolume sollte sich auf einem Datenträger befinden, der SSD oder ähnlich schnelle Medien nutzt, und nicht auf einer rotierenden Festplatte.  

    ```PowerShell  
    New-SRPartnership -SourceComputerName sr-srv01 -SourceRGName rg01 -SourceVolumeName "C:\ClusterStorage\Volume1" -SourceLogVolumeName e: -DestinationComputerName sr-srv03 -DestinationRGName rg02 -DestinationVolumeName d: -DestinationLogVolumeName e:  
    ```  

    > [!NOTE]  
    > Sie können auch an jedem Standort auf einem Knoten `New-SRGroup` und dann `New-SRPartnership` verwenden, um die Replikation nicht in einem Gesamtschritt, sondern in Einzelschritten zu erstellen.  

6.  Bestimmen Sie den Fortschritt der Replikation.  

    1.  Führen Sie auf dem Quellserver den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5015, 5002, 5004, 1237, 5001 und 2200:  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20  
        ```  

    2.  Führen Sie auf dem Zielserver den folgenden Befehl aus, um die Speicherreplikatereignisse anzuzeigen, die das Erstellen der Partnerschaft belegen. Dieses Ereignis gibt die Anzahl der kopierten Bytes sowie die dafür benötigte Zeit an. Beispiel:  

            Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | fl  

            TimeCreated  : 4/6/2016 4:52:23 PM  
            ProviderName : Microsoft-Windows-StorageReplica  
            Id           : 1215  
            Message      : Block copy completed for replica.  

               ReplicationGroupName: Replication 2  
               ReplicationGroupId: {c6683340-0eea-4abc-ab95-c7d0026bc054}  
               ReplicaName: ?Volume{43a5aa94-317f-47cb-a335-2a5d543ad536}  
               ReplicaId: {00000000-0000-0000-0000-000000000000}  
               End LSN in bitmap:   
               LogGeneration: {00000000-0000-0000-0000-000000000000}  
               LogFileId: 0  
               CLSFLsn: 0xFFFFFFFF  
               Number of Bytes Recovered: 68583161856  
               Elapsed Time (ms): 140  

    3.  Führen Sie auf dem Zielserver den folgenden Befehl aus, und überprüfen Sie die Ereignisse 5009, 1237, 5001, 5015, 5005 und 2200, um Informationen zum Verarbeitungsfortschritt zu erhalten. Diese Abfolge sollte keine Warnungen oder Fehler enthalten. Es werden eine Vielzahl von Ereignissen des Typs 1237 angezeigt, die für den Fortschritt stehen.  

        ```PowerShell  
        Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
        ```  

    4.  Alternativ gibt die Zielservergruppe für das Replikat jederzeit die Anzahl der noch zu kopierenden Bytes an. Dieser Wert kann auch über PowerShell abgefragt werden. Zum Beispiel:  

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

7.  Rufen Sie den Status der Replikationsquelle und des Replikationsziels innerhalb des Stretched Clusters mit `Get-SRGroup` ab, und zeigen Sie mithilfe von `Get-SRPartnership` den konfigurierten Status der Replikation im Stretched Cluster an.  

    ```PowerShell  
    Get-SRGroup  
    Get-SRPartnership  
    (Get-SRGroup).replicas  
    ```  

### <a name="manage-stretched-cluster-replication"></a>Verwalten der Replikation im Stretched Cluster  
Nun verwalten und betreiben Sie den Stretched Cluster. Sie können alle unten aufgeführten Schritte auf den Cluster Knoten direkt oder über einen Remote Verwaltungs Computer ausführen, der den Windows Server-Remoteserver-Verwaltungstools enthält.  

#### <a name="graphical-tools-method"></a>Methode mit grafischen Tools  

1.  Verwenden Sie den Failovercluster-Manager, um die aktuelle Quelle und das aktuelle Ziel der Replikation sowie den zugehörigen Status zu ermitteln.  

2.  Zum Ermitteln der Replikationsleistung verwenden Sie **Perfmon.exe** sowohl auf dem Quell- als auch auf dem Zielknoten.  

    1.  Vorgehensweise auf dem Zielknoten:  

        1.  Fügen Sie die Objekte der **Speicherreplikatstatistik** mit allen ihren Leistungsindikatoren für das Datenvolume hinzu.  

        2.  Überprüfen Sie die Ergebnisse.  

    2.  Vorgehensweise auf dem Quellknoten:  

        1.  Fügen Sie die Objekte der **Speicherreplikatstatistik** und der **Statistik zur Partitions-E/A des Speicherreplikats** mit allen ihren Leistungsindikatoren für das Datenvolume hinzu (die letztgenannte Statistik ist nur mit den Daten für den aktuellen Quellserver verfügbar).  

        2.  Überprüfen Sie die Ergebnisse.  

3.  Wenn Sie die Replikationsquelle und das Replikationsziel innerhalb des Stretched Clusters ändern möchten, gehen Sie wie folgt vor:  

    1.  Um die Quellreplikation zwischen Knoten am gleichen Standort zu verschieben, klicken Sie mit der rechten Maustaste auf das für die Quelle verwendete freigegebene Clustervolume und klicken auf **Speicher verschieben**. Klicken Sie anschließend auf **Knoten auswählen**, und wählen Sie einen Knoten am gleichen Standort aus. Wenn Sie für einen Datenträger mit Rollenzuweisung Speicher verwenden, der nicht auf freigegebenen Clustervolumes untergebracht ist, müssen Sie die Rolle verschieben.  

    2.  Um die Quellreplikation von einem Standort an einen anderen zu verschieben, klicken Sie mit der rechten Maustaste auf das für die Quelle verwendete freigegebene Clustervolume und klicken auf **Speicher verschieben**. Klicken Sie anschließend auf **Knoten auswählen**, und wählen Sie einen Knoten an einem anderen Standort aus. Wenn Sie einen bevorzugten Standort konfiguriert haben, können Sie den am besten geeigneten Knoten verwenden, um den Quellspeicher immer auf einen Knoten am bevorzugten Standort zu verschieben. Wenn Sie für einen Datenträger mit Rollenzuweisung Speicher verwenden, der nicht auf freigegebenen Clustervolumes untergebracht ist, müssen Sie die Rolle verschieben.  

    3.  Um ein geplantes Failover in der Replikationsrichtung von einem Standort zum anderen auszuführen, fahren Sie die beiden Knoten an einem Standort mithilfe von **ServerManager.exe** oder **SConfig** herunter.  

    4.  Um ein ungeplantes Failovers in der Replikationsrichtung von einem Standort zum anderen auszuführen, unterbrechen Sie die Stromversorgung für die beiden Knoten an einem Standort.  

        > [!NOTE]
        > In Windows Server 2016 müssen Sie unter Umständen den Failovercluster-Manager oder „Move-ClusterGroup“ verwenden, um die Zieldatenträger manuell wieder zurück zum anderen Standort zu verschieben, nachdem diese Knoten wieder online geschaltet wurden.  

        > [!NOTE]
        > Das Speicherreplikatfeature hebt die Bereitstellung der Zielvolumes auf. Dies ist beabsichtigt.  

4.  Um die Protokoll Größe von 8 GB zu ändern, klicken Sie mit der rechten Maustaste auf die Quell-und Ziel Protokoll Datenträger, klicken Sie auf die Registerkarte **Replikations Protokoll** , und ändern Sie dann die Größe der Datenträger entsprechend.  

    > [!NOTE]  
    > Die standardmäßige Protokollgröße beträgt 8GB. Abhängig von den Ergebnissen des Cmdlets `Test-SRTopology` können Sie `-LogSizeInBytes` mit einem höheren oder niedrigeren Wert verwenden.  

5.  Wenn Sie einer vorhandenen Replikationsgruppe ein weiteres Paar replizierter Datenträger hinzufügen, müssen Sie zunächst sicherstellen, dass sich im verfügbaren Speicher mindestens ein zusätzlicher Datenträger befindet. Anschließend können Sie mit der rechten Maustaste auf den Quelldatenträger klicken und **Replikationspartnerschaft hinzufügen** auswählen.  
    > [!NOTE]  
    > Die Notwendigkeit eines zusätzlichen Dummydatenträgers im verfügbaren Speicher ist Folge einer Regression und nicht beabsichtigt. Der Failovercluster-Manager hat das Hinzufügen weiterer Datenträger zuvor unterstützt, und in einer späteren Version wird das auch wieder der Fall sein.  


6.  So entfernen Sie die vorhandene Replikation:  

    1.  Führen Sie **cluadmin.msc** aus.  

    2.  Klicken Sie mit der rechten Maustaste auf den für die Quelle verwendeten Datenträger im freigegebenen Clustervolume, klicken Sie auf **Replikation** und dann auf **Entfernen**. Akzeptieren Sie die Warnung.  

    3.  Optional können Sie den Speicher auch aus dem freigegebenen Clustervolume entfernen und ihn zu weiteren Tests zum verfügbaren Speicher zurückführen.  

        > [!NOTE]  
        > Nach dem Zurückführen zum verfügbaren Speicher müssen Sie den Volumes unter Umständen mithilfe von **DiskMgmt.msc** oder **ServerManager.exe** wieder Laufwerksbuchstaben hinzufügen.  

#### <a name="windows-powershell-method"></a>Windows PowerShell-Methode  

1.  Verwenden Sie **Get-SRGroup** und **(Get-SRGroup).Replicas**, um die aktuelle Quelle und das aktuelle Ziel der Replikation sowie den zugehörigen Status zu ermitteln.  

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

    Weitere Informationen zu Leistungsindikatoren in Windows PowerShell finden Sie unter [Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter).  

3.  Wenn Sie die Replikationsquelle und das Replikationsziel innerhalb des Stretched Clusters ändern möchten, gehen Sie wie folgt vor:  

    1.  Um die Replikationsquelle am Standort **Redmond** von einem Knoten zum anderen zu verschieben, verwenden Sie das Cmdlet „Move-ClusterSharedVolume“ und verschieben die freigegebene Clustervolumeressource.  

        ```PowerShell  
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv02  
        ```  

    2.  Um die Replikationsrichtung von einem Standort zu einem anderen „geplanten“ zu ändern, verschieben Sie die freigegebene Clustervolumeressource mithilfe des Cmdlets **Move-ClusterSharedVolume**.  

        ```PowerShell 
        Get-ClusterSharedVolume | fl *  
        Move-ClusterSharedVolume -Name "cluster disk 4" -Node sr-srv04  
        ```  

        Dadurch werden auch die Protokolle und die Daten für den anderen Standort und die anderen Knoten entsprechend verschoben.  

    3.  Um ein ungeplantes Failovers in der Replikationsrichtung von einem Standort zum anderen auszuführen, unterbrechen Sie die Stromversorgung für die beiden Knoten an einem Standort.  

        > [!NOTE]  
        > Das Speicherreplikatfeature hebt die Bereitstellung der Zielvolumes auf. Dies ist beabsichtigt.  

4.  Um die Protokoll Größe aus den standardmäßigen 8 GB zu ändern, verwenden Sie **Set-srgroup** für die Quell-und Zielspeicher Replikat Gruppen.   Legen Sie z.B. für alle Protokolle wie folgt 2GB fest:  

    ```PowerShell  
    Get-SRGroup | Set-SRGroup -LogSizeInBytes 2GB  
    Get-SRGroup  
    ```  

5.  Wenn Sie einer vorhandenen Replikationsgruppe ein weiteres Paar replizierter Datenträger hinzufügen, müssen Sie zunächst sicherstellen, dass sich im verfügbaren Speicher mindestens ein zusätzlicher Datenträger befindet. Anschließend können Sie mit der rechten Maustaste auf den Quelldatenträger klicken und „Replikationspartnerschaft hinzufügen“ auswählen.  
       >[!NOTE]
       >Die Notwendigkeit eines zusätzlichen Dummydatenträgers im verfügbaren Speicher ist Folge einer Regression und nicht beabsichtigt. Der Failovercluster-Manager hat das Hinzufügen weiterer Datenträger zuvor unterstützt, und in einer späteren Version wird das auch wieder der Fall sein.  

    Verwenden Sie das Cmdlet **Set-SRPartnership** mit den Parametern **-SourceAddVolumePartnership** und **-DestinationAddVolumePartnership**.  
6.  Zum Entfernen der Replikation verwenden Sie `Get-SRGroup`, Get-`SRPartnership`, `Remove-SRGroup` und `Remove-SRPartnership` auf jedem Knoten.  

    ```PowerShell  
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]
    > Wenn Sie einen Remoteverwaltungscomputer verwenden, müssen Sie für diese Cmdlets den Namen des Clusters und die beiden Replikationsgruppennamen angeben.  

### <a name="related-topics"></a>Verwandte Themen  
- [Speicher Replikat](storage-replica-overview.md)  
- [Replikation von Server zu Server Speicher](server-to-server-storage-replication.md)  
- [Cluster-zu-Cluster Speicher Replikation](cluster-to-cluster-storage-replication.md)  
- [Speicherreplikat: Bekannte Probleme](storage-replica-known-issues.md) 
- [Speicherreplikat: Häufig gestellte Fragen](storage-replica-frequently-asked-questions.md)  

## <a name="see-also"></a>Siehe auch  
- [Windows Server 2016](../../get-started/windows-server-2016.md)  
- [Direkte Speicherplätze in Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)
