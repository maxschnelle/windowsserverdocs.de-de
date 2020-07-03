---
title: reg export
description: Referenz Artikel für den Befehl "reg Export", bei dem die angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung an andere Server kopiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c0cad839569651823e1c1a2bcca3c17c5550c8a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934644"
---
# <a name="reg-export"></a>reg export

Kopiert die angegebenen Unterschlüssel, Einträge und Werte des lokalen Computers in eine Datei für die Übertragung an andere Server.

## <a name="syntax"></a>Syntax

```
reg export <keyname> <filename> [/y]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an. Der Export Vorgang funktioniert nur mit dem lokalen Computer. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<filename>` | Gibt den Namen und Pfad der Datei an, die während des Vorgangs erstellt werden soll. Die Datei muss die Erweiterung ". reg" aufweisen. |
| /y | Überschreibt alle vorhandenen Dateien mit dem Namen *filename* , ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Export** Vorgang lauten:

    | Wert | Beschreibung |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Inhalt aller Unterschlüssel und Werte des Schlüssels "MyApp" in die Datei "appbkup. reg" zu exportieren:

```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
