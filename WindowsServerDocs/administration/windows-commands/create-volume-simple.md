---
title: Erstellen Sie eine einfache volume
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d754a6b5788656132459a0b4a42954e9084f26bb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836501"
---
# <a name="create-volume-simple"></a>Erstellen Sie eine einfache volume

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

erstellt ein einfaches Volume auf dem angegebenen dynamischen Datenträger.  
  
> [!IMPORTANT]  
> für Windows Vista ist dieser DiskPart-Befehl nur in der Windows Vista Ultimate, Windows Vista Enterprise und Windows Vista Business Edition verfügbar.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Größe\=<n>|Die Größe des Volumes in Megabytes \(MB\). Wenn keine Größe angegeben wird, beansprucht das neue Volume der verbleibende freie Speicherplatz auf dem Datenträger.|  
|disk\=<n>|Der dynamische Datenträger, auf dem das Volume erstellt wurde. Wenn kein Laufwerk angegeben wird, wird der aktuelle Datenträger verwendet.|  
|align\=<n>|Richtet alle Volume-Blöcke auf der nächsten. In der Regel verwendet, mit der Hardware-RAID Logical Unit Number \(LUN\) Arrays zur Verbesserung der Leistung. *n* ist die Anzahl der Kilobytes \(KB\) vom Anfang des Datenträgers an, die am nächsten Ausrichtungsgrenze.|  
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie das Volume erstellt haben, wechselt der Fokus automatisch auf das neue Volume.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie Folgendes ein, um ein Volume von 1000 MB Größe auf Datenträger 1 zu erstellen:  
  
```  
create volume simple size=1000 disk=1  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

