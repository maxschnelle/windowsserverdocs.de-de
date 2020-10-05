---
title: subst
description: Referenz Artikel für den SUBST-Befehl, der einen Pfad mit einem Laufwerk Buchstaben verknüpft.
ms.topic: reference
ms.assetid: 3e69234c-2312-4343-868b-afc1017c622a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 52d45c9139c70c4f513a972f7789f872145c8b63
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718227"
---
# <a name="subst"></a>subst

Ordnet einen Pfad einem Laufwerk Buchstaben zu. Bei Verwendung ohne Parameter zeigt **subst** die Namen der virtuellen Laufwerke an.

## <a name="syntax"></a>Syntax

```
subst [<drive1>: [<drive2>:]<path>]
subst <drive1>: /d
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<drive1>:` | Gibt das virtuelle Laufwerk an, dem Sie einen Pfad zuweisen möchten. |
| `[<drive2>:]<path>` | Gibt das physische Laufwerk und den Pfad an, die einem virtuellen Laufwerk zugewiesen werden sollen. |
| /d | Löscht ein ersetzes (virtuelles) Laufwerk. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Bemerkungen

- Die folgenden Befehle funktionieren nicht und dürfen nicht auf den im **subst** -Befehl angegebenen Laufwerken verwendet werden:

  - [chkdsk-Befehl](chkdsk.md)

    [diskcomp-Befehl](diskcomp.md)

    [DISKCOPY-Befehl](diskcopy.md)

    [Befehl "Format"](format.md)

    [Befehl "Bezeichnung"](label.md)

    [Befehl Wiederherstellen](recover.md)

- Der- `<drive1>` Parameter muss innerhalb des Bereichs liegen, der durch den **LastDrive** -Befehl angegeben wird. Andernfalls zeigt **subst** die folgende Fehlermeldung an: `Invalid parameter - drive1:`

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um ein virtuelles Laufwerk z für den Pfad b:\user\tool\forms zu erstellen:

```
subst z: b:\user\betty\forms
```

Anstatt den vollständigen Pfad einzugeben, können Sie dieses Verzeichnis erreichen, indem Sie den Buchstaben des virtuellen Laufwerks gefolgt von einem Doppelpunkt wie folgt eingeben:

```
z:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)