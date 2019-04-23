---
title: Volume auswählen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0ebf9896621268c384ea8129d32c985028054d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890731"
---
# <a name="select-volume"></a>Volume auswählen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Wählt das angegebene Volume und verlagert den Fokus auf sie. Dieser Befehl kann auch verwendet werden, um das Volume anzuzeigen, das gegenwärtig den Fokus in den ausgewählten Datenträger besitzt.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select volume={<n>|<d>}  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|<n>|Die Anzahl der dem Volume, das den Fokus erhalten. Sehen Sie die Zahlen für alle Volumes auf dem Datenträger, die derzeit ausgewählt wird, mithilfe der **Liste Volume** in DiskPart den Befehl.|  
|<d>|Der Laufwerkbuchstabe oder Bereitstellungspunkt Punkt Laufwerkpfad des Volumes, das den Fokus erhalten.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Volume angegeben wird, zeigt dieser Befehl das Volume, das gegenwärtig den Fokus in den ausgewählten Datenträger besitzt.  
  
-   Auf einem Basisdatenträger ein Volume erhält auswählen auch den Fokus auf die entsprechende Partition.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einer entsprechenden Menge ausgewählt ist, wird das Volume automatisch ausgewählt.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um den Fokus auf Volume 2 zu verschieben, geben Sie Folgendes ein:  
  
```  
select volume=2  
```  
  
Um den Fokus auf Laufwerk C zu verschieben, geben Sie Folgendes ein:  
  
```  
select volume=c  
```  
  
Um den Fokus auf das Volume bereitgestellt, die für einen Ordner mit dem Namen "Mountpath" verschieben möchten, geben Sie Folgendes ein:  
  
```  
select volume=c:\mountpath  
```  
  
Um das Volume anzuzeigen, das gerade den Fokus in den ausgewählten Datenträger besitzt, geben Sie Folgendes ein:  
  
```  
select volume  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

