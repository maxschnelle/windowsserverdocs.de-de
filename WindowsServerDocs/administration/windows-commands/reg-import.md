---
title: reg import
description: Referenz Artikel zum Befehl "reg Import", der den Inhalt einer Datei mit exportierten Registrierungs unter Schlüsseln, Einträgen und Werten in die Registrierung des lokalen Computers kopiert.
ms.topic: reference
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 49f83a20b4f9c9e1e64f6e33f0980757de60d9ec
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627033"
---
# <a name="reg-import"></a>reg import

Kopiert den Inhalt einer Datei, die exportierte Registrierungs Unterschlüssel, Einträge und Werte enthält, in die Registrierung des lokalen Computers.

## <a name="syntax"></a>Syntax

```
reg import <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<filename>` | Gibt den Namen und Pfad der Datei an, die Inhalte enthält, die in die Registrierung des lokalen Computers kopiert werden sollen. Diese Datei muss im Voraus mit dem reg- **Export**erstellt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Import** Vorgang lauten:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Registrierungseinträge aus der Datei mit dem Namen appbkup. reg zu importieren:

```
reg import AppBkUp.reg
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "reg Export"](reg-export.md)
