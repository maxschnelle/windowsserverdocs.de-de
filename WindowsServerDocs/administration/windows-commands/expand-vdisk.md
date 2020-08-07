---
title: expand vdisk
description: Referenz Artikel zum Erweitern des Vdisk-Befehls, mit dem eine virtuelle Festplatte (VHD) auf eine angegebene Größe erweitert wird.
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d9c5c859dfa506d9f8afd07a0e78bdef210f60a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890447"
---
# <a name="expand-vdisk"></a>expand vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erweitert eine virtuelle Festplatte (VHD) auf eine angegebene Größe.

Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem [Befehl Vdisk auswählen](select-vdisk.md) ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="syntax"></a>Syntax

```
expand vdisk maximum=<n>
```

### <a name="parameters"></a>Parameter

 | Parameter | BESCHREIBUNG |
 |---------- | ----------- |
 | Maximum =`<n>` | Gibt die neue Größe für die VHD in Megabyte (MB) an. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die ausgewählte VHD auf 20 GB zu erweitern:

```
expand vdisk maximum=20000
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Vdisk-Befehl auswählen](select-vdisk.md)

- [Befehl "Vdisk anfügen"](attach-vdisk.md)

- [Compact Vdisk-Befehl](compact-vdisk.md)

- [Befehl "Vdisk trennen"](detach-vdisk.md)

- [Detail-Vdisk-Befehl](detail-vdisk.md)

- [Befehl "Vdisk zusammenführen"](merge-vdisk.md)

- [List-Befehl](list.md)
