---
title: Erstellen eines virtuellen Linux-VM-Vorlagen Datenträgers
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 66d5f70f747a6209f2856afde58b6f486ea597f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386706"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>Erstellen eines virtuellen Linux-VM-Vorlagen Datenträgers

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), 

In diesem Thema wird erläutert, wie ein Vorlagen Datenträger für abgeschirmte Linux-VMs vorbereitet wird, mit denen eine oder mehrere Mandanten-VMS instanziiert werden können.

## <a name="prerequisites"></a>Erforderliche Komponenten

Zum Vorbereiten und Testen einer abgeschirmten Linux-VM benötigen Sie die folgenden verfügbaren Ressourcen:

- Ein Server mit Virtualisierungsplattformen, auf denen Windows Server, Version 1709 oder höher, ausgeführt wird
- Ein zweiter Computer (Windows 10 oder Windows Server 2016), der Hyper-V-Manager zum Herstellen einer Verbindung mit der Konsole des laufenden virtuellen Computers ausführen muss
- Ein ISO-Abbild für einen der unterstützten Linux-VM-Betriebssysteme:
    - Ubuntu 16,04 LTS mit dem 4,4-Kernel
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 Service Pack 2
- Internet Zugriff zum Herunterladen des lsvmtools-Pakets und der Betriebssystemupdates

> [!IMPORTANT]
> Neuere Versionen der vorangehenden Linux-Betriebssysteme können einen bekannten TPM-Treiber Fehler enthalten, der verhindert, dass Sie als abgeschirmte VMS erfolgreich bereitgestellt werden.
> Es wird nicht empfohlen, Ihre Vorlagen oder abgeschirmten VMS auf eine neuere Version zu aktualisieren, bis eine Korrektur vorliegt.
> Die Liste der oben unterstützten Betriebssysteme wird aktualisiert, wenn die Updates öffentlich gemacht werden.

## <a name="prepare-a-linux-vm"></a>Vorbereiten einer Linux-VM

Abgeschirmte VMS werden aus sicheren Vorlagen Datenträgern erstellt.
Vorlagen Datenträger enthalten das Betriebssystem für den virtuellen Computer und die Metadaten, einschließlich einer digitalen Signatur der/Boot-und/Root-Partitionen, um sicherzustellen, dass die wesentlichen Betriebssystemkomponenten vor der Bereitstellung nicht geändert

Um einen Vorlagen Datenträger zu erstellen, müssen Sie zunächst eine reguläre (nicht genehmigte) VM erstellen, die Sie als Basis Image für künftige abgeschirmte VMS vorbereiten.
Die von Ihnen installierte Software und Konfigurationsänderungen, die Sie an diesem virtuellen Computer vornehmen, gelten für alle abgeschirmten VMS, die auf dieser Vorlage erstellt werden.
Diese Schritte führen Sie durch die Mindestanforderungen für eine Linux-VM, die für die Vorlagen-atisierung bereit steht.

> [!NOTE]
> Die Linux-Datenträger Verschlüsselung wird konfiguriert, wenn der Datenträger partitioniert ist.
> Dies bedeutet, dass Sie einen neuen virtuellen Computer erstellen müssen, der mithilfe von dm-crypt vorverschlüsselt ist, um einen Linux-Vorlagen Datenträger für geschützte VM zu erstellen


1.  Stellen Sie auf dem Virtualisierungsserver sicher, dass Hyper-v und die Hyper-v-Unterstützung für den Host-Überwachungsdienst installiert werden, indem Sie die folgenden Befehle in einer PowerShell-Konsole mit erhöhten

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  Laden Sie das ISO-Abbild von einer vertrauenswürdigen Quelle herunter, und speichern Sie es auf Ihrem Virtualisierungsserver oder auf einer Dateifreigabe, auf die der Virtualisierungsserver

3.  Installieren Sie auf dem Verwaltungs Computer, auf dem Windows Server Version 1709 ausgeführt wird, den geschützten VM-Remoteserver-Verwaltungstools, indem Sie den folgenden Befehl ausführen:

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  Öffnen Sie den **Hyper-V-Manager** auf dem Verwaltungs Computer, und stellen Sie eine Verbindung mit dem Virtualisierungsserver
    Klicken Sie hierzu auf "Verbindung mit Server herstellen...". Klicken Sie im Aktionsbereich oder mit der rechten Maustaste auf Hyper-V-Manager, und wählen Sie "Verbindung mit Server herstellen..." aus. Geben Sie den DNS-Namen für den Hyper-V-Server und ggf. die Anmelde Informationen an, die zum Herstellen einer Verbindung erforderlich sind.

5.  Konfigurieren Sie mit dem Hyper-V-Manager [einen externen Switch](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines) auf dem Virtualisierungsserver, damit die Linux-VM auf das Internet zugreifen kann, um Updates abzurufen.

