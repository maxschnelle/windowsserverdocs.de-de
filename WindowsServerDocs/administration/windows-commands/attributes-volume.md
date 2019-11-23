---
title: Attribut Volume
description: 'Windows-Befehle Thema für **Attribute Volume** : zeigt die Attribute eines Volumes an, legt Sie fest oder löscht sie.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 225a10307123763d1a024fcc08fbae536fd0b5df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382585"
---
# <a name="attributes-volume"></a>Attribut Volume

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden die Attribute eines Volumes angezeigt, festgelegt oder gelöscht.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|set|Legt das angegebene Attribut des Volumes mit dem Fokus fest.|  
|clear|Löscht das angegebene Attribut des Volumes mit dem Fokus.|  
|ReadOnly|Gibt an, dass das Volume nur\-gelesen wird.|  
|verbirgt|Gibt an, dass das Volume ausgeblendet ist.|  
|nodefaultdriveletter|Gibt an, dass das Volume standardmäßig keinen Laufwerk Buchstaben erhält.|  
|"Shadowcopy|Gibt an, dass das Volume ein Schattenkopievolume ist.|  
|Noerr|nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Auf Basis Master Boot Record \(MBR\)-Datenträgern gelten die Parameter **Hidden**, Read **only**und **nodefaultdriveletter** für alle Volumes auf dem Datenträger.  
  
-   Bei der grundlegenden GUID-Partitionstabelle \(GPT-\) Datenträgern und auf dynamischen MBR-und GPT-Datenträgern gelten die Parameter **Hidden**, Read **only**und **nodefaultdriveletter** nur für das ausgewählte Volume.  
  
-   Es muss ein Volume ausgewählt werden, damit der **Attribut Volume** -Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.  
  
## <a name="BKMK_examples"></a>Beispiele  
Wenn Sie die aktuellen Attribute auf dem ausgewählten Volume anzeigen möchten, geben Sie Folgendes ein:  
  
```  
attributes volume  
```  
  
Wenn Sie das ausgewählte Volume als ausgeblendet festlegen und nur\-lesen möchten, geben Sie Folgendes ein:  
  
```  
attributes volume set hidden readonly  
```  
  
Um die ausgeblendeten und Lese\-nur Attribute auf dem ausgewählten Volume zu entfernen, geben Sie Folgendes ein:  
  
```  
attributes volume clear hidden readonly  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

