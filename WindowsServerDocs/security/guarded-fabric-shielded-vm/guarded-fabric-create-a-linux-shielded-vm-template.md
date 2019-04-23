---
title: Erstellen eines abgeschirmten Linux-Datenträger der VM-Vorlage
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e791d18e027e5e3e1c5b9c52659641ff588a96a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858671"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>Erstellen eines abgeschirmten Linux-Datenträger der VM-Vorlage

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal) 

In diesem Thema wird erläutert, wie Sie einen vorlagendatenträger Vorbereiten für Linux-VMs, die verwendet werden können abgeschirmten, um eine oder mehrere Mandanten-VMs zu instanziieren.

## <a name="prerequisites"></a>Vorraussetzungen

Zum Vorbereiten und Testen einer abgeschirmten Linux-VM, benötigen Sie die folgenden Ressourcen:

- Ein Server mit Virtualisierung Capababilities mit Windows Server, Version 1709 oder höher
- Einem zweiten Computer (Windows 10 oder Windows Server 2016) Hyper-V-Manager zur Verbindung mit der ausgeführten VM-Konsole ausgeführt werden kann
- Ein ISO-Abbild für eine der unterstützten Linux-abgeschirmte VM-Betriebssysteme:
    - Ubuntu 16.04 LTS mit dem Kernel 4.4
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 Service Pack 2
- Zugriff auf das Internet zum Herunterladen des Lsvmtools-Paket und Betriebssystemupdates

> [!IMPORTANT]
> Neuere Versionen der Linux-OSes ein bekanntes Problem des TPM-Treiber, das diese Bereitstellung wurde erfolgreich enthalten kann als verhindern vorangehenden abgeschirmte VMs.
> Es wird nicht empfohlen, dass Sie Ihre Vorlagen aktualisieren oder VMs auf eine neuere Version, abgeschirmte bis eine Korrektur verfügbar ist.
> Die Liste der unterstützten Betriebssysteme, die oben genannten wird aktualisiert werden, wenn die Updates öffentlich gemacht werden.

## <a name="prepare-a-linux-vm"></a>Vorbereiten einer Linux-VM

Abgeschirmte VMs werden aus sicheren vorlagedatenträger erstellt.
Vorlagedatenträger enthalten das Betriebssystem für den virtuellen Computer und die Metadaten, einschließlich einer digitalen Signatur der/Boot "und" / Root-Partitionen, um sicherzustellen, dass die zentralen Betriebssystemkomponenten vor der Bereitstellung nicht geändert werden.

Um einen vorlagendatenträger erstellen zu können, müssen Sie zuerst einen normalen (nicht geschirmten) virtuellen Computer erstellen, die Sie als Basisimage für zukünftige abgeschirmte VMs vorbereitet werden.
Die Software, die Sie installieren und die Änderungen an der Konfiguration, die Sie an diesen virtuellen Computer gilt für alle geschützten VMs, die aus dieser vorlagendatenträger erstellt wurde.
Diese Schritte begleiten Sie durch die Mindestanforderungen auf einer Linux-VM Templatization vorzubereiten.

> [!NOTE]
> Linux-datenträgerverschlüsselung wird konfiguriert, wenn der Datenträger partitioniert ist.
> Dies bedeutet, die Sie einen neuen virtuellen Computer erstellen müssen, die mithilfe von dm-Crypt zum Erstellen eines Linux bereits verschlüsselt ist abgeschirmte vorlagedatenträger VM.


1.  Klicken Sie auf dem Virtualisierungsserver stellen Sie sicher, dass Hyper-V und die Funktionen der Hyper-V-Unterstützung für Host-Überwachungsdiensts installiert werden, indem Sie die folgenden Befehle in einer PowerShell-Konsole mit erhöhten Rechten ausführen:

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  Laden Sie das ISO-Abbild von einer vertrauenswürdigen Quelle herunter, und auf dem Server Virtualization oder auf einer Dateifreigabe für Ihren Virtualisierungsserver zugänglich zu speichern.

3.  Installieren Sie die abgeschirmte VM Remoteserver-Verwaltungstools auf Ihrem Computer Management mit Windows Server, Version 1709 durch den folgenden Befehl ausführen:

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  Open **Hyper-V-Manager** auf Ihrem Computer Management und eine Verbindung mit dem Server Virtualization.
    Sie erreichen dies durch Klicken auf "Verbindung zum Server …" in den Bereich "Aktionen" oder mit der rechten "Verbinden auf Hyper-V-Manager darauf klicken und auswählen mit Server..." Geben Sie den DNS-Namen für den Hyper-V-Server und, falls erforderlich, die erforderlichen Anmeldeinformationen herstellen.

5.  Mit dem Hyper-V-Manager, [konfigurieren ein externes Switches](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines) auf dem Server Virtualization, damit die Linux-VM, das Internet zugreifen können, um Updates zu erhalten.

