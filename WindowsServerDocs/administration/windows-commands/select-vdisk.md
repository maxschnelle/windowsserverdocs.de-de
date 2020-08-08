---
title: select vdisk
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b66a02633cac60faf85824acb9191be61b551ee3
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992911"
---
# <a name="select-vdisk"></a>select vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

wählt die angegebene virtuelle Festplatten \( -VHD aus \) und verschiebt den Fokus darauf.

> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.

## <a name="syntax"></a>Syntax

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|Datei\=<full path>|Gibt den vollständigen Pfad und den Dateinamen einer vorhandenen VHD-Datei an.|
|Noerr|Wird nur für die Skripterstellung verwendet. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.|

## <a name="examples"></a>Beispiele
Um den Fokus auf die VHD mit dem Namen Test. VHD zu verschieben, geben Sie Folgendes ein:

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

-   [attach vdisk](attach-vdisk.md)

-   [compact vdisk](compact-vdisk.md)



-   [Vdisk trennen](detach-vdisk.md)

-   [detail vdisk](detail-vdisk.md)

-   [expand vdisk](expand-vdisk.md)

-   [Vdisk zusammenführen](merge-vdisk.md)

-   [list_1](./list.md)