6.  Erstellen Sie als nächstes einen neuen virtuellen Computer, auf dem das Linux-Betriebssystem installiert werden soll.
    Klicken Sie im Aktionsbereich auf **neu** > **virtueller Computer** , um den Assistenten zu beenden.
    Geben Sie einen anzeigen Amen für den virtuellen Computer an, z. b. "Pre--Vorlagen-Linux", und klicken Sie auf **weiter**.

7.  Wählen Sie auf der zweiten Seite des Assistenten **Generation 2** aus, um sicherzustellen, dass die VM mit einem UEFI-basierten firmwareprofil bereitgestellt wird.

8.  Vervollständigen Sie den Rest des Assistenten gemäß Ihren Einstellungen.
    Verwenden Sie für diese VM keinen differenzierenden Datenträger. für geschützte VM-Vorlagen Datenträger können keine differenzierenden Datenträger
    Verbinden Sie schließlich das ISO-Abbild, das Sie zuvor heruntergeladen haben, mit dem virtuellen DVD-Laufwerk für diese VM, damit Sie das Betriebssystem installieren können.

9.  Wählen Sie im Hyper-V-Manager den neu erstellten virtuellen Computer aus, und klicken Sie im Aktionsbereich auf **verbinden...** , um ihn an eine virtuelle Konsole der VM anzufügen.
    Klicken Sie im angezeigten Fenster auf **Start** , um den virtuellen Computer zu aktivieren.

10. Durchlaufen Sie den Setup Vorgang für die ausgewählte Linux-Distribution.
    Obwohl jede Linux-Distribution einen anderen Setup-Assistenten verwendet, müssen die folgenden Anforderungen für VMS erfüllt sein, die zu Linux-Vorlagen Datenträger für virtuelle Computer werden.

    - Der Datenträger muss mithilfe des GPT-Layouts (GUID-Partitionstabelle) partitioniert werden.
    - Die Stamm Partition muss mit dm-crypt verschlüsselt werden. Die Passphrase sollte auf **Passphrase** (nur Kleinbuchstaben) festgelegt werden. Diese Passphrase wird zufällig erstellt, und die Partition wird neu verschlüsselt, wenn eine abgeschirmte VM bereitgestellt wird.
    - Die Start Partition muss das **ext2** -Dateisystem verwenden.

11. Nachdem das Linux-Betriebssystem vollständig gestartet wurde und Sie sich angemeldet haben, wird empfohlen, den Linux-virtuellen Kernel und zugehörige Hyper-V-Integrations Dienst Pakete zu installieren.
    Außerdem sollten Sie einen SSH-Server oder ein anderes Remote Verwaltungs Tool installieren, um auf die VM zuzugreifen, nachdem Sie geschützt wurde.

    Führen Sie unter Ubuntu den folgenden Befehl aus, um diese Komponenten zu installieren:

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    Führen Sie unter RHEL stattdessen den folgenden Befehl aus:

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    Führen Sie unter SLES den folgenden Befehl aus:

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. Konfigurieren Sie das Linux-Betriebssystem wie gewünscht.
    Jede Software, die Sie installieren, Benutzerkonten, die Sie hinzufügen, und von Ihnen vorgenommene systemweiten Konfigurationsänderungen gelten für alle zukünftigen virtuellen Computer, die auf dieser Vorlagen Datenträger
    Vermeiden Sie, geheime oder unnötige Pakete auf dem Datenträger zu speichern.

13. Wenn Sie beabsichtigen, System Center Virtual Machine Manager für die Bereitstellung Ihrer VMS zu verwenden, installieren Sie den VMM-Gast-Agent, damit VMM das Betriebssystem während der VM-Bereitstellung spezialisiert.
    Die Spezialisierung ermöglicht die sichere Einrichtung jeder VM mit unterschiedlichen Benutzern und SSH-Schlüsseln, Netzwerkkonfigurationen und benutzerdefinierten Einrichtungs Schritten.
    Erfahren Sie, wie Sie [den VMM-Gast-Agent](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent) in der VMM-Dokumentation abrufen und installieren.

14. [Fügen Sie als nächstes das Microsoft Linux-Softwarerepository Ihrem Paket-Manager hinzu](../../administration/linux-package-repository-for-microsoft-software.md).

15. Installieren Sie mithilfe des Paket-Managers das lsvmtools-Paket, das die Linux-Shim für abgeschirmte VM-Bootloader, Bereitstellungs Komponenten und das Tool zur Datenträger Vorbereitung enthält.

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. Wenn Sie die Anpassung des Linux-Betriebssystems abgeschlossen haben, suchen Sie das Installationsprogramm lsvmprep auf dem System, und führen Sie es aus.
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. Fahren Sie Ihren virtuellen Computer herunter.

