---
title: compact vdisk
description: Referenz Artikel für den Compact Vdisk-Befehl, mit dem die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD) reduziert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7379975981c2df386b7180c814799f7129eee7da
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929050"
---
# <a name="compact-vdisk"></a>compact vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). Dieser Parameter ist nützlich, da sich dynamisch erweiternde VHDs vergrößern, wenn Sie Dateien hinzufügen, aber Sie reduzieren beim Löschen von Dateien nicht automatisch die Größe.

## <a name="syntax"></a>Syntax

```
compact vdisk
```

### <a name="remarks"></a>Hinweise

- Eine dynamisch erweiterbare virtuelle Festplatte muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem [Befehl Vdisk auswählen](select-vdisk.md) eine VHD aus, und verschieben Sie den Fokus darauf.

- Sie können nur kompakte dynamisch erweiterbare virtuelle Festplatten verwenden, die getrennt oder als schreibgeschützt angefügt sind.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Vdisk anfügen"](attach-vdisk.md)

- [Detail-Vdisk-Befehl](detail-vdisk.md)

- [Befehl "Vdisk trennen"](detach-vdisk.md)

- [Vdisk-Befehl erweitern](expand-vdisk.md)

- [Befehl "Vdisk zusammenführen"](merge-vdisk.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [List-Befehl](list.md)
