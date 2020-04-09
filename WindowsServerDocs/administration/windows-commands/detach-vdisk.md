---
title: detach vdisk
description: Windows-Befehls Artikel zum Trennen von Vdisk, mit dem die ausgewählte virtuelle Festplatte (VHD) nicht als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14eb66031841624156afb03f492e2afce5bc56f0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846503"
---
# <a name="detach-vdisk"></a>detach vdisk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. Nachdem eine virtuelle Festplatte getrennt wurde, können Sie sie verschieben.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.  
  
## <a name="syntax"></a>Syntax  
  
```  
detach vdisk [noerr]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.  
  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Geben Sie Folgendes ein, um die ausgewählte VHD zu trennen:  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Vdisk anfügen](attach-vdisk.md)  
  
-   [Compact Vdisk](compact-vdisk.md)  

-   [Detail-Vdisk](detail-vdisk.md)  
  
-   [Erweitern von Vdisk](expand-vdisk.md)  
  
-   [Vdisk zusammenführen](merge-vdisk.md)  
  
-   [Vdisk auswählen](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

