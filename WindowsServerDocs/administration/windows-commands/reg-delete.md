---
title: reg delete
description: Referenz Artikel für den Befehl reg DELETE, mit dem ein Unterschlüssel oder Einträge aus der Registrierung gelöscht werden.
ms.topic: reference
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e7c132be937fab973bee0f5bb81bf6377128e483
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627042"
---
# <a name="reg-delete"></a>reg delete

Löscht einen Unterschlüssel oder Einträge aus der Registrierung.

## <a name="syntax"></a>Syntax

```
reg delete <keyname> [{/v Valuename | /ve | /va}] [/f]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname1>` | Gibt den vollständigen Pfad des hinzu zufügenden unter Schlüssels oder Eintrags an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /v `<Valuename>` | Löscht einen bestimmten Eintrag unter dem Unterschlüssel. Wenn kein Eintrag angegeben wird, werden alle Einträge und Unterschlüssel unter dem Unterschlüssel gelöscht. |
| /ve | Gibt an, dass nur Einträge, für die kein Wert vorhanden ist, gelöscht werden. |
| /va | Löscht alle Einträge unter dem angegebenen Unterschlüssel. Unterschlüssel unter dem angegebenen Unterschlüssel werden nicht gelöscht. |
| /f | Löscht den vorhandenen Registrierungs Unterschlüssel oder Eintrag, ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Lösch** Vorgang lauten:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Registrierungsschlüssel Timeout und dessen alle Unterschlüssel und Werte zu löschen:

```
reg delete HKLM\Software\MyCo\MyApp\Timeout
```

Geben Sie Folgendes ein, um den Registrierungs Wert auf dem Computer mit dem Namen "Zodiac" unter HKLM\Software\MyCo zu löschen:

```
reg delete \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
