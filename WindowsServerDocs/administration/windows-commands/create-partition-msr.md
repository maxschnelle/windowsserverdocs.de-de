---
title: Erstellen einer Partition MSR
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45cc215b097ce048b15f0e907f95f976e4941e28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378899"
---
# <a name="create-partition-msr"></a>Erstellen einer Partition MSR

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt eine reservierte Microsoft-\(msr @ no__t-1-Partition für eine GUID-Partitionstabelle \(gpt @ no__t-3-Datenträger.  
  
> [!CAUTION]  
> Gehen Sie bei der Verwendung dieses Befehls sehr vorsichtig vor. Da GPT-Datenträger ein bestimmtes Partitionslayout erfordern, kann das Erstellen von reservierten Microsoft-Partitionen dazu führen, dass der Datenträger nicht mehr lesbar ist.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                         Beschreibung                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Size @ no__t-0 @ no__t-1  |               Die Größe der Partition in Megabyte \(MB @ no__t-1. Die Partition ist mindestens so lang wie die Zahl, die durch <n> angegeben wird. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist.               |
| Offset @ no__t-0 @ no__t-1 | Gibt den Offset in Kilobyte \(KB @ no__t-1 an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um alle verwendeten Sektorgrößen vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. |
|    Noerr    |                            Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                             |
  
## <a name="remarks"></a>Hinweise  
  
-   Auf GPT-Datenträgern, die zum Starten des Windows-Betriebssystems verwendet werden, ist die Extensible Firmware Interface \(efi @ no__t-1-Systempartition die erste Partition auf dem Datenträger, gefolgt von der reservierten Microsoft-Partition. GPT-Datenträger, die nur für die Datenspeicherung verwendet werden, verfügen über keine EFI-Systempartition. in diesem Fall ist die reservierte Microsoft-Partition die erste Partition.  
  
-   Von Windows werden keine reservierten Partitionen in Microsoft einbinden. Sie können keine Daten auf den Daten speichern, und Sie können Sie nicht löschen.  
  
-   Auf jedem GPT-Datenträger ist eine reservierte Microsoft-Partition erforderlich. Die Größe dieser Partition hängt von der Gesamtgröße des GPT-Datenträgers ab. Der GPT-Datenträger muss mindestens 32 MB groß sein, um eine reservierte Microsoft-Partition zu erstellen.  
  
-   Ein einfacher GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen einfachen GPT-Datenträger aus, und verschieben Sie den Fokus darauf.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine reservierte Microsoft-Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition msr size=1000  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

