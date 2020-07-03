---
title: reg save
description: Referenz Artikel für den Befehl reg Save, mit dem eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei gespeichert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4051d69819cfd3550d094de8e9d4bc73f77c4e4b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931028"
---
# <a name="reg-save"></a>reg save

Speichert eine Kopie der angegebenen Unterschlüssel, Einträge und Werte der Registrierung in einer angegebenen Datei.

## <a name="syntax"></a>Syntax

```
reg save <keyname> <filename> [/y]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<filename>` | Gibt den Namen und den Pfad der erstellten Datei an. Wenn kein Pfad angegeben ist, wird der aktuelle Pfad verwendet. |
| /y | Überschreibt eine vorhandene Datei mit dem Namen *filename* , ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Vor dem Bearbeiten von Registrierungs Einträgen müssen Sie den übergeordneten Unterschlüssel mithilfe des Befehls **reg Save** speichern. Wenn die Bearbeitung fehlschlägt, können Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wiederherstellen.

- Die Rückgabewerte für den **reg-Speicher** Vorgang lauten:

    | Wert | Beschreibung |
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