---
title: reg compare
description: Referenz Artikel für den Befehl "reg Compare", der die angegebenen Registrierungs Unterschlüssel oder Einträge vergleicht.
ms.topic: reference
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 51c385b9a051574602c2508b8efd8f657c62ec7c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627099"
---
# <a name="reg-compare"></a>reg compare

Vergleicht die angegebenen Registrierungs Unterschlüssel oder-Einträge.

## <a name="syntax"></a>Syntax

```
reg compare <keyname1> <keyname2> [{/v Valuename | /ve}] [{/oa | /od | /os | on}] [/s]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname1>` | Gibt den vollständigen Pfad des hinzu zufügenden unter Schlüssels oder Eintrags an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| `<keyname2>` | Gibt den vollständigen Pfad des zweiten unter Schlüssels an, der verglichen werden soll. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Wenn Sie nur den Computernamen in *keyname2* angeben, wird vom-Vorgang der Pfad zum Unterschlüssel verwendet, der in *keyname1*angegeben ist. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /v `<Valuename>` | Gibt den Namen des Werts an, der unter dem Unterschlüssel verglichen werden soll. |
| /ve | Gibt an, dass nur Einträge mit dem Wertnamen NULL verglichen werden sollen. |
| /oa | Gibt an, dass alle Unterschiede und Übereinstimmungen angezeigt werden. Standardmäßig sind nur die Unterschiede aufgeführt. |
| /od | Gibt an, dass nur Unterschiede angezeigt werden. Dies ist das Standardverhalten. |
| /OS | Gibt an, dass nur Übereinstimmungen angezeigt werden. Standardmäßig sind nur die Unterschiede aufgeführt. |
| /on | Gibt an, dass nichts angezeigt wird. Standardmäßig sind nur die Unterschiede aufgeführt. |
| /s | Vergleicht alle Unterschlüssel und Einträge rekursiv. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Vergleichs** Vorgang lauten wie folgt:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Der Vergleich ist erfolgreich, und das Ergebnis ist identisch. |
    | 1 | Der Vergleich ist fehlgeschlagen. |
    | 2 | Der Vergleich war erfolgreich, und es wurden Unterschiede gefunden. |

- Zu den Symbolen, die in den Ergebnissen angezeigt werden, gehören:

    | Symbol | BESCHREIBUNG |
    |--|--|
    | = | *KeyName1* -Daten sind gleich *KeyName2* -Daten. |
    | < | *KeyName1* -Daten sind kleiner als *KeyName2* -Daten. |
    | > | *KeyName1* -Daten sind größer als *KeyName2* -Daten. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Werte unter dem Schlüssel " **myapp** " mit allen Werten unter dem Schlüssel " **SaveMyApp**" zu vergleichen:

```
reg compare HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp
```

Um den Wert für die Version unter dem Schlüssel **myco** und den Wert für die Version unter dem Schlüssel **MyCo1**zu vergleichen, geben Sie Folgendes ein:

```
reg compare HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version
```

Geben Sie Folgendes ein, um alle untergeordneten Schlüssel und Werte unter "HKLM\Software\MyCo" auf dem Computer mit dem Namen "Zodiac" mit allen unter Schlüsseln und Werten unter "HKLM\Software\MyCo" auf dem lokalen Computer zu vergleichen:

```
reg compare \\ZODIAC\HKLM\Software\MyCo \\. /s
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