6.  Als Nächstes erstellen Sie einen neuen virtuellen Computer verwenden, um auf Linux-Betriebssystem zu installieren.
    Klicken Sie im Aktionsbereich auf **neu** > **VM** , um den Assistenten zu öffnen.
    Geben Sie einen Anzeigenamen für den virtuellen Computer, z. B. "Pre-templatized Linux", und klicken Sie auf **Weiter**.

7.  Wählen Sie auf der zweiten Seite des Assistenten, **Generation 2** um sicherzustellen, dass die VM mit einem UEFI-basierter Firmware-Profil bereitgestellt wird.

8.  Führen Sie den Assistenten nach Ihren Bedürfnissen an.
    Verwenden Sie einen differenzierenden Datenträger nicht für diesen virtuellen Computer. vorlagendatenträger für abgeschirmte virtuelle Computer können keine differenzierende Datenträgern.
    Schließlich verbinden Sie das ISO-Abbild, die, das Sie zuvor auf dem virtuellen DVD-Laufwerk für diesen virtuellen Computer heruntergeladen, damit Sie das Betriebssystem installieren können.

9.  Wählen Sie im Hyper-V-Manager Ihren neu erstellten virtuellen Computer aus, und klicken Sie auf **verbinden...**  im Bereich "Aktionen" auf einer virtuellen-Konsole des virtuellen Computers anfügen.
    Klicken Sie im Fenster, das angezeigt wird, auf **starten** auf dem virtuellen Computer zu aktivieren.

10. Für Ihre ausgewählte Linux-Verteilung durch die Installation fortgesetzt werden.
    Während jedes Linux-Distribution ein anderen Setup-Assistenten verwendet, müssen die folgenden Anforderungen erfüllt sein, für die Datenträger der VM-Vorlage von abgeschirmten VMs, die Linux werden sollen:

    - Der Datenträger muss partitioniert werden mit dem Layout Paritioning Tabelle GPT (GUID)
    - Das Stammpartition muss mit der dm-Crypt verschlüsselt werden. Die Passphrase sollte festgelegt werden, um **Passphrase** (nur Kleinbuchstaben). Diese Passphrase wird zufällig festgelegt werden, und die Partition wieder verschlüsselt, wenn eine abgeschirmte VM bereitgestellt wird.
    - Verwenden Sie die Startpartition muss die **ext2** -Dateisystem

11. Sobald Ihr Linux-Betriebssystem vollständig gestartet wurde, und Sie angemeldet haben, empfiehlt es sich, dass Sie den virtuellen Linux-Kernel und die zugehörigen Hyper-V Integration Services-Pakete installieren.
    Darüber hinaus möchten Sie installieren ein SSH-Server oder andere Remoteverwaltungstools, um den virtuellen Computer zugreifen, nachdem sie geschützt ist.

    Führen Sie den folgenden Befehl zum Installieren dieser Komponenten unter Ubuntu:

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    Führen Sie unter RHEL stattdessen den folgenden Befehl aus:

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    Und unter SLES, führen Sie den folgenden Befehl aus:

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. Konfigurieren Sie Ihre Linux-Betriebssystem wie gewünscht.
    Jede Software Installation, Benutzerkonten, die Sie hinzufügen möchten, die und systemweite konfigurationsänderungen vornehmen, Sie gelten für alle zukünftigen erstellten virtuellen Computer anhand dieses Datenträgers Vorlage.
    Vermeiden Sie die geheimen Schlüssel oder nicht benötigte Pakete auf dem Datenträger gespeichert.

13. Wenn Sie System Center Virtual Machine Manager zu verwenden, um Ihre virtuellen Computer bereitstellen möchten, installieren Sie den VMM-Gast-Agent, um VMM spezialisiert werden Ihr Betriebssystem während der Bereitstellung der VM zu aktivieren.
    Dank der Spezialisierung kann jeden virtuellen Computer sicher mit verschiedenen Benutzern und SSH-Schlüssel, Netzwerkkonfigurationen und benutzerdefinierte Setupschritte eingerichtet werden.
    Erfahren Sie, wie Sie [beziehen und installieren den VMM-Gast-Agent](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent) in der Dokumentation zu VMM.

14. Als Nächstes [Ihr Paket-Manager die Microsoft-Linux-Softwarerepository hinzugefügt](../../administration/linux-package-repository-for-microsoft-software.md).

15. Mithilfe des Paket-Managers, geschützte installieren das Lsvmtools-Paket enthält die Linux VM-Bootloader-Shim, Komponenten und datenträgervorbereitungstool-Bereitstellung.

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. Wenn Sie fertig sind anpassen Linux-Betriebssystem, suchen Sie das Installationsprogramm Lsvmprep auf Ihrem System, und führen Sie sie.
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. Herunterfahren Sie Ihres virtuellen Computers ein.

