---
title: reg restore
description: Referenz Artikel für den Befehl "reg Restore", mit dem gespeicherte Unterschlüssel und Einträge in die Registrierung zurückgeschrieben werden.
ms.topic: reference
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d5c0e51ed3b16c2655647919f360a56b2aee6344
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639851"
---
# <a name="reg-restore"></a>reg restore

Schreibt gespeicherte Unterschlüssel und Einträge zurück in die Registrierung.

## <a name="syntax"></a>Syntax

```
reg restore <keyname> <filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an, der wieder hergestellt werden soll. Der Wiederherstellungs Vorgang funktioniert nur mit dem lokalen Computer. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<filename>` | Gibt den Namen und Pfad der Datei mit Inhalt an, der in die Registrierung geschrieben werden soll. Diese Datei muss im Voraus mit dem Befehl **reg Save** erstellt werden, und Sie muss über die Erweiterung. HIV verfügen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Vor dem Bearbeiten von Registrierungs Einträgen müssen Sie den übergeordneten Unterschlüssel mithilfe des Befehls **reg Save** speichern. Wenn die Bearbeitung fehlschlägt, können Sie den ursprünglichen Unterschlüssel mit dem **reg Restore** -Vorgang wiederherstellen.

- Die Rückgabewerte für den **reg-Wiederherstellungs** Vorgang lauten:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datei mit dem Namen "NTRKBkUp. HIV" im Schlüssel "HKLM\Software\Microsoft\ResKit" wiederherzustellen, und überschreiben Sie den vorhandenen Inhalt des Schlüssels:

```
reg restore HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl zum Speichern von reg](reg-save.md)
