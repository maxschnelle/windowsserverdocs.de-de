---
title: Trennen Sie die virtuellen Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0b6a1ecd3d787506c89f120bed204cc30e6d68d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822731"
---
# <a name="detach-vdisk"></a>Trennen Sie die virtuellen Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beendet die ausgewählte virtuelle Festplatte \(VHD\) als ein lokales Festplattenlaufwerk auf dem Hostcomputer angezeigt werden. Nachdem eine virtuelle Festplatte getrennt wurde, können Sie sie verschieben.  
  
> [!NOTE]  
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.  
  
## <a name="syntax"></a>Syntax  
  
```  
detach vdisk [noerr]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|Diskpart|Nur für Skripting verwendet. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|  
  
## <a name="remarks"></a>Hinweise  
  
-   Eine virtuelle Festplatte muss ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Vdisk** Befehl aus, um die virtuelle Festplatte auswählen, und verschiebt den Fokus auf sie.  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Um die ausgewählte VHD zu trennen, geben Sie Folgendes ein:  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [attach vdisk](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [detail vdisk](detail-vdisk.md)  
  
-   [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)  
  
-   [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)  
  
-   [select vdisk](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

