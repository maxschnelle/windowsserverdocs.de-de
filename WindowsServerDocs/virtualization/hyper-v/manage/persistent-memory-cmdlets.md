---
title: Cmdlets zum Konfigurieren von persistenten Speichergeräten für Hyper-V-VMS
description: Konfigurieren von persistenten Speichergeräten für Hyper-V-VMS
ms.prod: windows-server
ms.service: na
manager: jasgroce
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: ecae1fe96bc5088fa840c6e2e24a75bb72a9e8f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392541"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Cmdlets zum Konfigurieren von persistenten Speichergeräten für Hyper-V-VMS

>Gilt für: Windows Server 2019

Dieser Artikel bietet Systemadministratoren und IT-Experten Informationen zum Konfigurieren von Hyper-V-VMS mit persistentem Speicher (Speicher Klassen Speicher oder nvdimm). Jdec-kompatible nvdimm-N persistente Speichergeräte werden in Windows Server 2016 und Windows 10 unterstützt und ermöglichen den Zugriff auf bytebene auf nicht flüchtige Geräte mit sehr geringer Latenzzeit. Persistente VM-Speichergeräte werden in Windows Server 2019 unterstützt. 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>Erstellen eines persistenten Speichergeräts für eine VM

Verwenden Sie das Cmdlet **[New-VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** , um ein dauerhaftes Speichergerät für einen virtuellen Computer zu erstellen. Das Gerät muss auf einem vorhandenen NTFS-DAX-Volume erstellt werden.  Die neue Dateinamenerweiterung (vhdpmem) wird verwendet, um anzugeben, dass es sich bei dem Gerät um ein dauerhaftes Speichergerät handelt. Nur das festgelegte VHD-Dateiformat wird unterstützt.

**Beispiel:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>Erstellen eines virtuellen Computers mit einem permanenten Speichercontroller



Verwenden Sie das **Cmdlet New-VM** , um einen virtuellen Computer der Generation 2 mit der angegebenen Speichergröße und dem Pfad zu einem vhdx-Image zu erstellen. Verwenden Sie dann **Add-vmpmemcontroller** , um einem virtuellen Computer einen persistenten Speichercontroller hinzuzufügen.

**Beispiel** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>Anfügen eines permanenten Speichergeräts an einen virtuellen Computer

Verwenden **[Sie "Add-vmharddiskdrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** ", um ein dauerhaftes Speichergerät an eine VM anzufügen.

**Beispiel:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Persistente Speichergeräte in einem virtuellen Hyper-V-Computer werden als persistentes Speichergerät angezeigt, das vom Gast Betriebssystem genutzt und verwaltet werden muss. Gast Betriebssysteme können das Gerät als Block-oder DAX-Volume verwenden. Wenn persistente Speichergeräte innerhalb eines virtuellen Computers als DAX-Volume verwendet werden, profitieren Sie von einer geringen Wartezeit für die Adress Fähigkeit des Host Geräts (keine e/a-Virtualisierung im Codepfad). 

>[!NOTE] 
>Persistenter Speicher wird nur für Hyper-V Gen2-VMS unterstützt. Livemigration-und Speicher Migration werden für virtuelle Computer mit persistentem Arbeitsspeicher nicht unterstützt. Produktions Prüfpunkte von VMS enthalten keinen permanenten Speicherstatus. 