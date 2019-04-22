---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: Abgeschirmte virtuelle Computer für Mandanten – Erstellen einer neuen abgeschirmten VM lokal und verschiebt es in ein geschütztes fabric
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2da1e33d24fa6d68815f4fbc0891be0616004856
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817471"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>Abgeschirmte virtuelle Computer für Mandanten – Erstellen einer neuen abgeschirmten VM lokal und verschiebt es in ein geschütztes fabric

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


<!-- NOTE THAT THIS FILE HAS A "redirect_url" LINE IN THE METADATA. EVENTUALLY WE WILL PROBABLY STRIP OUT THE DETAILED METADATA AND THE CONTENT BELOW, SO IT'S PURELY A REDIRECTED TOPIC. However, as of mid-November 2016, we're still deciding. -->



In diesem Thema wird beschrieben, die Schritte zum Erstellen einer abgeschirmten VM mit nur Hyper-V; d. h. ohne Virtual Machine Manager, vorlagendatenträger oder eine geschützte Datendatei. Dies ist ein ungewöhnliches Szenario für die meisten öffentlichen Cloud-Hostingumgebungen, jedoch kann nützlich sein, wenn Sie ein geschütztes Fabric zu testen, oder klicken Sie in Unternehmen Szenarien, in denen ein virtuellen Computer aus eine Textur auf Abteilungsebene zu verschoben wird, IT-Infrastruktur freigegeben, und vor der Migration verschlüsselt werden müssen.

