---
title: Zusammenführen von virtuellen Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 159e307912cb06bc3ea5e452f735e786c0cf9965
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847011"
---
# <a name="merge-vdisk"></a>Zusammenführen von virtuellen Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Führt eine differenzierende virtuelle Festplatte (VHD) mit dem entsprechenden übergeordneten virtuellen Festplatte zusammen. Die übergeordnete virtuelle Festplatte wird geändert werden, sollen die Änderungen aus der differenzierenden VHD.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.
## <a name="syntax"></a>Syntax
```
merge vdisk depth=<n>
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|depth=<n>|Gibt die Anzahl der übergeordneten VHD-Dateien zusammenführen. Z. B. **Depth = 1** gibt an, dass die differenzierende VHD mit einer Ebene der differenzierungskette zusammengeführt werden.|
## <a name="remarks"></a>Hinweise
-   Eine virtuelle Festplatte muss ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Vdisk** Befehl aus, um die virtuelle Festplatte auswählen, und verschiebt den Fokus auf sie.
-   Dieser Parameter wird die übergeordnete virtuelle Festplatte geändert. Daher werden die andere differenzierenden virtuelle Festplatten, die vom übergeordneten Element abhängig sind nicht mehr gültig sein.
## <a name="BKMK_Examples"></a>Beispiele für
Wenn eine differenzierende virtuelle Festplatte mit dem übergeordneten virtuellen Festplatte zusammenführen möchten, geben Sie Folgendes ein:
```
merge vdisk depth=1
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [attach vdisk](attach-vdisk.md)
-   [compact vdisk](compact-vdisk.md)

-   [detail vdisk](detail-vdisk.md)
-   [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)
-   [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)
-   [select vdisk](select-vdisk.md)
-   [list_1](list_1.md)
