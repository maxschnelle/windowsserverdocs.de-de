---
title: Erstellen einer Partition MSR
description: Windows-Befehls Artikel zum Erstellen einer Partition MSR, mit der eine Microsoft Reserved-Partition (MSR) auf einem GPT-Datenträger (GUID-Partitionstabelle) erstellt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a0f0390cd3b9f390e1f65b034fecd00d8ff41079
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847013"
---
# <a name="create-partition-msr"></a>Erstellen einer Partition MSR

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt eine reservierte Microsoft-Partition (MSR) auf einem GPT-Datenträger (GUID-Partitionstabelle).
  
> [!CAUTION]  
> Gehen Sie bei der Verwendung dieses Befehls sehr vorsichtig vor. Da GPT-Datenträger ein bestimmtes Partitionslayout erfordern, kann das Erstellen von reservierten Microsoft-Partitionen dazu führen, dass der Datenträger nicht mehr lesbar ist.
  
## <a name="syntax"></a>Syntax  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                         Beschreibung                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Größe\=<n>  |               Die Größe der Partition in Megabyte \(MB\). Die Partition ist mindestens so lang wie die Zahl, die durch <n>angegeben wird. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis in der aktuellen Region kein freier Speicherplatz mehr verfügbar ist.               |
| Offset\=<n> | Gibt den Offset in Kilobyte \(KB-\)an, bei dem die Partition erstellt wird. Der Offset wird aufgerundet, um alle verwendeten Sektorgrößen vollständig auszufüllen. Wenn kein Offset angegeben wird, wird die Partition in den ersten Datenträger Block eingefügt, der groß genug ist, um Sie zu speichern. |
|    Noerr    |                            Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                             |
  
## <a name="remarks"></a>Hinweise  
  
-   Auf GPT-Datenträgern, die zum Starten des Windows-Betriebssystems verwendet werden, ist die Extensible Firmware Interface \(EFI-\) Systempartition die erste Partition auf dem Datenträger, gefolgt von der reservierten Microsoft-Partition. GPT-Datenträger, die nur für die Datenspeicherung verwendet werden, verfügen über keine EFI-Systempartition. in diesem Fall ist die reservierte Microsoft-Partition die erste Partition.  
  
-   Von Windows werden keine reservierten Partitionen in Microsoft einbinden. Sie können keine Daten auf den Daten speichern, und Sie können Sie nicht löschen.  
  
-   Auf jedem GPT-Datenträger ist eine reservierte Microsoft-Partition erforderlich. Die Größe dieser Partition hängt von der Gesamtgröße des GPT-Datenträgers ab. Der GPT-Datenträger muss mindestens 32 MB groß sein, um eine reservierte Microsoft-Partition zu erstellen.  
  
-   Ein einfacher GPT-Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger **auswählen** einen einfachen GPT-Datenträger aus, und verschieben Sie den Fokus darauf.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie Folgendes ein, um eine reservierte Microsoft-Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition msr size=1000  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

