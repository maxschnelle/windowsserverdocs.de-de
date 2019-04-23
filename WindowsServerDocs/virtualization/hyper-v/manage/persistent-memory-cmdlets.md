---
title: Cmdlets zum Konfigurieren von Geräten von persistenten Speicher für Hyper-V-VMs
description: Konfigurieren Sie Geräte von persistenten Speicher für Hyper-V-VMs
ms.prod: windows-server-threshold
ms.service: na
manager: jasgroce
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: fd1b04ce74f0b8d490529d2a7f65091f5847d0f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878181"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Cmdlets zum Konfigurieren von Geräten von persistenten Speicher für Hyper-V-VMs

>Gilt für: Windows Server 2019

In diesem Artikel werden Informationen zum Konfigurieren von Hyper-V-VMs mit persistenten Speicher (auch bekannt als speicherklassenspeicher oder NVDIMM) Systemadministratoren und IT-Experten bietet. JDEC-kompatible NVDIMM-N-persistenten Speicher-Geräte in Windows Server 2016 und Windows 10 unterstützt werden und bieten auf Byteebene auf sehr niedriger Latenz nicht flüchtigen Geräte. VM persistenten Speicher in Windows Server-2019 unterstützt. 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>Erstellen eines persistenten Speicher-Geräts für einen virtuellen Computer

Verwenden der **[New-VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** Cmdlet, um ein Gerät persistenten Speicher für einen virtuellen Computer zu erstellen. Das Gerät muss auf einem vorhandenen NTFS DAX-Volume erstellt werden.  Die neue Dateierweiterung (.vhdpmem) wird verwendet, um anzugeben, dass das Gerät einen persistenten Speicher wird. Nur das feste VHD-Dateiformat wird unterstützt.

**Beispiel:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>Erstellen eines virtuellen Computers mit einem persistenten Speicher-controller



Verwenden der **Cmdlet "New-VM"** einer VM der Generation 2 mit angegebene Arbeitsspeichergröße und der Pfad zu einem VHDX-Abbild zu erstellen. Verwenden Sie dann **hinzufügen-VMPmemController** einen persistenten Speicher-Controller eines virtuellen Computers hinzu.

**Beispiel:** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>Fügen Sie einen persistenten Speicher-Gerät an einen virtuellen Computer

Verwendung **[Add-VMHardDiskDrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** einem persistenten Speicher-Gerät an einen virtuellen Computer Anfügen

**Beispiel:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Persistenten Speicher-Geräte auf einem virtuellen Hyper-V-Computer angezeigt, als persistenten Speichergerät verarbeitet und vom Gastbetriebssystem verwaltet werden. Gastbetriebssysteme können das Gerät als einen Block oder ein DAX-Volume verwenden. Wenn Geräte von persistenten Speicher auf einem virtuellen Computer als DAX-Volume verwendet werden, profitieren sie mit niedriger Latenz auf Byteebene Adresse – Möglichkeit des Hostgeräts (keine e/a-Virtualisierung auf dem Codepfad). 

>[!NOTE] 
>Persistenten Speicher wird nur für Hyper-V-Gen2-VMs unterstützt. Live Migration und Speichermigration werden für virtuelle Computer mit persistenten Speicher nicht unterstützt. Produktionsprüfpunkte der virtuellen Computer enthalten keine persistenten Speicher enthaltenen Status. 