---
title: reg query
description: Referenz Artikel für den Befehl "reg Query", der eine Liste der nächsten Ebene von unter Schlüsseln und Einträgen zurückgibt, die sich unter einem angegebenen Unterschlüssel in der Registrierung befinden.
ms.topic: reference
ms.assetid: 0e6a0d7c-ed9b-4318-833d-33f265a81f39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 633928d89059e1b9a9677141011b391ee0d34757
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025084"
---
# <a name="reg-query"></a>reg query

Gibt eine Liste der nächsten Ebene von unter Schlüsseln und Einträgen zurück, die sich unter einem angegebenen Unterschlüssel in der Registrierung befinden.

## <a name="syntax"></a>Syntax

```
reg query <keyname> [{/v <Valuename> | /ve}] [/s] [/se <separator>] [/f <data>] [{/k | /d}] [/c] [/e] [/t <Type>] [/z]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /v `<Valuename>` | Gibt den Namen des Registrierungs Werts an, der abgefragt werden soll. Wenn der Wert nicht ausgelassen wird, werden alle Wert Namen für *keyName* zurückgegeben. *ValueName* für diesen Parameter ist optional, wenn auch die Option **/f** verwendet wird. |
| /ve | Führt eine Abfrage für Werte Namen aus, die leer sind. |
| /s | Gibt an, dass alle Unterschlüssel und Wertnamen rekursiv abgefragt werden sollen. |
| /se `<separator>` | Gibt das einzelne Wert Trennzeichen an, nach dem in der wertnamensart **REG_MULTI_SZ**gesucht werden soll. Wenn das *Trenn* Zeichen nicht angegeben wird, wird **\ 0** verwendet. |
| /f `<data>` | Gibt die zu suchenden Daten oder Muster an. Verwenden Sie doppelte Anführungszeichen, wenn eine Zeichenfolge Leerzeichen enthält. Wenn nicht angegeben, wird ein Platzhalter (**&#42;**) als Suchmuster verwendet. |
| /k | Gibt an, dass nur in Schlüsselnamen gesucht werden soll. |
| /d | Gibt an, dass nur Daten durchsucht werden sollen. |
| /C | Gibt an, dass bei der Abfrage groß-und Kleinschreibung Standardmäßig wird bei Abfragen die Groß-/Kleinschreibung nicht beachtet. |
| /e | Gibt an, dass nur genaue Übereinstimmungen zurückgegeben werden. Standardmäßig werden alle Übereinstimmungen zurückgegeben. |
| /t `<Type>` | Gibt die zu durchsuchenden Registrierungs Typen an. Gültige Typen sind: **REG_SZ**, **REG_MULTI_SZ**, **REG_EXPAND_SZ**, **REG_DWORD**, **REG_BINARY REG_NONE** **.** Wenn nicht angegeben, werden alle Typen durchsucht. |
| /z | Gibt an, dass die numerische Entsprechung für den Registrierungstyp in den Suchergebnissen enthalten soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Die Rückgabewerte für den **reg-Abfrage** Vorgang lauten:

    | Wert | Beschreibung |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Wert der namens Wert Version im Schlüssel "HKLM\Software\Microsoft\ResKit" anzuzeigen:

```
reg query HKLM\Software\Microsoft\ResKit /v Version
```

Wenn Sie alle untergeordneten Schlüssel und Werte unter dem Schlüssel HKLM\Software\Microsoft\ResKit\Nt\Setup auf einem Remote Computer mit dem Namen ABC anzeigen möchten, geben Sie Folgendes ein:

```
reg query \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s
```

Geben Sie Folgendes ein, um alle untergeordneten Schlüssel und Werte des Typs REG_MULTI_SZ mit **#** als Trennzeichen anzuzeigen:

```
reg query HKLM\Software\Microsoft\ResKit\Nt\Setup /se #
```

Geben Sie Folgendes ein, um den Schlüssel, den Wert und die Daten für exakte und Groß-/Kleinschreibung des Systems unter dem HKLM-Stamm des Datentyps REG_SZ anzuzeigen:

```
reg query HKLM /f SYSTEM /t REG_SZ /c /e
```

Geben Sie Folgendes ein, um den Schlüssel, den Wert und die Daten anzuzeigen, die **0F** in den Daten unter dem HKCU-Stamm Schlüssel des Datentyps "REG_BINARY" entsprechen:

```
reg query HKCU /f 0F /d /t REG_BINARY
```

Geben Sie Folgendes ein, um den Wert und die Daten für Werte Namen von NULL (Standard) unter "HKLM\Software" anzuzeigen:

```
reg query HKLM\SOFTWARE /ve
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
