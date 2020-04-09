---
title: Volume auswählen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9337d7e4b37adcc22084249e53fb272335bf4f3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834703"
---
# <a name="select-volume"></a>Volume auswählen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt das angegebene Volume aus und verschiebt den Fokus auf das Volume. Dieser Befehl kann auch verwendet werden, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select volume={<n>|<d>}  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter |                                                                               Beschreibung                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <n>    | Die Nummer des Volumes, das den Fokus erhalten soll. Sie können die Zahlen für alle Volumes auf dem aktuell ausgewählten Datenträger anzeigen, indem Sie den Befehl **Volume auflisten** in DiskPart verwenden. |
|    <d>    |                                                 Der Laufwerk Buchstabe oder der einstellungspunktpfad des Volumes, das den Fokus erhalten soll.                                                 |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Volume angegeben ist, zeigt dieser Befehl das Volume an, das derzeit den Fokus auf dem ausgewählten Datenträger hat.  
  
-   Auf einem Basis Datenträger wird beim Auswählen eines Volumes auch der Fokus auf die entsprechende Partition fest.  
  
-   Wenn ein Volume mit einer entsprechenden Partition ausgewählt ist, wird die Partition automatisch ausgewählt.  
  
-   Wenn eine Partition mit einem entsprechenden Volume ausgewählt wird, wird das Volume automatisch ausgewählt.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Wenn Sie den Fokus auf Volume 2 verschieben möchten, geben Sie Folgendes ein:  
  
```  
select volume=2  
```  
  
Um den Fokus auf Laufwerk C zu verschieben, geben Sie Folgendes ein:  
  
```  
select volume=c  
```  
  
Geben Sie Folgendes ein, um den Fokus auf das Volume zu verschieben, das in einem Ordner namens mountpath eingebunden ist:  
  
```  
select volume=c:\mountpath  
```  
  
Geben Sie Folgendes ein, um das Volume anzuzeigen, das derzeit den Fokus auf dem ausgewählten Datenträger hat:  
  
```  
select volume  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