Um zu verstehen, wie in diesem Thema in den gesamten Vorgang der Bereitstellung von abgeschirmten VMs passt, finden Sie unter [Service Provider-Konfigurationsschritte für das Hosten von überwachten Hosts und abgeschirmte VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>Importieren Sie die Konfiguration der Überwachungsdienst auf dem Hyper-V-mandantenserver

1.  Bevor Sie mit die Prozedur beginnen, sicher, dass Sie auf einem Hyper-V-Host unter Windows Server 2016 mit den folgenden Rollen und Features installiert sind:

    - Role-Eigenschaft

        - Hyper-V

    - Features

        - Remoteserver-Verwaltungstools\\Feature-Verwaltungstools\\abgeschirmte VM-Tools

    > [!NOTE]
    > Sollten Sie der Host, der hier verwendete *nicht* werden von ein Host in der geschützten Fabrics. Dies ist es sich um einen separaten Host, in dem virtuellen Computer vorbereitet werden, vor dem Verschieben auf des geschützten Fabrics.

2.  Bevor Sie eine abgeschirmte VM auf diesem Computer ausführen können, müssen Sie sicherstellen, dass die virtualisierungsbasierte Sicherheit aktiviert ist und ausgeführt wird. Führen Sie den folgenden Befehl in einem erhöhten Windows PowerShell-Fenster zur Installation der Hyper-V-Unterstützung für Host-Überwachungsdiensts-Funktion. Dadurch wird alle erforderlichen Einstellungen konfiguriert, auf dem Computer, um abgeschirmte VMs ausführen zu können.

        Install-WindowsFeature HostGuardian

3.  Sie benötigen, der überwachungsmetadaten für die geschützte Fabric abzurufen, in dem Ihr virtueller Computer ausgeführt wird. Diese Metadaten werden verwendet, zum Autorisieren von diesem Fabric an, die abgeschirmte VM ausgeführt werden. Wie Sie diese Informationen erhalten werden für jede hosting-Anbieter oder das Unternehmen unterscheiden. Der Hoster (oder Sie, wenn Sie auf dem geschützten Fabric-Netzwerk zugreifen) können diese Informationen abzurufen, durch den folgenden Windows PowerShell-Befehl ausführen:

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    Im obigen Beispiel "Host-Überwachungsdienst" ist der Name der verteilten Netzwerk des Host-Überwachungsdienst-Clusters, und "bastion.local" ist der Name der HGS-Domäne.

4.  Zum Importieren von des Überwachungsdienst-Schlüssels, die Sie in einer späteren Prozedur benötigen, führen Sie den folgenden Befehl aus.

    Für &lt;Pfad&gt;&lt;Filename&gt;, ersetzen Sie den Pfad und Dateiname der XML-Datei, die Sie im vorherigen Schritt gespeichert sind, z.B.: **"C:"\\Temp\\GuardianKey.xml**

    Für &lt;GuardianName&gt;, geben Sie einen Namen für Ihre hosting-Anbieter oder das Datencenter eines Unternehmens, z. B. **HostingProvider1**. Notieren Sie den Namen für den nächsten Vorgang.

    Umfassen **- AllowUntrustedRoot** nur dann, wenn der HGS-Server mit selbstsignierten Zertifikaten eingerichtet wurde. (Diese Zertifikate sind Teil der Schlüsselschutzdienst in Host-Überwachungsdienst.)

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>Erstellen Sie eine neue abgeschirmte virtuelle Maschine auf dem host

Sie werden in diesem Verfahren erstellen einen virtuellen Computer, auf dem Hyper-V-Host und Vorbereiten für den Export in Ihrem Hostinganbieter oder Datencenter-Administrator, die auf einem bewachten Host ausgeführt werden kann.

Im Rahmen des Verfahrens erstellen Sie eine Schlüsselschutzvorrichtung, die zwei wichtige Elemente enthält:

-   **Besitzer**: In der Schlüsselschutzvorrichtung, werden Sie – oder wahrscheinlicher ist es möglich, die Gruppe die, Arbeit, die gemeinsam Sicherheitselemente wie z. B. Zertifikate – als "Besitzer" des virtuellen Computers identifiziert. Ihre Identität als Besitzer wird durch ein Zertifikat dargestellt, die, wenn Sie die Befehle ausführen, wie gezeigt, wie ein selbst signiertes Zertifikat generiert wird. Optional können Sie stattdessen verwenden Sie ein Zertifikat von PKI-Infrastruktur unterstützt und lassen Sie die **- AllowUntrustedRoot** Parameter in den Befehlen.

-   **Überwachungen**: Außerdem wird in die Schlüsselschutzvorrichtung, Ihr Hostinganbieter oder Enterprise-Datacenter (der Host-Überwachungsdiensts und überwachter Hosts ausgeführt wird) als ein "Wächter". identifiziert Der Überwachungsdienst wird dargestellt, mit dem Überwachungsdienst-Schlüssel, die Sie in der vorherigen Prozedur importiert [importieren Sie die Konfiguration der Überwachungsdienst auf dem Hyper-V-mandantenserver](#import-the-guardian-configuration-on-the-tenant-hyper-v-server).

Eine Abbildung, zeigt die Schlüsselschutzvorrichtung, die ein Element in eine geschützte Datendatei ist, finden Sie unter [welche Daten Schutz ist und warum dies erforderlich ist?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary).

1.  Führen Sie auf einem Hyper-V-Host-Mandanten zum Erstellen einer neuen Generation 2 VM den folgenden Befehl ein.

    Für &lt;ShieldedVMname&gt;, geben Sie einen Namen für den virtuellen Computer, z.B.: **ShieldVM1**
    
    Für &lt;%vhdpath&gt;, geben Sie einen Speicherort zum Speichern von VHDX des virtuellen Computers, z.B.: **C:\\VMs\\ShieldVM1\\ShieldVM1.vhdx**
    
    Für &lt;NnGB&gt;, geben Sie z. B. eine Größe für die VHDX: **60GB**

        New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2.  Installieren Sie ein unterstütztes Betriebssystem (WindowsServer 2012 oder höher, Windows 8-Client oder höher) auf dem virtuellen Computer, und aktivieren Sie die Remotedesktopverbindung und den entsprechenden Firewall-Regel. Notieren Sie IP-Adresse bzw. in der DNS-Namen des virtuellen Computers an; Sie benötigen diese Remote eine Verbindung damit herstellen.

3.  Verwenden Sie RDP, Remote eine Verbindung mit dem virtuellen Computer und stellen Sie sicher, dass RDP und die Firewall ordnungsgemäß konfiguriert sind. Als Teil des geschützten Prozesses ist Konsolenzugriff auf den virtuellen Computer über Hyper-V deaktiviert werden, daher es wichtig ist, um sicherzustellen, dass Sie das System Remote über das Netzwerk verwalten können.

4.  Führen Sie den folgenden Befehl, um eine neue Schlüsselschutzvorrichtung (am Anfang des in diesem Abschnitt beschrieben) zu erstellen.

    Für &lt;GuardianName&gt;, den angegebenen Namen in der vorherigen Prozedur, z. B. verwenden: **HostingProvider1**

    Umfassen **- AllowUntrustedRoot** um selbstsignierte Zertifikate zu ermöglichen.

        $Guardian = Get-HgsGuardian -Name '<GuardianName>'

        $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

        $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

    Wenn Sie sich für mehr als einem Rechenzentrum, um Ihre abgeschirmte VM (z. B. Standort für die notfallwiederherstellung und einem öffentlichen Cloudanbieter) ausgeführt werden zu können möchten, können Sie eine Liste von Überwachungen auf Bereitstellen der **-Überwachungsdienst** Parameter. Weitere Informationen finden Sie unter [New-HgsKeyProtector] (https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-ps.

5.  Führen Sie den folgenden Befehl, um die vTPM mithilfe der Schlüsselschutzvorrichtung zu aktivieren. Für &lt;ShieldedVMname&gt;, verwenden Sie den gleichen VM-Namen in den vorherigen Schritten verwendet.

        $VMName="<ShieldedVMname>"

        Stop-VM -Name $VMName -Force

        Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

        Set-VMSecurityPolicy -VMName $VMName -Shielded $true

        Enable-VMTPM -VMName $VMName

6.  Führen Sie den folgenden Befehl zum Starten des virtuellen Computers, um sicherzustellen, dass die Schlüsselschutzvorrichtung mit lokalen besitzerzertifikate arbeitet.

        Start-VM -Name $VMName

7.  Stellen Sie sicher, dass der virtuelle Computer in der Hyper-V-Konsole gestartet wurde.

8.  Verwenden Sie RDP, Remote eine Verbindung mit dem virtuellen Computer und Aktivieren von BitLocker auf alle Partitionen auf alle vhdx-Dateien, die die abgeschirmte VM angefügt sind.

    > [!IMPORTANT]
    > Warten Sie vor dem Fortfahren mit dem nächsten Schritt die BitLocker-Verschlüsselung für alle Partitionen abgeschlossen, in denen es aktiviert.

9.  Herunterfahren des virtuellen Computers ein, wenn Sie bereit sind, verschieben Sie es zum überwachten Fabric.

10.  Exportieren Sie den virtuellen Computer mit dem Tool Ihrer Wahl (Windows PowerShell oder Hyper-V-Manager), auf dem Hyper-V-mandantenserver. Ordnen Sie für die Dateien auf einem bewachten Host verwaltet, die von Ihrem Hostinganbieter oder Unternehmensrechenzentren kopiert werden sollen.

11.  **Für das hosting-Anbieter bzw. unternehmensrechenzentrums**:

    Importieren Sie die abgeschirmte VM, die mit dem Hyper-V-Manager oder Windows PowerShell. Sie müssen die Konfigurationsdatei des virtuellen Computers aus der VM-Besitzer importieren, um den virtuellen Computer zu starten. Dies ist, da die Schlüsselschutzvorrichtung "und" virtual TPM des virtuellen Computers in der Konfigurationsdatei gespeichert werden. Wenn der virtuelle Computer für die Ausführung auf dem geschützten Fabric konfiguriert ist, sollte er erfolgreich starten können.

## <a name="see-also"></a>Siehe auch

- [Hosten von Service Provider-Konfigurationsschritte für die überwachten Hosts und abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
