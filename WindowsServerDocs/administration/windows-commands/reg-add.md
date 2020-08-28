---
title: reg add
description: Referenz Artikel für den Befehl "reg Add", mit dem der Registrierung ein neuer Unterschlüssel oder Eintrag hinzugefügt wird.
ms.topic: reference
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b34ad768cdcd324ee2b0601785dbe12b7693d557
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037088"
---
# <a name="reg-add"></a>reg add

Fügt der Registrierung einen neuen Unterschlüssel oder Eintrag hinzu.

## <a name="syntax"></a>Syntax

```
reg add <keyname> [{/v Valuename | /ve}] [/t datatype] [/s Separator] [/d Data] [/f]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des hinzu zufügenden unter Schlüssels oder Eintrags an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /v `<Valuename>` | Gibt den Namen des Registrierungs Eintrags "Add" an. |
| /ve | Gibt an, dass der hinzugefügte Registrierungs Eintrag einen NULL-Wert aufweist. |
| /t `<Type>` | Gibt den Typ des Registrierungs Eintrags an. Der *Typ* muss einer der folgenden sein:<ul><li>REG_SZ</li><li>REG_MULTI_SZ</li><li>REG_DWORD_BIG_ENDIAN</li><li>REG_DWORD</li><li>REG_BINARY</li><li>REG_DWORD_LITTLE_ENDIAN</li><li>REG_LINK</li><li>REG_FULL_RESOURCE_DESCRIPTOR</li><li>REG_EXPAND_SZ</li></ul> |
| /s `<Separator>` | Gibt das Zeichen an, das verwendet werden soll, um mehrere Instanzen von Daten zu trennen, wenn der **REG_MULTI_SZ** -Datentyp angegeben wird und mehr als ein Eintrag aufgeführt wird. Wenn kein Wert angegeben wird, ist das Standard Trennzeichen **\ 0**. |
| /d `<Data>` | Gibt die Daten für den neuen Registrierungs Eintrag an. |
| /f | Fügt den Registrierungs Eintrag hinzu, ohne zur Bestätigung aufzufordern. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Mit diesem Vorgang können keine Teil Strukturen hinzugefügt werden. Diese Version von **reg** fordert beim Hinzufügen eines unter Schlüssels nicht zur Bestätigung auf.

- Die Rückgabewerte für den reg-Vorgang zum **Hinzufügen** lauten:

| Wert | Beschreibung |
|--|--|
| 0 | Erfolgreich |
| 1 | Fehler |

- Verwenden Sie für den **REG_EXPAND_SZ** Schlüsseltyp das Caretzeichen Symbol ( **^** ) mit **%** im/d-Parameter.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Schlüssel *HKLM\Software\MyCo* auf Remote Computer *ABC*hinzuzufügen:

```
reg add \\ABC\HKLM\Software\MyCo
```

Zum Hinzufügen eines Registrierungs Eintrags zu *HKLM\Software\MyCo* mit einem Wert namens *Data*, dem Typ *REG_BINARY*und den Daten von *fe340ead*geben Sie Folgendes ein:

```
reg add HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```

Zum Hinzufügen eines mehrwertigen Registrierungs Eintrags zu  *HKLM\Software\MyCo* mit einem Wert namens *MRU*, dem Typ *REG_MULTI_SZ*und den Daten von *fax\0mail\0\0*geben Sie Folgendes ein:

```
reg add HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```

Zum Hinzufügen eines erweiterten Registrierungs Eintrags zu *HKLM\Software\MyCo* mit einem Wert namens *path*, dem Typ *REG_EXPAND_SZ*und den Daten von *% systemroot%* geben Sie Folgendes ein:

```
reg add HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
