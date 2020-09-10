---
title: reg save
description: Referenz Artikel für den Befehl reg Save, mit dem eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei gespeichert wird.
ms.topic: reference
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f75aedc391eec495a82fe2ea674164552ef66e80
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640320"
---
# <a name="reg-save"></a>reg save

Speichert eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei.

## <a name="syntax"></a>Syntax

```
reg save <keyname> <filename> [/y]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<filename>` | Gibt den Namen und den Pfad der erstellten Datei an. Wenn kein Pfad angegeben ist, wird der aktuelle Pfad verwendet. |
| /y | Überschreibt eine vorhandene Datei mit dem Namen *filename* , ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Vor dem Bearbeiten von Registrierungs Einträgen müssen Sie den übergeordneten Unterschlüssel mithilfe des Befehls **reg Save** speichern. Wenn die Bearbeitung fehlschlägt, können Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wiederherstellen.

- Die Rückgabewerte für den **reg-Speicher** Vorgang lauten:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Hive-Datei "MyApp" als Datei mit dem Namen appbkup. HIV im aktuellen Ordner zu speichern:

```
reg save HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "reg Restore"](reg-restore.md)