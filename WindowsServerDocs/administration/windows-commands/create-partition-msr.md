---
title: Erstellen der Partition msr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 79288fe90d037659f5e3934f1925dd8b7c21ad7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873431"
---
# <a name="create-partition-msr"></a>Erstellen der Partition msr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt einen Microsoft Reserved \(MSR\) Partition auf eine GUID-Partitionstabelle \(Gpt\) Datenträger.  
  
> [!CAUTION]  
> Vorsicht beim Verwenden dieses Befehls. Da Gpt-Datenträger auf eine bestimmte Partitionslayout erfordern, verursachen die Microsoft Reserved-Partitionen erstellen, dass den Datenträger nicht mehr gelesen werden.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Größe\=<n>|Die Größe der Partition in Megabytes \(MB\). Die Partition ist als die angegebene Anzahl mindestens so lange in Byte <n>. Wenn keine Größe angegeben wird, wird die Partition erst in der aktuellen Region nicht mehr Speicherplatz verfügbar ist.|  
|offset\=<n>|Gibt den Offset in Kilobyte \(KB\), an dem die Partition erstellt wird. Der Offset wird aufgerundet, vollständig ausgefüllt beliebige Sektorgröße verwendet wird. Wird kein Offset angegeben wird, wird die Partition in der ersten Datenträgerbereich platziert, die groß genug für die sie enthalten ist.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Auf Gpt-Datenträgern, die verwendet werden, starten Sie das Windows-Betriebssystem, die Extensible Firmware Interface \(EFI\) -Systempartition ist die erste Partition auf dem Datenträger, gefolgt von der Microsoft Reserved-Partition. GPT-Datenträger, die nur für die datenspeicherung verwendet werden müssen sich nicht auf eine EFI-Systempartition, in der Fall Microsoft Reserved-Partition die erste Partition ist, aus.  
  
-   Microsoft Reserved-Partitionen wird von Windows nicht bereitgestellt. Sie können keine Daten darauf speichern, und nicht löschen.  
  
-   Eine Microsoft Reserved-Partition ist auf jedem Gpt-Datenträger erforderlich. Die Größe dieser Partition hängt die Gesamtgröße der Gpt-Datenträger ab. Die Anzahl der Gpt-Datenträger muss mindestens 32 MB zum Erstellen einer Microsoft Reserved-Partition sein.  
  
-   Ein einfache Gpt-Datenträger muss ausgewählt werden, für diesen Vorgang erfolgreich ausgeführt werden kann. Verwenden der **select Disk** Befehl aus, wählen Sie einen einfache Gpt-Datenträger und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um eine Microsoft Reserved-Partition von 1000 MB Größe zu erstellen, geben Sie Folgendes ein:  
  
```  
create partition msr size=1000  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

