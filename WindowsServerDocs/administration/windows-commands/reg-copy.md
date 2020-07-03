---
title: reg copy
description: Referenz Artikel zum Befehl "reg Copy", bei dem ein Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer kopiert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e98faa37f1d123c584a3e12ae013c35688c37680
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937029"
---
# <a name="reg-copy"></a>reg copy

Kopiert einen Registrierungs Eintrag an einen angegebenen Speicherort auf dem lokalen Computer oder auf dem Remote Computer.

## <a name="syntax"></a>Syntax

```
reg copy <keyname1> <keyname2> [/s] [/f]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<keyname1>` | Gibt den vollständigen Pfad des hinzu zufügenden unter Schlüssels oder Eintrags an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<keyname2>` | Gibt den vollständigen Pfad des zweiten unter Schlüssels an, der verglichen werden soll. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /s | Kopiert alle Unterschlüssel und Einträge unter den angegebenen Unterschlüssel. |
| /f | Kopiert den Unterschlüssel, ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Dieser Befehl fordert beim Kopieren eines unter Schlüssels keine Bestätigung an.

- Die Rückgabewerte für den **reg-Vergleichs** Vorgang lauten wie folgt:

    | Wert | Beschreibung |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Unterschlüssel und Werte unter dem Schlüssel "MyApp" in den Schlüssel "SaveMyApp" zu kopieren:

```
reg copy HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```

Wenn Sie alle Werte unter dem Schlüssel myco auf dem Computer mit dem Namen "Zodiac" in den Schlüssel MyCo1 auf dem aktuellen Computer kopieren möchten, geben Sie Folgendes ein:

```
reg copy \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
