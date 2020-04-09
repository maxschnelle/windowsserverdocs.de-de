---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: 'Abgeschirmte VMs für Mandanten: lokales Erstellen einer neuen abgeschirmten VM und verschieben in ein geschütztes Fabric'
ms.prod: windows-server
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: a5ca3ab29b83d0cb6cb2d55507471790f65800a2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856723"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>Abgeschirmte VMs für Mandanten: lokales Erstellen einer neuen abgeschirmten VM und verschieben in ein geschütztes Fabric

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die Schritte zum Erstellen einer abgeschirmten VM unter Verwendung von Hyper-V beschrieben. Das heißt, ohne Virtual Machine Manager, Vorlagen Datenträger oder eine geschützte Datendatei. Dies ist ein ungewöhnliches Szenario für die meisten Public Cloud Hostingumgebungen, kann jedoch beim Testen eines geschützten Fabrics oder in Unternehmens Szenarios nützlich sein, in denen ein virtueller Computer von einem Abteilungs-Fabric in eine freigegebene IT-Infrastruktur verschoben wird und vor der Migration verschlüsselt werden muss.

Informationen dazu, wie sich dieses Thema in den Gesamtprozess der Bereitstellung von abgeschirmten VMS einfügt, finden Sie unter [Hosten von Dienstanbietern Konfigurationsschritte für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>Importieren der Überwachungskonfiguration auf dem Hyper-V-Mandanten Server

1.  Stellen Sie vor Beginn des Verfahrens sicher, dass Sie sich auf einem Hyper-V-Host mit Windows Server 2016 mit den folgenden installierten Rollen und Features befinden:

    - Rolle

        - Hyper-V

    - Features

        - Remoteserver-Verwaltungstools\\Features-Verwaltungs Tools\\abgeschirmte VM-Tools

    > [!NOTE]
    > Der hier verwendete Host sollte *kein* Host im geschützten Fabric sein. Dabei handelt es sich um einen separaten Host, auf dem VMS vorbereitet werden, bevor Sie in das geschützte Fabric verschoben werden.

2.  Bevor Sie auf diesem Computer eine abgeschirmte VM ausführen können, müssen Sie sicherstellen, dass die virtualisierungsbasierte Sicherheit aktiviert ist und ausgeführt wird. Führen Sie den folgenden Befehl in einem Windows PowerShell-Fenster mit erhöhten Rechten aus, um die Hyper-V-Unterstützung des Host-Überwachungstools Dadurch werden alle erforderlichen Einstellungen auf Ihrem Computer konfiguriert, um abgeschirmte VMS ausführen zu können.

        Install-WindowsFeature HostGuardian

3.  Sie müssen die Überwachungs Metadaten für das geschützte Fabric abrufen, in dem Ihr virtueller Computer ausgeführt wird. Diese Metadaten werden verwendet, um dieses Fabric zum Ausführen ihrer abgeschirmten VM zu autorisieren. Die Art und Weise, wie Sie diese Informationen erhalten, unterscheidet sich für jeden hostingdienstanbieter oder jedes Der Host (oder Sie, wenn Sie Zugriff auf das geschützte Fabric-Netzwerk haben) kann diese Informationen abrufen, indem Sie den folgenden Windows PowerShell-Befehl ausführen:

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    Im obigen Beispiel ist "HGS" der verteilte Netzwerkname des HGS-Clusters und "Bastion. local" der Name der HGS-Domäne.

4.  Führen Sie den folgenden Befehl aus, um den Überwachungs Schlüssel zu importieren, den Sie in einem späteren Verfahren benötigen.

    Geben Sie für &lt;Pfad&gt;&lt;filename-&gt;den Pfad und den Dateinamen der XML-Datei ein, die Sie im vorherigen Schritt gespeichert haben, z. b.: **C:\\Temp\\guardiankey. XML**

    Geben Sie für den&gt;&lt;guardianname einen Namen für den Hostinganbieter oder das Unternehmens Rechenzentrum ein, z. b. **HostingProvider1**. Notieren Sie sich den Namen für das nächste Verfahren.

    Include **-zuordnertreuhändroot** nur, wenn der HGS-Server mit selbst signierten Zertifikaten eingerichtet wurde. (Diese Zertifikate sind Teil des Schlüsselschutz Dienstanbieter in HGS.)

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>Erstellen einer neuen abgeschirmten virtuellen Maschine auf dem Host

In diesem Verfahren erstellen Sie eine virtuelle Maschine auf dem Hyper-V-Host und bereiten Sie für den Export in ihren Hostinganbieter oder Datacenter-Administrator vor, der Sie auf einem überwachten Host ausführen kann.

Im Rahmen des Verfahrens erstellen Sie eine Schlüssel Schutzvorrichtung, die zwei wichtige Elemente enthält:

-   **Besitzer**: in der Schlüssel Schutzvorrichtung sind Sie oder wahrscheinlicher, dass die Gruppe, in der Sie arbeiten, die Sicherheitselemente wie Zertifikate verwendet, als "Besitzer" des virtuellen Computers bezeichnet wird. Ihre Identität als Besitzer wird durch ein Zertifikat dargestellt, das, wenn Sie die Befehle wie dargestellt ausführen, als selbst signiertes Zertifikat generiert wird. Optional können Sie stattdessen ein Zertifikat verwenden, das von der PKI-Infrastruktur unterstützt wird, und den Parameter " **-Zuweisung wuntreudroot** " in den Befehlen weglassen.

-   **Wächter**: in der Schlüssel Schutzvorrichtung wird auch der Hostinganbieter oder das Unternehmens Rechenzentrum (das HGS und geschützte Hosts ausführt) als "Wächter" bezeichnet. Der Wächter wird durch den in der vorherigen Prozedur importierten Überwachungs Schlüssel dargestellt. importieren Sie [die Überwachungskonfiguration auf dem Hyper-V-Mandanten Server](#import-the-guardian-configuration-on-the-tenant-hyper-v-server).

Eine Abbildung der Schlüssel Schutzvorrichtung, bei der es sich um ein Element in einer Schutz Datendatei handelt, finden [Sie unter Was sind geschützte Daten und warum ist es erforderlich?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

1. Führen Sie auf einem Mandanten-Hyper-V-Host den folgenden Befehl aus, um einen neuen virtuellen Computer der Generation 2 zu erstellen.

   Geben Sie für &lt;shieldebug Name&gt;einen Namen für den virtuellen Computer an, z. b.: **ShieldVM1**
    
   Geben Sie für &lt;vhdpath-&gt;einen Speicherort zum Speichern der vhdx-Datei des virtuellen Computers an, z. b.: **C:\\VMS\\ShieldVM1\\ShieldVM1. vhdx**
    
   Geben Sie für &lt;nngb-&gt;eine Größe für die vhdx-Datei an, z. b. **60 GB** .

       New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2. Installieren Sie ein unterstütztes Betriebssystem (Windows Server 2012 oder höher, Windows 8-Client oder höher) auf dem virtuellen Computer, und aktivieren Sie die Remote Desktop Verbindung und die entsprechende Firewallregel. Notieren Sie die IP-Adresse und/oder den DNS-Namen des virtuellen Computers. Sie benötigen Sie, um eine Remote Verbindung mit dem Dienst herzustellen.

3. Stellen Sie mithilfe von RDP eine Remote Verbindung mit der VM her, und überprüfen Sie, ob RDP und die Firewall ordnungsgemäß konfiguriert sind Im Rahmen des Schutz Prozesses wird der Konsolenzugriff auf den virtuellen Computer über Hyper-V deaktiviert. Daher ist es wichtig, sicherzustellen, dass Sie das System über das Netzwerk remote verwalten können.

4. Führen Sie den folgenden Befehl aus, um eine neue Schlüssel Schutzvorrichtung zu erstellen (die am Anfang dieses Abschnitts beschrieben wird).

   Verwenden Sie für &lt;guardianname&gt;den Namen, den Sie im vorherigen Verfahren angegeben haben, z. b.: **HostingProvider1**

   Include **-zusorwuntreuhändroot** , um selbst signierte Zertifikate zuzulassen.

       $Guardian = Get-HgsGuardian -Name '<GuardianName>'

       $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

       $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

   Wenn Sie möchten, dass mehr als ein Rechenzentrum Ihre abgeschirmte VM ausführen kann (z. b. ein Standort für die Notfall Wiederherstellung und ein Public Cloud Anbieter), können Sie dem **-Wächter-** Parameter eine Liste von Erziehungsberechtigten bereitstellen. Weitere Informationen finden Sie unter [New-hgskeyprotector] (https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-ps.

5. Um das vtpm mithilfe der Schlüssel Schutzvorrichtung zu aktivieren, führen Sie den folgenden Befehl aus. Verwenden Sie für &lt;shieldedvmname-&gt;denselben VM-Namen, den Sie in den vorherigen Schritten verwendet haben.

       $VMName="<ShieldedVMname>"

       Stop-VM -Name $VMName -Force

       Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

       Set-VMSecurityPolicy -VMName $VMName -Shielded $true

       Enable-VMTPM -VMName $VMName

6. Führen Sie den folgenden Befehl aus, um den virtuellen Computer zu starten, um zu überprüfen, ob die Schlüssel Schutzvorrichtung mit lokalen Besitzer Zertifikaten arbeitet.

       Start-VM -Name $VMName

7. Vergewissern Sie sich, dass der virtuelle Computer in der Hyper-V-Konsole gestartet wurde.

8. Stellen Sie mithilfe von RDP eine Remote Verbindung mit dem virtuellen Computer her, und aktivieren Sie BitLocker für alle Partitionen auf allen vhdx-Computern, die mit der abgeschirmten VM verbunden sind

   > [!IMPORTANT]
   > Bevor Sie mit dem nächsten Schritt fortfahren, warten Sie, bis die BitLocker-Verschlüsselung auf allen Partitionen abgeschlossen ist, auf denen Sie aktiviert wurde.

9. Fahren Sie die VM herunter, wenn Sie bereit sind, Sie in das geschützte Fabric zu verschieben.

10. Exportieren Sie den virtuellen Computer auf dem Hyper-v-Mandanten Server mit dem Tool Ihrer Wahl (Windows PowerShell oder Hyper-v-Manager). Ordnen Sie dann die Dateien an, die auf einen überwachten Host kopiert werden sollen, der von Ihrem Hostinganbieter oder Unternehmens Rechenzentrum verwaltet wird.

11. **Für den Hostinganbieter oder das Unternehmens**Rechenzentrum:

    Importieren Sie den abgeschirmten virtuellen Computer mit dem Hyper-V-Manager oder mit Windows PowerShell. Sie müssen die VM-Konfigurationsdatei vom Besitzer der VM importieren, um den virtuellen Computer zu starten. Dies liegt daran, dass die Schlüssel Schutzvorrichtung und das virtuelle TPM des virtuellen Computers in der Konfigurationsdatei gespeichert werden. Wenn der virtuelle Computer für die Durchführung auf dem geschützten Fabric konfiguriert ist, sollte er erfolgreich gestartet werden können.

## <a name="see-also"></a>Siehe auch

- [Konfigurationsschritte des hostingdienstanbieters für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
