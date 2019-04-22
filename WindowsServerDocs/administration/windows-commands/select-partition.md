---
title: Wählen Sie die partition
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c7d5675aa6c33ddbe1e5e873e1a7cf7a2e8f8017
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824961"
---
# <a name="select-partition"></a>Wählen Sie die partition

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Wählt die angegebene Partition aus, und verlagert den Fokus auf sie. Dieser Befehl kann auch verwendet werden, um die Partition anzuzeigen, die gegenwärtig den Fokus in den ausgewählten Datenträger besitzt.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select partition=<n>  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|partition\=<n>|Die Anzahl der Partition, die den Fokus erhalten. Sie können die Zahlen für alle Partitionen anzeigen, auf dem Datenträger, die derzeit ausgewählt wird, mithilfe der **Liste Partition** in DiskPart den Befehl.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Bevor Sie eine Partition auswählen, können Sie müssen zunächst auswählen einen Datenträger mithilfe der **select Disk** Befehl.  
  
-   Wenn keine Partitionsnummer angegeben wird, zeigt dieser Befehl die Partition, die gegenwärtig den Fokus in den ausgewählten Datenträger besitzt.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einer entsprechenden Menge ausgewählt ist, wird das Volume automatisch ausgewählt.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um den Fokus Partition 3 zu verschieben:  
  
```  
select partitition=3  
```  
  
Um die Partition anzuzeigen, die gerade den Fokus in den ausgewählten Datenträger besitzt, geben Sie Folgendes ein:  
  
```  
select partition  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

