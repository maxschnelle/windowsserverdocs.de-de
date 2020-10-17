---
title: Typ
description: Referenz Artikel zum Type-Befehl, der den Inhalt einer Textdatei anzeigt.
ms.topic: reference
ms.assetid: c44fe905-a865-4c97-8cc5-fb95fec7d4d5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.openlocfilehash: 879cd68b4995c65d623d56e97c0680587eda15b4
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156368"
---
# <a name="type"></a>Typ

**Geben** Sie in der Windows-Befehlsshell einen integrierten Befehl ein, der den Inhalt einer Textdatei anzeigt. Verwenden Sie den Befehl **Type** , um eine Textdatei anzuzeigen, ohne Sie zu ändern.

In PowerShell ist **Type** ein integrierter Alias für das [Get-Content-Cmdlet](/powershell/module/microsoft.powershell.management/get-content), das auch den Inhalt einer Datei anzeigt, aber eine andere Syntax verwendet.

## <a name="syntax"></a>Syntax

```
type [<drive>:][<path>]<filename>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `[<drive>:][<path>]<filename>` | Gibt den Speicherort und den Namen der Datei oder Dateien an, die Sie anzeigen möchten. Wenn Sie `<filename>` Leerzeichen enthält, müssen Sie Sie in Anführungszeichen einschließen (z. b. "Dateiname mit Spaces.txt"). Sie können auch mehrere Dateinamen hinzufügen, indem Sie Leerzeichen zwischen diesen hinzufügen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn Sie eine Binärdatei oder eine Datei anzeigen, die von einem Programm erstellt wird, werden möglicherweise ungewöhnliche Zeichen auf dem Bildschirm angezeigt, einschließlich Seiten Vorschub-und escapesequenzsymbolen. Diese Zeichen stellen Steuerungs Codes dar, die in der Binärdatei verwendet werden. Vermeiden Sie im Allgemeinen die Verwendung des Befehls **Type** , um Binärdateien anzuzeigen.

## <a name="examples"></a>Beispiele

Um den Inhalt einer Datei mit dem Namen " *Holiday. Mar*" anzuzeigen, geben Sie Folgendes ein:

```
type holiday.mar
```

Geben Sie Folgendes ein, um den Inhalt einer langen Datei mit dem Namen " *Holiday. Mar* " jeweils auf einem Bildschirm anzuzeigen:

```
type holiday.mar | more
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
