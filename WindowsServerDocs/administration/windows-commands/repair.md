---
title: Reparieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1e4b9cde10e11558aaa95edda94921144dac1f86
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441805"
---
# <a name="repair"></a>Reparieren

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

repariert RAID\-5-Volume mit Fokus, und Ersetzen Sie die fehlerhafte Festplatte Region durch den angegebenen dynamischen Datenträger.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter  |                                                                                             Beschreibung                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| disk\=<n>  |                                                                 Gibt an, den dynamischen Datenträger, der die Region für die fehlerhafte Festplatte ersetzt wird.                                                                 |
| align\=<n> |          Richtet alle Volumes oder einer Partition Blöcke auf der nächsten. *n* ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze.           |
|   Diskpart    | nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden. |
  
## <a name="remarks"></a>Hinweise  
  
-   Der angegebene dynamische Datenträger benötigen Speicherplatz größer als oder gleich auf die Gesamtgröße des fehlerhaften Datenträgers der Region, in das RAID\-5-Volumes.  
  
-   Ein Volume in einem RAID\-5-Array muss ausgewählt sein, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Volume** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um das Volume mit dem Schwerpunkt zu ersetzen, sie durch dynamische Datenträger 4 ersetzen, geben Sie Folgendes ein:  
  
```  
repair disk=4  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

