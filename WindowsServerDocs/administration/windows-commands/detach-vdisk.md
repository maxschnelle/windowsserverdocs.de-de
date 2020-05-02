---
title: detach vdisk
description: Referenz Thema zum Trennen von Vdisk, das verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5e64559650597eb8d15e28075f74704fdf338a6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716669"
---
# <a name="detach-vdisk"></a>detach vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. Nachdem eine virtuelle Festplatte getrennt wurde, können Sie sie verschieben.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.  
  
## <a name="syntax"></a>Syntax  
  
```  
detach vdisk [noerr]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="remarks"></a>Bemerkungen  
  
-   Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.  
  
## <a name="examples"></a>Beispiele  
Geben Sie Folgendes ein, um die ausgewählte VHD zu trennen:  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [attach vdisk](attach-vdisk.md)  
  
-   [Compact Vdisk](compact-vdisk.md)  

-   [Detail-Vdisk](detail-vdisk.md)  
  
-   [Erweitern von Vdisk](expand-vdisk.md)  
  
-   [Vdisk zusammenführen](merge-vdisk.md)  
  
-   [Vdisk auswählen](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

