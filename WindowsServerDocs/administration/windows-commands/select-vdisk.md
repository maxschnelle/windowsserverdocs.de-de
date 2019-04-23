---
title: Wählen Sie die virtuellen Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a71a5c15c05a1e969d0720bc8e67e669d553f649
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852571"
---
# <a name="select-vdisk"></a>Wählen Sie die virtuellen Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Wählt das angegebene virtuelle Festplatte \(VHD\) und verlagert den Fokus auf sie.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.  
  
## <a name="syntax"></a>Syntax  
  
```  
select vdisk file=<full path> [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Datei\=<full path>|Gibt den vollständigen Pfad und Dateiname den Namen einer vorhandenen VHD-Datei an.|  
|Diskpart|Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um den Fokus auf die virtuelle Festplatte mit dem Namen Test.vhd verschieben möchten, geben Sie Folgendes ein:  
  
```  
select vdisk file="c:\test\test.vhd"  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [attach vdisk](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)  
  
-   [detail vdisk](detail-vdisk.md)  
  
-   [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)  
  
-   [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

