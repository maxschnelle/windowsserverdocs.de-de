---
title: reg unload
description: Referenz Artikel für den Befehl reg entladen, mit dem ein Abschnitt der Registrierung entfernt wird, der mit dem reg Load-Vorgang geladen wurde.
ms.topic: reference
ms.assetid: 1d07791d-ca27-454e-9797-27d7e84c5048
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5a94f4c3193a7096bd99d83a927ccb0b694d7faa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640310"
---
# <a name="reg-unload"></a>reg unload

Entfernt einen Abschnitt der Registrierung, der mit dem reg- **Lade** Vorgang geladen wurde.

## <a name="syntax"></a>Syntax

```
reg unload <keyname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<keyname>` | Gibt den vollständigen Pfad des unter Schlüssels an. Wenn Sie einen Remote Computer angeben möchten, schließen Sie den Computernamen (im Format `\\<computername>\` ) als Teil des *keyName*-Steuerelement ein. Das Weglassen bewirkt, dass `\\<computername>\` der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt wird. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: **HKLM**, **HKCU**, **HKCR**, **HKU**und **HKCC**. Wenn ein Remote Computer angegeben ist, lauten gültige Stamm Schlüssel: **HKLM** und **HKU**. Wenn der Registrierungsschlüssel Name ein Leerzeichen enthält, müssen Sie den Schlüsselnamen in Anführungszeichen einschließen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Rückgabewerte für den **reg-Entlade** Vorgang lauten wie folgt:

    | Wert | BESCHREIBUNG |
    |--|--|
    | 0 | Erfolgreich |
    | 1 | Fehler |

## <a name="examples"></a>Beispiele

Zum Entladen der Hive-temphive in der Datei HKLM geben Sie Folgendes ein:

```
reg unload HKLM\TempHive
```

> [!CAUTION]
> Bearbeiten Sie die Registrierung nur dann direkt, wenn Sie keine Alternative haben. Der Registrierungs-Editor umgeht Standard-Sicherheitsvorkehrungen und ermöglicht Einstellungen, die die Leistung beeinträchtigen, das System beschädigen oder sogar die Neuinstallation von Windows erfordern. Sie können die meisten Registrierungs Einstellungen sicher ändern, indem Sie die Programme in der Systemsteuerung oder Microsoft Management Console (MMC) verwenden. Wenn Sie die Registrierung direkt bearbeiten müssen, sichern Sie Sie zuerst.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl zum Laden von reg](reg-load.md)