16. Wenn Sie Prüfpunkte Ihres virtuellen Computers (einschließlich automatischer Prüfpunkte, die von Hyper-V mit dem Windows 10 Fall Creators Update erstellt wurden) vorgenommen haben, achten Sie darauf, dass Sie Sie löschen, bevor Sie fortfahren.
    Prüfpunkte erstellen differenzierende Datenträger (. avhdx), die vom Vorlagen-Assistenten für Vorlagen nicht unterstützt werden.
    
    Um Prüfpunkte zu löschen, öffnen Sie den **Hyper-V-Manager**, wählen Sie den virtuellen Computer aus, **Klicken Sie mit**der rechten Maustaste auf den obersten Prüfpunkt im Bereich Prüfpunkte, und klicken Sie dann auf Prüf Punkt

    ![Löschen Sie alle Prüfpunkte für Ihre Vorlagen-VM im Hyper-V-Manager.](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>Schützen des Vorlagen Datenträgers

Der virtuelle Computer, den Sie im vorherigen Abschnitt vorbereitet haben, ist fast bereit für die Verwendung als Vorlage für abgeschirmte Linux-VM-Vorlagen.
Der letzte Schritt besteht darin, den Datenträger mit dem datenträgerdatenträger-Assistenten auszuführen, der den aktuellen Zustand der Stamm-und Start Partitionen Hashs und digital signiert.
Der Hash und die digitale Signatur werden überprüft, wenn eine abgeschirmte VM bereitgestellt wird, um sicherzustellen, dass keine nicht autorisierten Änderungen an den beiden Partitionen zwischen der Vorlagen Erstellung und der Bereitstellung vorgenommen wurden.

### <a name="obtain-a-certificate-to-sign-the-disk"></a>Abrufen eines Zertifikats zum Signieren des Datenträgers

Um die Datenträger Messungen Digital zu signieren, müssen Sie auf dem Computer, auf dem Sie den Vorlagen Datenträger-Assistenten ausführen werden, ein Zertifikat abrufen.
Das Zertifikat muss die folgenden Anforderungen erfüllen:

Zertifikat Eigenschaft | Erforderlicher Wert
---------------------|---------------
Schlüssel Algorithmus | RSA
Minimale Schlüsselgröße | 2048 Bits
Signatur Algorithmus | SHA256 (empfohlen)
Schlüsselverwendung | Digitale Signatur

Details zu diesem Zertifikat werden den Mandanten angezeigt, wenn Sie Ihre geschützten Datendateien erstellen und die Datenträger autorisierst, denen Sie vertrauen.
Daher ist es wichtig, dass Sie dieses Zertifikat von einer Zertifizierungsstelle abrufen, die von Ihnen und ihren Mandanten als nicht vertrauenswürdig eingestuft wird.
In Unternehmens Szenarios, in denen Sie sowohl der Host als auch der Mandant sind, sollten Sie dieses Zertifikat von Ihrer Unternehmens Zertifizierungsstelle ausgeben.
Schützen Sie dieses Zertifikat sorgfältig, da jeder, der dieses Zertifikat besitzt, neue Vorlagen Datenträger erstellen kann, die mit dem authentischen Datenträger vertrauenswürdig sind.

In einer Testumgebung können Sie mit dem folgenden PowerShell-Befehl ein selbst signiertes Zertifikat erstellen:

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>Verarbeiten des Datenträgers mit dem Datenträger-Assistenten-Cmdlet

Kopieren Sie den Vorlagen Datenträger und das Zertifikat auf einen Computer unter Windows Server, Version 1709, und führen Sie dann die folgenden Befehle aus, um den Signatur Prozess zu initiieren
Die vhdx-Datei, die Sie für den Parameter "`-Path`" bereitstellen, wird mit dem aktualisierten Vorlagen Datenträger überschrieben. Achten Sie daher darauf, dass Sie vor dem Ausführen des Befehls

> [!IMPORTANT]
> Der Remoteserver-Verwaltungstools, der unter Windows Server 2016 oder Windows 10 verfügbar ist, kann nicht verwendet werden, um einen Linux-Vorlagen Datenträger für geschützte
> Verwenden Sie das Cmdlet " [Protect-templatedisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps) ", das unter Windows Server, Version 1709, verfügbar ist, oder das Remoteserver-Verwaltungstools, das unter Windows Server 2019 verfügbar ist, um einen Linux-Vorlagen Datenträger

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

Der Vorlagen Datenträger kann jetzt zum Bereitstellen von abgeschirmten Linux-VMs verwendet werden.
Wenn Sie System Center Virtual Machine Manager zum Bereitstellen Ihrer VM verwenden, können Sie jetzt die vhdx-Datei in die VMM-Bibliothek kopieren.

Möglicherweise möchten Sie auch den volumesignaturkatalog aus der vhdx-Datei extrahieren.
Diese Datei wird verwendet, um Informationen über das Signaturzertifikat, den Datenträger Namen und die Version für die VM-Besitzer bereitzustellen, die Ihre Vorlage verwenden möchten.
Sie müssen diese Datei in den Assistenten für die Schutz Datendatei importieren, um Sie zu autorisieren, den Vorlagen Autor im Besitz des Signatur Zertifikats, um diesen und zukünftige Vorlagen Datenträger zu erstellen.

Führen Sie den folgenden Befehl in PowerShell aus, um den volumesignaturkatalog zu extrahieren:

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
