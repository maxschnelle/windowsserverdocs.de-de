---
title: reg load
description: Referenz Artikel für den Befehl "reg Load", mit dem gespeicherte Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung geschrieben werden.
ms.topic: reference
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 31b0baf4f4c6e903c7dc9716f8a9dc47d29227b5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627066"
---
# <a name="reg-load"></a>reg load

Schreibt gespeicherte Unterschlüssel und Einträge in einen anderen Unterschlüssel in der Registrierung. Dieser Befehl ist für die Verwendung mit temporären Dateien vorgesehen, die für die Problembehandlung oder Bearbeitung von Registrierungs Einträgen verwendet werden.

## <a name="syntax"></a>Syntax

```
reg load <keyname> <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des zu ladenden unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen.  |
| `<filename>` | Gibt den Namen und den Pfad der Datei an, die geladen werden soll. Diese Datei muss im Voraus mit dem Befehl **reg Save** erstellt werden, und Sie muss über die Erweiterung. HIV verfügen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Lade** Vorgang lauten:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Wenn Sie die Datei mit dem Namen temphive. HIV in den Schlüssel hklm\temphive laden möchten, geben Sie Folgendes ein:

```
reg load HKLM\TempHive TempHive.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl zum Speichern von reg](reg-save.md)
