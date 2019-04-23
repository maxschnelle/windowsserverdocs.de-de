---
title: Erweitern Sie die virtuellen Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf8fd0b05ca5baeeee4fadd670adb3169130d04e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837401"
---
# <a name="expand-vdisk"></a>Erweitern Sie die virtuellen Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

wird eine virtuelle Festplatte (VHD) auf den, die von Ihnen angegebene Größe erweitert.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.
## <a name="syntax"></a>Syntax
```
expand vdisk maximum=<n>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|maximum=<n>|Gibt die neue Größe für die virtuelle Festplatte in Megabyte (MB) an.|
## <a name="remarks"></a>Hinweise
-   Eine virtuelle Festplatte muss ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Vdisk** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.
## <a name="BKMK_Examples"></a>Beispiele für
Um der ausgewählten virtuellen Festplatte auf 20 GB erweitern möchten, geben Sie Folgendes ein:
```
expand vdisk maximum=20000
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [attach vdisk](attach-vdisk.md)
-   [compact vdisk](compact-vdisk.md)

-   [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)
-   [detail vdisk](detail-vdisk.md)
-   [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)
-   [select vdisk](select-vdisk.md)
-   [list_1](list_1.md)
