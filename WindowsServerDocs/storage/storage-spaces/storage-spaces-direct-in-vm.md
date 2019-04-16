---
title: Mithilfe von "direkte Speicherplätze" auf einem virtuellen Computer
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: Informationen zum Bereitstellen von direkte Speicherplätze in einem virtuellen Computer Gast-Cluster – z. B. in Microsoft Azure.
ms.localizationpriority: medium
ms.openlocfilehash: a741475d09ab7f7ab29f158ef55378ca9a37beac
ms.sourcegitcommit: 52883945fd6e6bb5c24bd81944ca4bc0c5e6a216
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2018
ms.locfileid: "8964612"
---
# Die Verwendung von "direkte Speicherplätze" in gastcluster für virtuelle Computer

> Gilt für: WindowsServer 2019, WindowsServer 2016

Sie können den direkten Speicherplätzen auf ein Cluster mit physischen Servern oder virtuellen Computer gastcluster wie in diesem Thema erläutert bereitstellen. Diese Art der Bereitstellung bietet virtuellen freigegebenen Speicher über eine Reihe von VMs auf eine private oder öffentliche Cloud, damit die Anwendung hohe Verfügbarkeit Lösungen zum Erhöhen der Verfügbarkeit von Anwendungen verwendet werden können.

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## Bereitstellen von in Azure Iaas-VM-gastcluster

[Azure-Vorlagen](https://github.com/robotechredmond/301-storage-spaces-direct-md) wurden veröffentlichten Verringerung der Komplexität, konfigurieren Sie am besten Methoden und Geschwindigkeit des von "direkte Speicherplätze"-Bereitstellungen in einer Azure Iaas-VM. Dies ist die empfohlene Lösung für die Bereitstellung von in Azure.

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## Anforderungen

Folgendes gilt, wenn Sie "direkte Speicherplätze" in einer virtualisierten Umgebung bereitstellen.

> [!TIP]
> Azure Vorlagen werden automatisch konfiguriert, die folgenden Aspekte und sind die empfohlene Lösung, bei der Bereitstellung in Azure IaaS-VMs.

-   Mindestens 2 Knoten und bis zu 3 Knoten

-   2-Knoten-Bereitstellungen müssen einen Zeugen (Cloudzeugen oder Dateifreigabezeugen) konfigurieren.

-   3-Knoten-Bereitstellungen können 1 Knoten nach unten und den Verlust von 1 oder mehr Datenträger auf einen anderen Knoten toleriert.  Wenn 2 Knoten Herunterfahren sind dann die virtueller Datenträger wir offline erst, einen Knoten zurückgibt.  

-   Konfigurieren der virtuellen Computer über Fehlerdomänen bereitgestellt werden

    -   Azure – Verfügbarkeit konfigurieren

    -   Hyper-V – konfigurieren AntiAffinityClassNames auf die virtuellen Computer, die virtuellen Computer auf die Knoten zu trennen.

    -   VMware – Konfigurieren von VM-VM Anti-Affinität Regel erstellen Sie eine DRS Rule vom Typ "separater virtueller Computer", die VMs auf ESX-Hosts zu trennen. Datenträger, die für die Verwendung mit "direkte Speicherplätze" angezeigt, sollte der Paravirtual SCSI (PVSCSI)-Adapter verwenden. PVSCSI-Unterstützung in Windows Server finden Sie in https://kb.vmware.com/s/article/1010398.

-   Nutzen Sie geringer Latenz / mit hoher Leistung Speicher - Azure-Premium-Speicher verwaltet Datenträger sind erforderlich

-   Bereitstellen eines Speicherentwurfs flache mit keine Geräte für das Zwischenspeichern konfiguriert

-   Mindestens 2 virtuelle Datenträger, die von jedem virtuellen Computer angezeigt (VHD / VHDX / VMDK)

    Diese Zahl ist anders als bare-Metal-Bereitstellungen, da die virtueller Datenträger als Dateien implementiert werden können, die keine physischen Fehler anfällig sind.

-   Deaktivieren Sie die automatische Laufwerk Ersatz-Funktionen in der Zustandsdienst durch Ausführen des folgenden PowerShell-Cmdlets:

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   Nicht unterstützt: Hosten auf virtuellen Datenträger Snapshot und Wiederherstellung

    Stattdessen verwenden Sie herkömmliche Gast-Level-backup-Lösungen zum Sichern und Wiederherstellen von Daten auf Volumes "direkte Speicherplätze".

-   Mögliche VHD größer resilienz erteilen / VHDX / VMDK Speicher Latenz in gastcluster, erhöhen Sie den Speicher Leerzeichen e/a:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    Decimal entspricht hexadezimale 7530 30000, d. h. 30 Sekunden. Beachten Sie, dass der Standardwert 1770 hexadezimalen oder 6000 Decimal, 6 Sekunden handelt.

## Weitere Informationen:

[Weitere Azure-VM Iaas-Vorlagen für die Bereitstellung von "direkte Speicherplätze", Videos und Leitfäden](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/).

[Weitere "direkte Speicherplätze" Übersicht über die] (https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
