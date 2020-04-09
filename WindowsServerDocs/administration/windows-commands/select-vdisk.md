---
title: Vdisk auswählen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65e186413bebbf467cd4c2033d274badd1fbea80
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834743"
---
# <a name="select-vdisk"></a>Vdisk auswählen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene virtuelle Festplatte \(VHD-\) aus und verschiebt den Fokus darauf.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.  
  
## <a name="syntax"></a>Syntax  
  
```  
select vdisk file=<full path> [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Datei\=<full path>|Gibt den vollständigen Pfad und den Dateinamen einer vorhandenen VHD-Datei an.|  
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Um den Fokus auf die VHD mit dem Namen Test. VHD zu verschieben, geben Sie Folgendes ein:  
  
```  
select vdisk file=c:\test\test.vhd  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Vdisk anfügen](attach-vdisk.md)  
  
-   [Compact Vdisk](compact-vdisk.md)  
  
  
  
-   [Vdisk trennen](detach-vdisk.md)  
  
-   [Detail-Vdisk](detail-vdisk.md)  
  
-   [Erweitern von Vdisk](expand-vdisk.md)  
  
-   [Vdisk zusammenführen](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

