---
title: Mithilfe von "direkte Speicherplätze" in einem virtuellen Computer
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: "\"Direkte Speicherplätze\" Bereitstellen in einem VM-gastcluster – z. B. in Microsoft Azure"
ms.localizationpriority: medium
ms.openlocfilehash: a741475d09ab7f7ab29f158ef55378ca9a37beac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841021"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>Mithilfe von "direkte Speicherplätze" in VM-gastclustern

> Gilt für: Windows Server 2019, Windows Server 2016

Sie können "direkte Speicherplätze" in einem Cluster von physischen Servern oder auf der VM-gastclustern wie in diesem Thema beschrieben bereitstellen. Diese Art der Bereitstellung bietet virtuellen freigegebenen Speicher für eine Gruppe von VMs über eine private oder öffentliche Cloud, so, dass hochverfügbarkeitslösungen Anwendung zur Steigerung der Verfügbarkeit von Anwendungen verwendet werden können.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Bereitstellen in Azure IaaS-VM-gastclustern

[Azure-Vorlagen](https://github.com/robotechredmond/301-storage-spaces-direct-md) wurden veröffentlichten Verringerung der Komplexität, konfigurieren Sie die besten Methoden und die Geschwindigkeit Ihrer "direkte Speicherplätze"-Bereitstellungen in einer Azure-IaaS-VM. Dies ist die empfohlene Lösung für die Bereitstellung in Azure.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>Anforderungen

Die folgenden Überlegungen gelten, wenn Sie "direkte Speicherplätze" in einer virtualisierten Umgebung bereitstellen.

> [!TIP]
> Azure-Vorlagen konfiguriert automatisch die folgenden Überlegungen, die für Sie und sind die empfohlene Lösung, bei der Bereitstellung in Azure IaaS-VMs.

-   Mindestens 2 Knoten und maximal 3 Knoten

-   Bereitstellungen mit 2 Knoten müssen ein Zeuge (Cloudzeugen oder File Share Witness) konfigurieren.

-   3-Knoten-Bereitstellungen können es sich um 1 Knoten nach unten und zum Verlust von 1 oder mehrere Datenträger auf einem anderen Knoten tolerieren.  Wenn 2 Knoten heruntergefahren sind. Klicken Sie dann die virtuellen Datenträger wird offline bis einer der Knoten zurückgegeben.  

-   Konfigurieren der virtuellen Computer über Fehlerdomänen hinweg bereitgestellt werden

    -   Azure – Konfigurieren der Verfügbarkeitsgruppe

    -   Hyper-V – konfigurieren "AntiAffinityClassNames" auf den virtuellen Computern, um die virtuellen Computer über Knoten hinweg zu trennen.

    -   VMware-VM-VM-Antiaffinität Konfigurieren der Regel durch das Erstellen einer DRS Rule vom Typ "Separate virtuelle Computer" um die virtuellen Computer auf ESX-Hosts zu trennen. Der Datenträger angezeigt wird, für den Adapter Paravirtual-SCSI (verwenden) verwenden, die mit "direkte Speicherplätze" verwendet werden soll. -Unterstützung in Windows Server verwenden, finden Sie in https://kb.vmware.com/s/article/1010398.

-   Mit geringer Latenz nutzen / verwalteten Speicher für hohe Leistung – Azure Storage Premium-Datenträger erforderlich sind

-   Bereitstellen Sie einen flache Speicherentwurf mit keine konfigurierten Zwischenspeicherung Geräte

-   Mindestens 2 virtuelle Datenträger, die für jeden virtuellen Computer angezeigt (VHD / VHDX / VMDK-Datei)

    Diese Zahl ist anders als bare-Metal-Bereitstellungen, da die virtuellen Datenträger als Dateien, die anfällig für Ausfälle von physischen nicht implementiert werden können.

-   Deaktivieren Sie die automatische Laufwerk Ersatz-Funktionen in den Health-Dienst durch Ausführen des folgenden PowerShell-Cmdlets:

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   Nicht unterstützt: Hosten Sie auf Datenträger/momentaufnahmenwiederherstellung

    Stattdessen verwenden Sie herkömmliche Gast auf sicherungslösungen, Sichern und Wiederherstellen der Daten auf den "direkte Speicherplätze"-Volumes.

-   Gerne größere resilienz zu möglichen VHD / VHDX / VMDK-Speicherlatenz in gastclustern, erhöhen Sie den Storage Spaces-e/a-Timeout-Wert:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    Die dezimale Entsprechung des hexadezimal 7530 beträgt 30000, d. h. 30 Sekunden. Beachten Sie, dass der Standardwert 1770 Hexadezimal- oder 6000 Dezimal ist, 6 Sekunden beträgt.

## <a name="see-also"></a>Siehe auch

[Zusätzliche Azure-IaaS-VM-Vorlagen für die Bereitstellung von "direkte Speicherplätze", Videos und Anleitungen](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/).

[Zusätzliche "direkte Speicherplätze" Overview] (https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
