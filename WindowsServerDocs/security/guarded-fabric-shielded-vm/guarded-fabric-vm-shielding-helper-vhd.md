---
title: 'Abgeschirmte VMS: Vorbereiten einer VHD für ein VM-Schutz Hilfsprogramm'
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 2c6a74b3dd18465534a662e6c1afa37ac197aca6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943990"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>Abgeschirmte VMS: Vorbereiten einer VHD für ein VM-Schutz Hilfsprogramm

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

> [!IMPORTANT]
> Bevor Sie mit diesen Verfahren beginnen, stellen Sie sicher, dass Sie das neueste kumulative Update für Windows Server 2016 installiert haben oder die neuesten Windows 10- [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=45520)verwenden. Andernfalls funktionieren die Prozeduren nicht.

In diesem Abschnitt werden die Schritte beschrieben, die von einem hostingdienstanbieter ausgeführt werden, um die Unterstützung für die Umstellung vorhandener virtueller

Informationen dazu, wie sich dieses Thema in den Gesamtprozess der Bereitstellung von abgeschirmten VMS einfügt, finden Sie unter [Hosten von Dienstanbietern Konfigurationsschritte für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="which-vms-can-be-shielded"></a>Welche VMs können geschützt werden?

Der Schutz Vorgang für vorhandene VMS ist nur für VMS verfügbar, die die folgenden Voraussetzungen erfüllen:

- Das Gast Betriebssystem ist Windows Server 2012, 2012 R2, 2016 oder eine halbjährliche Kanal Version. Vorhandene virtuelle Linux-Computer können nicht in abgeschirmte VMS konvertiert werden.
- Der virtuelle Computer ist eine VM der Generation 2 (UEFI-Firmware).
- Der virtuelle Computer verwendet keine differenzierenden Datenträger für das Betriebssystem Volume.

## <a name="prepare-helper-vhd"></a>Vorbereiten der VHD

1.  Erstellen Sie auf einem Computer mit Hyper-V und dem Remoteserver-Verwaltungstools Feature **abgeschirmte VM-Tools** installiert einen neuen virtuellen Computer der Generation 2 mit einer leeren vhdx-Datei, und installieren Sie Windows Server 2016 mithilfe der ISO-Installationsmedien von Windows Server. Diese VM sollte nicht geschützt werden und muss Server Core oder Server mit Desktop Darstellung ausführen.

    > [!IMPORTANT]
    > Die VHD für das VM-Schutz Hilfsprogramm **darf nicht** mit den Vorlagen Datenträgern verknüpft sein, die Sie im [hostingdienstanbieter](guarded-fabric-create-a-shielded-vm-template.md)erstellt haben. Wenn Sie einen Vorlagen Datenträger wieder verwenden, wird während des Schutz Vorgangs ein Datenträger Signatur Konflikt festgestellt, da beide Datenträger denselben GPT-Datenträger Bezeichner aufweisen. Sie können dies vermeiden, indem Sie eine neue (leere) VHD erstellen und Windows Server 2016 mithilfe der ISO-Installationsmedien auf diesem Server installieren.

2.  Starten Sie den virtuellen Computer, führen Sie alle Setup Schritte aus, und melden Sie sich beim Desktop an. Nachdem Sie überprüft haben, dass sich die VM in einem funktionierenden Zustand befindet, fahren Sie den virtuellen Computer herunter.

3.  Führen Sie in einem Windows PowerShell-Fenster mit erhöhten Rechten den folgenden Befehl aus, um die zuvor erstellte vhdx-Datei als VM-schutzhilfshilf-Daten Träger vorzubereiten. Aktualisieren Sie den Pfad mit dem richtigen Pfad für Ihre Umgebung.

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  Nachdem der Befehl erfolgreich abgeschlossen wurde, kopieren Sie die vhdx-Datei in die VMM-Bibliotheks Freigabe. Starten Sie den virtuellen Computer **nicht** erneut aus Schritt 1. Dadurch wird der hilfsprogrammdatenträger beschädigt.

5.  Nun können Sie den virtuellen Computer aus Schritt 1 in Hyper-V löschen.

## <a name="configure-vmm-host-guardian-server-settings"></a>VMM-Host-Überwachungs Server Einstellungen konfigurieren

Öffnen Sie in der VMM-Konsole den Bereich Einstellungen, und wählen Sie dann unter **Allgemein**die Einstellungen des Überwachungs **Diensts** . Am unteren Rand dieses Fensters befindet sich ein Feld, in dem Sie den Speicherort der Hilfs-VHD konfigurieren können. Verwenden Sie die Schaltfläche Durchsuchen, um die VHD aus der Bibliotheks Freigabe auszuwählen. Wenn der Datenträger in der Freigabe nicht angezeigt wird, müssen Sie die Bibliothek in VMM möglicherweise manuell aktualisieren, damit Sie angezeigt wird.

![VMM-Einstellungen für den Host-Überwachungsdienst](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="additional-references"></a>Weitere Verweise

- [Geschützte Hosts und abgeschirmte VMs: Konfigurationsschritte für Hosting-Anbieter](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
