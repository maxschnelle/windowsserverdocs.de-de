---
title: detach vdisk
description: Referenz Artikel zum Befehl "Vdisk trennen", mit dem die ausgewählte virtuelle Festplatte (VHD) nicht mehr als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bce18dcf55940ca8529e4bee21af2f09282d0e00
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928702"
---
# <a name="detach-vdisk"></a>detach vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verhindert, dass die ausgewählte virtuelle Festplatte (VHD) als lokales Festplattenlaufwerk auf dem Host Computer angezeigt wird. Nachdem eine virtuelle Festplatte getrennt wurde, können Sie sie verschieben. Bevor Sie beginnen, müssen Sie eine VHD auswählen, damit dieser Vorgang erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl [Vdisk auswählen](select-vdisk.md) eine VHD aus, und verschieben Sie den Fokus darauf.


## <a name="syntax"></a>Syntax

```
detach vdisk [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die ausgewählte VHD zu trennen:

```
detach vdisk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Vdisk anfügen"](attach-vdisk.md)

- [Compact Vdisk-Befehl](compact-vdisk.md)

- [Detail-Vdisk-Befehl](detail-vdisk.md)

- [Vdisk-Befehl erweitern](expand-vdisk.md)

- [Befehl "Vdisk zusammenführen"](merge-vdisk.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [List-Befehl](list.md)
