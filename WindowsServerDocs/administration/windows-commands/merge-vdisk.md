---
title: merge vdisk
description: Referenz Artikel zum Merge-Vdisk-Befehl, der eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammenfasst.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41201885861b7084fa7b49be8b5bf5a0e7394981
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925030"
---
# <a name="merge-vdisk"></a>merge vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammen. Die übergeordnete VHD wird so geändert, dass Sie die Änderungen der differenzierenden VHD einschließt. Mit diesem Befehl wird die übergeordnete VHD geändert. Folglich sind andere differenzierende VHDs, die vom übergeordneten Element abhängig sind, nicht mehr gültig.

> [!IMPORTANT]
> Sie müssen eine VHD auswählen und trennen, damit dieser Vorgang erfolgreich ist. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.

## <a name="syntax"></a>Syntax

```
merge vdisk depth=<n>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Tiefe =`<n>` | Gibt die Anzahl der übergeordneten VHD-Dateien an, die zusammengeführt werden sollen. `depth=1`Gibt z. b. an, dass die differenzierende VHD mit einer Ebene der differenzierenden Kette zusammengeführt wird. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine differenzierende VHD mit der übergeordneten VHD zusammenzuführen:

```
merge vdisk depth=1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Vdisk anfügen"](attach-vdisk.md)

- [Compact Vdisk-Befehl](compact-vdisk.md)

- [Detail-Vdisk-Befehl](detail-vdisk.md)

- [Befehl "Vdisk trennen"](detach-vdisk.md)

- [Vdisk-Befehl erweitern](expand-vdisk.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [List-Befehl](list.md)
