---
title: 'Abgeschirmte VMs: Vorbereiten eines virtuellen Computers, die VHD für Schutzhilfsprogramm'
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8e14cdeed435f23f28ca514e232fbcfa6220fc74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887721"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>Abgeschirmte VMs: Vorbereiten eines virtuellen Computers, die VHD für Schutzhilfsprogramm

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

<!-- This comment creates a break between the Applies To above and the Important note below. -->

> [!IMPORTANT]
> Bevor Sie diese Schritte ausführen, stellen Sie sicher, dass Sie das neueste kumulative Update für Windows Server 2016 installiert haben, oder das neueste Windows 10 verwenden- [Remoteserver-Verwaltungstools](https://www.microsoft.com/en-us/download/details.aspx?id=45520). Andernfalls funktioniert die Prozeduren nicht. 

Dieser Abschnitt enthält Schritte, die vom hosting-Anbieter um Unterstützung für die Konvertierung vorhandener VMs in abgeschirmte VMs zu aktivieren.

Um zu verstehen, wie in diesem Thema in den gesamten Vorgang der Bereitstellung von abgeschirmten VMs passt, finden Sie unter [Service Provider-Konfigurationsschritte für das Hosten von überwachten Hosts und abgeschirmte VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="which-vms-can-be-shielded"></a>Die VMs können geschützt werden?

Des geschützten Prozesses für vorhandene virtuelle Computer ist nur verfügbar, für VMs, die die folgenden Voraussetzungen erfüllen:

- Das Gastbetriebssystem ist Windows Server 2012, 2012 R2, 2016 oder einem halbjährlicher Kanal-Version. Vorhandene virtuelle Linux-Computer kann nicht in abgeschirmte VMs konvertiert werden.
- Der virtuelle Computer ist eine Generation 2 VM (UEFI-Firmware)
- Differenzierende Datenträger ist für die BS-Volume des virtuellen Computers nicht verwendet.

## <a name="prepare-helper-vhd"></a>Hilfsprogramm-VHD vorbereiten

1.  Auf einem Computer mit Hyper-V und das Feature der Remoteserver-Verwaltungstools **Tools für geschützte VMs** installiert haben, erstellen Sie eine neue Generation 2 VM mit einem leeren VHDX und installieren Sie Windows Server 2016, mit der ISO-Datei von Windows Server-Installation Medien. Dieser virtuelle Computer nicht geschützt werden und muss, werden die Server Core oder Server mit Desktopdarstellung ausführen.

    > [!IMPORTANT]
    > Die VM VHD für das Schutzhilfsprogramm **darf nicht** verknüpft werden kann, die im erstellten vorlagedatenträger [Hosting-Service-Anbieter erstellt die Vorlage für eine abgeschirmte VM](guarded-fabric-create-a-shielded-vm-template.md). Wenn Sie einen vorlagendatenträger erneut verwenden, fallen ein Datenträger Signatur Konflikt während des geschützten Prozesses da beide Datenträger auf die gleiche GPT-Datenträger-ID zugreifen können. Sie können dies vermeiden, erstellen eine neue (leere) virtuelle Festplatte, und installieren Windows Server 2016 auf dem ISO-Installationsmedium verwenden.

2.  Starten Sie die VM, Setupschritte ausführen, und melden Sie sich bei dem Desktop. Nachdem Sie, dass der virtuelle Computer in einem lauffähigen Zustand ist überprüft haben, müssen Sie den virtuellen Computer herunterfahren.

3.  Führen Sie in einer Windows PowerShell-Fenster mit erhöhten Rechten den folgenden Befehl aus, um einen Datenträger für virtuelle Computer das schutzhilfsprogramm werden zuvor erstellte VHDX vorbereiten. Aktualisieren Sie den Pfad durch den korrekten Pfad für Ihre Umgebung.

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  Nachdem der Befehl erfolgreich abgeschlossen wurde, kopieren Sie die VHDX in Ihrer VMM-Bibliotheksfreigabe aus. **Nicht** starten Sie den virtuellen Computer aus Schritt 1. Auf diese Weise wird der Datenträger beschädigt.

5.  Sie können nun den virtuellen Computer aus Schritt 1 unter Hyper-V löschen.

## <a name="configure-vmm-host-guardian-server-settings"></a>Konfigurieren der VMM-Host-Überwachungsdienst-Server-Einstellungen

Öffnen Sie in der VMM-Konsole den Bereich "abfrageeinstellungen" und dann **Einstellungen für Host-Überwachungsdienst** unter **allgemeine**. Am unteren Rand dieses Fensters gibt es ein Feld so konfigurieren Sie den Speicherort des Hilfsprogramm-VHD. Verwenden Sie die Schaltfläche zum Durchsuchen, um die virtuelle Festplatte aus der Bibliotheksfreigabe auszuwählen. Wenn Sie Ihre Datenträger in die Freigabe nicht angezeigt werden, müssen Sie manuell aktualisieren, die Bibliothek im VMM, damit sie angezeigt werden.

![VMM - Einstellungen für Host-Überwachungsdienst](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="see-also"></a>Siehe auch

- [Hosten von Service Provider-Konfigurationsschritte für die überwachten Hosts und abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
