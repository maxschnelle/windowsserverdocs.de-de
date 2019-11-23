---
title: Vdisk trennen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4850f9f17218178f210820dd4c6ca96fd918accc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378688"
---
# <a name="detach-vdisk"></a>Vdisk trennen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verhindert, dass die ausgewählte virtuelle Festplatte \(VHD-\) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. Nachdem eine virtuelle Festplatte getrennt wurde, können Sie sie verschieben.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.  
  
## <a name="syntax"></a>Syntax  
  
```  
detach vdisk [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.  
  
## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie Folgendes ein, um die ausgewählte VHD zu trennen:  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Vdisk anfügen](attach-vdisk.md)  
  
-   [Compact Vdisk](compact-vdisk.md)  
  
  
  
-   [Detail-Vdisk](detail-vdisk.md)  
  
-   [Erweitern von Vdisk](expand-vdisk.md)  
  
-   [Vdisk zusammenführen](merge-vdisk.md)  
  
-   [Vdisk auswählen](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

