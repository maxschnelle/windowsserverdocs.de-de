---
title: Attribute-volume
description: Windows-Befehle Thema **Attribute Volume** -zeigt, Mengen oder löscht die Attribute eines Volumes.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 37af55ee2a041fbcf8068e0def72147732d3a687
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846581"
---
# <a name="attributes-volume"></a>Attribute-volume

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, legt fest oder löscht die Attribute eines Volumes.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|set|Legt das angegebene Attribut des Volumes mit dem Fokus fest.|  
|clear|Löscht das angegebene Attribut des Volumes mit dem Fokus.|  
|ReadOnly|Gibt an, dass das Volume zu lesen ist\-nur.|  
|Ausgeblendet|Gibt an, dass das Volume ausgeblendet ist.|  
|nodefaultdriveletter|Gibt an, dass das Volume einen Laufwerkbuchstaben nicht in der Standardeinstellung erhält.|  
|Schattenkopie|Gibt an, dass das Volume eine Schattenkopievolume.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   In einfachen master Boot Records \(MBR\) Datenträger, die **ausgeblendeten**, **Readonly**, und **Nodefaultdriveletter** Parameter gelten für alle Volumes, auf der Datenträger.  
  
-   Für grundlegende GUID-Partitionstabelle \(Gpt\) Datenträger und dynamischen MBR- und Gpt-Datenträgern die **ausgeblendeten**, **Readonly**, und **Nodefaultdriveletter** Parameter gelten nur für das ausgewählte Volume.  
  
-   Ein Volume muss ausgewählt werden, für die **Attribute Volume** Befehl erfolgreich ausgeführt werden kann. Verwenden der **wählen Volume** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um die aktuellen Attribute auf dem ausgewählten Volume anzuzeigen, geben Sie Folgendes ein:  
  
```  
attributes volume  
```  
  
Um das ausgewählte Volume als schreibgeschützten und ausgeblendeten festzulegen\-nur geben:  
  
```  
attributes volume set hidden readonly  
```  
  
So entfernen Sie verborgene und read\-Geben Sie nur die Attribute auf ausgewählten Volumes:  
  
```  
attributes volume clear hidden readonly  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

