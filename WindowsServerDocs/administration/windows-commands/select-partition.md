---
title: Partition auswählen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a186e2678fde64396a8b4b57a2d14e4b0b7bf26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371070"
---
# <a name="select-partition"></a>Partition auswählen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene Partition aus und verschiebt den Fokus darauf. Dieser Befehl kann auch verwendet werden, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select partition=<n>  
```  
  
## <a name="parameters"></a>Parameter  
  
|   Parameter    |                                                                                    Beschreibung                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Partitions\=<n> | Die Nummer der Partition, die den Fokus erhalten soll. Sie können die Zahlen für alle Partitionen auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Partition auflisten** in DiskPart verwenden. |
  
## <a name="remarks"></a>Hinweise  
  
-   Bevor Sie eine Partition auswählen können, müssen Sie zunächst mithilfe des Befehls **Select Disk** (Datenträger auswählen) einen Datenträger auswählen.  
  
-   Wenn keine Partitionsnummer angegeben ist, zeigt dieser Befehl die Partition an, die derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.  
  
## <a name="BKMK_examples"></a>Beispiele  
Wenn Sie den Fokus auf Partition 3 verschieben möchten, geben Sie Folgendes ein:  
  
```  
select partitition=3  
```  
  
Geben Sie Folgendes ein, um die Partition anzuzeigen, die derzeit den Fokus auf dem ausgewählten Datenträger hat:  
  
```  
select partition  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