16. Wenn Sie alle Prüfpunkte des virtuellen Computers (einschließlich automatische Prüfpunkte erstellt, die von Hyper-V, mit der Windows 10 Fall Creators Update) durchgeführt haben, achten Sie darauf, dass Sie sie löschen, bevor Sie fortfahren.
    Prüfpunkte erstellen, differenzierende Datenträger (.avhdx), die von den Vorlagendatenträger-Assistenten nicht unterstützt werden.
    
    Um Prüfpunkte zu löschen, öffnen Sie **Hyper-V-Manager**, wählen Sie den Computer, klicken Sie mit der rechten Maustaste auf den obersten Prüfpunkt im Bereich Prüfpunkte, und klicken Sie dann **Löschen von Prüfpunkt-Unterstruktur**.

    ![Löschen Sie alle Prüfpunkte für die VM-Vorlage im Hyper-V-manager](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>Schützen Sie den vorlagendatenträger

Der virtuelle Computer, die Sie im vorherigen Abschnitt vorbereitet ist fast bereit, wie einer Linux-Datenträger der VM-Vorlage abgeschirmten verwendet werden.
Der letzte Schritt ist die Ausführung des Datenträgers über den Vorlagendatenträger-Assistenten, der hash und digitalen Signieren von den aktuellen Status der Stamm "und" Boot Partitionen.
Der Hash und der digitalen Signatur werden überprüft, wenn eine abgeschirmte VM bereitgestellt wird, um sicherzustellen, dass nicht autorisierten Änderungen an den beiden Partitionen zwischen Erstellung und Bereitstellung vorgenommen wurden.

### <a name="obtain-a-certificate-to-sign-the-disk"></a>Rufen Sie ein Zertifikat zum Signieren des Datenträgers

Um die Datenträger-Messungen digital zu signieren, müssen Sie ein Zertifikat auf dem Computer zu erhalten, in dem Sie den Vorlagendatenträger-Assistenten ausgeführt werden.
Das Zertifikat muss die folgenden Anforderungen erfüllen:

Certificate-Eigenschaft | Erforderlicher Wert
---------------------|---------------
Schlüsselalgorithmus | RSA
Minimale Schlüsselgröße | 2048 Bit
Signaturalgorithmus | SHA256 (empfohlen)
Schlüsselverwendung | Digitale Signatur

Details zu diesem Zertifikat werden für Mandanten angezeigt werden, bei der Erstellung ihrer schutzdatendateien und Autorisieren von Datenträgern, denen, die Sie vertrauen, werden.
Aus diesem Grund ist es wichtig, um dieses Zertifikat von einer Zertifizierungsstelle, die von Ihnen und Ihren Mandanten sich gegenseitig vertrauenswürdigen zu erhalten.
In Enterprise-Szenarien, in denen Sie sowohl Hoster als auch Mandant sind, sollten Sie dieses Zertifikat von Ihrer Unternehmenszertifizierungsstelle ausgestellt.
Dieses Zertifikat sorgfältig geschützt, da jeder Benutzer im Besitz dieses Zertifikats erstellen, kann neue Festplatten der Vorlage, die vertrauenswürdige Ihre Authentizität Datenträger identisch.

In einer testumgebung auszuführen können Sie ein selbstsigniertes Zertifikat mithilfe des folgenden PowerShell-Befehls erstellen:

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>Verarbeiten Sie den Datenträger mit dem Cmdlet Vorlagendatenträger-Assistenten

Kopieren Sie Ihre vorlagendatenträger Zertifikat auf einem Computer mit Windows Server, Version 1709, und führen Sie die folgenden Befehle zum Prozess den signaturvergabe initiieren.
Die VHDX, die Sie, um angeben die `-Path` Typparameter wird mit dem Datenträger für die aktualisierte Vorlage überschrieben werden, daher unbedingt eine Kopie zu erstellen, bevor der Befehl ausgeführt wird.

> [!IMPORTANT]
> Der Remoteserver-Verwaltungstools auf Windows Server 2016 oder Windows 10 kann nicht verwendet werden, zum Vorbereiten einer abgeschirmten Linux VM-Vorlage-Datenträger.
> Verwenden Sie nur die [schützen-TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps) Cmdlet verfügbar unter Windows Server, Version 1709 oder die Remoteserver-Verwaltungstools auf Windows Server-2019 verfügbar, zum Vorbereiten eines Linux abgeschirmte vorlagedatenträger VM.

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

Ihre vorlagendatenträger kann jetzt zum Bereitstellen der abgeschirmten Linux-VMs verwendet werden.
Wenn Sie System Center Virtual Machine Manager zur Bereitstellung Ihrer VM verwenden, können Sie jetzt die VHDX auf die VMM-Bibliothek kopieren.

Sie sollten auch die Volume-signaturkatalogs von VHDX zu extrahieren.
Diese Datei wird verwendet, Informationen über das Signaturzertifikat, Datenträgername und Version um VM-Besitzer ermöglichen Ihrer Vorlage verwendet werden soll.
Sie müssen diese Datei in den Assistenten für geschützte Datendateien, autorisieren Sie den Autor der Vorlage im Besitz des Signaturzertifikats, zum Erstellen dieser importieren und zukünftige Vorlage für diese Datenträger.

Um die Volume-signaturkatalogs zu extrahieren, führen Sie den folgenden Befehl in PowerShell aus:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
