---
title: Verwenden von direkte Speicherplätze auf einem virtuellen Computer
ms.prod: windows-server
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: Bereitstellen von direkte Speicherplätze in einem Gast Cluster für virtuelle Maschinen, z. b. in Microsoft Azure.
ms.localizationpriority: medium
ms.openlocfilehash: 74b1b90a780a0b238a356e942f8348e2a483d94a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856113"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>Verwenden von direkte Speicherplätze in Clustern virtueller Gastcomputer

> Gilt für: Windows Server 2019, Windows Server 2016

Sie können direkte Speicherplätze auf einem Cluster physischer Server oder auf Gast Clustern für virtuelle Maschinen bereitstellen, wie in diesem Thema erläutert. Diese Art der Bereitstellung bietet virtuellen freigegebenen Speicher über eine Gruppe von virtuellen Computern, die auf einem privaten oder Public Cloud basieren, damit Anwendungslösungen mit hoher Verfügbarkeit verwendet werden können, um die Verfügbarkeit von Anwendungen zu erhöhen.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Bereitstellen in Azure IaaS-VM-Gast Clustern

[Azure-Vorlagen](https://github.com/robotechredmond/301-storage-spaces-direct-md) wurden veröffentlicht, um die Komplexität zu verringern, bewährte Methoden und die Geschwindigkeit Ihrer direkte Speicherplätze Bereitstellungen auf einem virtuellen Azure-IaaS-Computer zu konfigurieren. Dies ist die empfohlene Lösung für die Bereitstellung in Azure.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>Voraussetzungen

Beim Bereitstellen von direkte Speicherplätze in einer virtualisierten Umgebung gelten die folgenden Überlegungen.
       
>        !TIP]
>        zure templates will automatically configure the below considerations for you and are the recommended solution when deploying in Azure IaaS VMs.

-   Mindestens 2 Knoten und maximal 3 Knoten

-   zwei Knoten Bereitstellungen müssen einen Zeugen konfigurieren (cloudzeuge oder Dateifreigabe Zeuge)

-   bei bereit Stellungen mit 3 Knoten kann ein Knoten Ausfall und der Verlust von mindestens einem Datenträger auf einem anderen Knoten toleriert werden.  Wenn zwei Knoten heruntergefahren werden, werden die virtuellen Datenträger offline geschaltet, bis einer der Knoten zurückgibt.  

-   Konfigurieren der virtuellen Computer, die über Fehler Domänen hinweg bereitgestellt werden sollen

    -   Azure – Verfügbarkeits Gruppe konfigurieren

    -   Hyper-V – Konfigurieren von AntiAffinityClassNames auf den virtuellen Computern, um die VMs Knoten übergreifend zu trennen

    -   VMware – konfigurieren Sie die antiaffinitäts Regel für VM-VM, indem Sie eine DRS-Regel vom Typ "separate Virtual Machines" erstellen, um die VMs zwischen ESX-Hosts zu trennen. Für Datenträger, die mit direkte Speicherplätze verwendet werden sollen, sollte der Adapter "paravirtual SCSI" (pvscsi) verwendet werden. Informationen zur pvscsi-Unterstützung mit Windows Server finden Sie unter https://kb.vmware.com/s/article/1010398.

-   Nutzen von geringer Latenz/Hochleistungsspeicher: verwaltete Azure Storage Premium-Datenträger sind erforderlich

-   Bereitstellen eines flachen Speicher Entwurfs ohne konfigurierte cachinggeräte

-   Mindestens zwei virtuelle Datenträger, die jedem virtuellen Computer angezeigt werden (VHD/vhdx/VMDK)

    Diese Zahl unterscheidet sich von Bare-Metal-bereit Stellungen, da die virtuellen Datenträger als Dateien implementiert werden können, die nicht anfällig für physische Fehler sind.

-   Deaktivieren Sie die automatische Laufwerk Ersetzung "apab"-lities im Integritätsdienst, indem Sie das folgende PowerShell-Cmdlet ausführen:

    ```powershell
          Get-storagesubsystem clus* | set-storagehealthsetting -name "System.Storage.PhysicalDisk.AutoReplace.Enabled" -value "False"
          ```

-   To give greater resiliency to possible VHD / VHDX / VMDK storage latency in guest clusters, increase the Storage Spaces I/O timeout value:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    The decimal equivalent of Hexadecimal 7530 is 30000, which is 30 seconds. Note that the default value is 1770 Hexadecimal, or 6000 Decimal, which is 6 seconds.

## Not supported

-   Host level virtual disk snapshot/restore

    Instead use traditional guest level backup solutions to backup and restore the data on the Storage Spaces Direct volumes.

-   Host level virtual disk size change

    The virtual disks exposed through the virtual machine must retain the same size and characteristics. Adding more capacity to the storage pool can be accomplished by adding more virtual disks to each of the virtual machines and adding them to the pool. It's highly recommended to use virtual disks of the same size and characteristics as the current virtual disks.

## See also

[Additional Azure Iaas VM templates for deploying Storage Spaces Direct, videos, and step-by-step guides](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

[Additional Storage Spaces Direct Overview](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
""""""''''                                                                                                                                                                        """"""''''                                                                                                                                                                        