---
title: Volume auswählen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: cc981131c8de2dc4534e390645ef45c39a7b02ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371063"
---
# <a name="select-volume"></a>Volume auswählen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt das angegebene Volume aus und verschiebt den Fokus auf das Volume. Dieser Befehl kann auch verwendet werden, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select volume={<n>|<d>}  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter |                                                                               Beschreibung                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <n>    | Die Nummer des Volumes, das den Fokus erhalten soll. Sie können die Zahlen für alle Volumes auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Volume auflisten** in DiskPart verwenden. |
|    <d>    |                                                 Der Laufwerk Buchstabe oder der einstellungspunktpfad des Volumes, das den Fokus erhalten soll.                                                 |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Volume angegeben ist, zeigt dieser Befehl das Volume an, das derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
-   Auf einem Basis Datenträger wird beim Auswählen eines Volumes auch der Fokus auf die entsprechende Partition fest.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.  
  
## <a name="BKMK_examples"></a>Beispiele  
Wenn Sie den Fokus auf Volume 2 verschieben möchten, geben Sie Folgendes ein:  
  
```  
select volume=2  
```  
  
Um den Fokus auf Laufwerk C zu verschieben, geben Sie Folgendes ein:  
  
```  
select volume=c  
```  
  
Um den Fokus auf das Volume zu verschieben, das in einem Ordner namens "mountpath" eingebunden ist, geben Sie Folgendes ein:  
  
```  
select volume=c:\mountpath  
```  
  
Geben Sie Folgendes ein, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat:  
  
```  
select volume  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

