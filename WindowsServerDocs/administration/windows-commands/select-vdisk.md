---
title: Vdisk auswählen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 1bfa6450d1704cde1e5ff2a50a8e3b61a30d0766
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384189"
---
# <a name="select-vdisk"></a>Vdisk auswählen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene virtuelle Festplatte \(vhd @ no__t-1 aus und verschiebt den Fokus darauf.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.  
  
## <a name="syntax"></a>Syntax  
  
```  
select vdisk file=<full path> [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|file @ no__t-0 @ no__t-1|Gibt den vollständigen Pfad und den Dateinamen einer vorhandenen VHD-Datei an.|  
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="BKMK_examples"></a>Beispiele  
Um den Fokus auf die VHD mit dem Namen Test. VHD zu verschieben, geben Sie Folgendes ein:  
  
```  
select vdisk file="c:\test\test.vhd"  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Vdisk anfügen](attach-vdisk.md)  
  
-   [Compact Vdisk](compact-vdisk.md)  
  
  
  
-   [Vdisk trennen](detach-vdisk.md)  
  
-   [Detail-Vdisk](detail-vdisk.md)  
  
-   [Erweitern von Vdisk](expand-vdisk.md)  
  
-   [Vdisk zusammenführen](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

