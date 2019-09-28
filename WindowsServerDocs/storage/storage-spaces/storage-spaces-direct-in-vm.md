---
title: Verwenden von direkte Speicherplätze auf einem virtuellen Computer
ms.prod: windows-server
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: Bereitstellen von direkte Speicherplätze in einem Gast Cluster für virtuelle Maschinen, z. b. in Microsoft Azure.
ms.localizationpriority: medium
ms.openlocfilehash: ab0ce792c5a948e763a48493a78ccdac7a6fe74c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366048"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>Verwenden von direkte Speicherplätze in Clustern virtueller Gastcomputer

> Gilt für: Windows Server 2019, Windows Server 2016

Sie können direkte Speicherplätze auf einem Cluster physischer Server oder auf Gast Clustern für virtuelle Maschinen bereitstellen, wie in diesem Thema erläutert. Diese Art der Bereitstellung bietet virtuellen freigegebenen Speicher über eine Gruppe von virtuellen Computern, die auf einem privaten oder Public Cloud basieren, damit Anwendungslösungen mit hoher Verfügbarkeit verwendet werden können, um die Verfügbarkeit von Anwendungen zu erhöhen.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Bereitstellen in Azure IaaS-VM-Gast Clustern

[Azure-Vorlagen](https://github.com/robotechredmond/301-storage-spaces-direct-md) wurden veröffentlicht, um die Komplexität zu verringern, bewährte Methoden und die Geschwindigkeit Ihrer direkte Speicherplätze Bereitstellungen auf einem virtuellen Azure-IaaS-Computer zu konfigurieren. Dies ist die empfohlene Lösung für die Bereitstellung in Azure.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>Anforderungen

Beim Bereitstellen von direkte Speicherplätze in einer virtualisierten Umgebung gelten die folgenden Überlegungen.

> [!TIP]
> Azure-Vorlagen konfigurieren automatisch die folgenden Überlegungen für Sie und sind bei der Bereitstellung auf Azure-IaaS-VMS empfehlenswert.

-   Mindestens 2 Knoten und maximal 3 Knoten

-   zwei Knoten Bereitstellungen müssen einen Zeugen konfigurieren (cloudzeuge oder Dateifreigabe Zeuge)

-   bei bereit Stellungen mit 3 Knoten kann ein Knoten Ausfall und der Verlust von mindestens einem Datenträger auf einem anderen Knoten toleriert werden.  Wenn zwei Knoten heruntergefahren werden, werden die virtuellen Datenträger offline geschaltet, bis einer der Knoten zurückgibt.  

-   Konfigurieren der virtuellen Computer, die über Fehler Domänen hinweg bereitgestellt werden sollen

    -   Azure – Verfügbarkeits Gruppe konfigurieren

    -   Hyper-V – Konfigurieren von AntiAffinityClassNames auf den virtuellen Computern, um die VMs Knoten übergreifend zu trennen

    -   VMware – konfigurieren Sie die antiaffinitäts Regel für VM-VM, indem Sie eine DRS-Regel vom Typ "separate Virtual Machines" erstellen, um die VMs zwischen ESX-Hosts zu trennen. Für Datenträger, die mit direkte Speicherplätze verwendet werden sollen, sollte der Adapter "paravirtual SCSI" (pvscsi) verwendet werden. Informationen zur pvscsi-Unterstützung mit Windows Server finden Sie https://kb.vmware.com/s/article/1010398.

-   Nutzen von geringer Latenz/Hochleistungsspeicher: verwaltete Azure Storage Premium-Datenträger sind erforderlich

-   Bereitstellen eines flachen Speicher Entwurfs ohne konfigurierte cachinggeräte

-   Mindestens zwei virtuelle Datenträger, die jedem virtuellen Computer angezeigt werden (VHD/vhdx/VMDK)

    Diese Zahl unterscheidet sich von Bare-Metal-bereit Stellungen, da die virtuellen Datenträger als Dateien implementiert werden können, die nicht anfällig für physische Fehler sind.

-   Deaktivieren Sie die automatischen Laufwerk Ersetzungs Funktionen in der Integritätsdienst, indem Sie das folgende PowerShell-Cmdlet ausführen:

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   Nicht unterstützt: Momentaufnahme/Wiederherstellung virtueller Datenträger auf Hostebene

    Verwenden Sie stattdessen herkömmliche Sicherungslösungen auf Gast Ebene, um die Daten auf den direkte Speicherplätze Volumes zu sichern und wiederherzustellen.

-   Erhöhen Sie den Wert für den e/a-Timeout Wert für Speicherplätze, um der möglichen Speicherlatenz von VHD/vhdx/VMDK in Gast Clustern eine höhere Resilienz zu ermöglichen:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    Das Dezimaltrennzeichen von hexadezimal 7530 ist 30000 (30 Sekunden). Beachten Sie, dass der Standardwert 1770 hexadezimal ist, oder 6000 Decimal, d. h. 6 Sekunden.

## <a name="see-also"></a>Siehe auch

[Weitere Azure-IaaS-VM-Vorlagen zum Bereitstellen von direkte Speicherplätze, Videos und Schritt-für-Schritt-Anleitungen](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

[Weitere direkte Speicherplätze Übersicht](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
