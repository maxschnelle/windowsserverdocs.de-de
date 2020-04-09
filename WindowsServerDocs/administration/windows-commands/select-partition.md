---
title: Partition auswählen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97145d73cbbe1bdc9b27e545b047b78fe89e4984
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834803"
---
# <a name="select-partition"></a>Partition auswählen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene Partition aus und verschiebt den Fokus darauf. Dieser Befehl kann auch verwendet werden, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select partition=<n>  
```  
  
### <a name="parameters"></a>Parameter  
  
|   Parameter    |                                                                                    Beschreibung                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Partitions\=<n> | Die Nummer der Partition, die den Fokus erhalten soll. Sie können die Zahlen für alle Partitionen auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Partition auflisten** in DiskPart verwenden. |
  
## <a name="remarks"></a>Hinweise  
  
-   Bevor Sie eine Partition auswählen können, müssen Sie zunächst mithilfe des Befehls **Select Disk** (Datenträger auswählen) einen Datenträger auswählen.  
  
-   Wenn keine Partitionsnummer angegeben ist, zeigt dieser Befehl die Partition an, die derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Wenn Sie den Fokus auf Partition 3 verschieben möchten, geben Sie Folgendes ein:  
  
```  
select partitition=3  
```  
  
Geben Sie Folgendes ein, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat:  
  
```  
select partition  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

