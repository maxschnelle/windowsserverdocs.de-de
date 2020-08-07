---
title: )
description: Referenz Artikel für den weiteren Befehl, der einen Bildschirm der Ausgabe gleichzeitig anzeigt.
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/26/2019
ms.openlocfilehash: 198f3f3f3b80282d876e4fdda9e7cde649a8c7da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886375"
---
# <a name="more"></a>)

Zeigt jeweils einen Bildschirm der Ausgabe an.

> [!NOTE]
> Der **more** -Befehl mit unterschiedlichen Parametern ist auch über die Wiederherstellungskonsole verfügbar.

## <a name="syntax"></a>Syntax

```
<command> | more [/c] [/p] [/s] [/t<n>] [+<n>]
more [[/c] [/p] [/s] [/t<n>] [+<n>]] < [<drive>:][<path>]<filename>
more [/c] [/p] [/s] [/t<n>] [+<n>] [<files>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<command>` | Gibt einen Befehl an, für den die Ausgabe angezeigt werden soll. |
| /C | Löscht den Bildschirm, bevor eine Seite angezeigt wird. |
| /p | Erweitert Formular-Feed-Zeichen. |
| /s | Zeigt mehrere leere Zeilen als einzelne Leerzeile an. |
| /t`<n>` | Zeigt Registerkarten als Anzahl von Leerzeichen an, die durch *n*angegeben werden. |
| +`<n>` | Zeigt die erste Datei an, beginnend bei der Zeile, die durch *n*angegeben wird. |
| `[<drive>:][<path>]<filename>` | Gibt den Speicherort und den Namen einer Datei an, die angezeigt werden soll. |
| `<files>` | Gibt eine Liste der anzuzeigenden Dateien an. Dateien müssen mithilfe von Leerzeichen getrennt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Die folgenden Unterbefehle werden an der **ausführlicheren** Eingabeaufforderung ( `-- More --` ) akzeptiert, einschließlich:

    | Schlüssel | Aktion |
    | --- | ------ |
    | LEERTASTE | Drücken Sie die **LEERTASTE** , um den nächsten Bildschirm anzuzeigen. |
    | EINGABETASTE | Drücken **Sie die Eingabe** Taste, um die Datei nacheinander anzuzeigen. |
    | f | Drücken Sie **F** , um die nächste Datei anzuzeigen, die in der Befehlszeile aufgelistet ist. |
    | q | Drücken Sie **Q** , um den Befehl **Weitere** zu beenden. |
    | = | Zeigt die Zeilennummer an. |
    | cker`<n>` | Drücken Sie **P** , um die nächsten *n* Zeilen anzuzeigen. |
    | Hymnen`<n>` | Drücken Sie **S** , um die nächsten *n* Zeilen zu überspringen. |
    | ? | Drücken **?** , um die Befehle anzuzeigen, die an der **ausführlicheren** Eingabeaufforderung verfügbar sind.|

- Wenn Sie das-Umleitungs Zeichen ( `<` ) verwenden, müssen Sie auch einen Dateinamen als Quelle angeben.

- Wenn Sie die Pipe ( `|` ) verwenden, können Sie diese Befehle wie **dir**, **Sort**und **Type**verwenden.

### <a name="examples"></a>Beispiele

Geben Sie einen der folgenden Befehle ein, um den ersten Bildschirm der Informationen einer Datei mit dem Namen *Clients. New*anzuzeigen:

```
more < clients.new
type clients.new | more
```

Der Befehl **Weitere** zeigt den ersten Bildschirm der Informationen von Clients. neu an, und Sie können die Leertaste drücken, um den nächsten Bildschirm anzuzeigen.

Geben Sie einen der folgenden Befehle ein, um den Bildschirm zu löschen und alle zusätzlichen leeren Zeilen vor dem Anzeigen der Datei *Clients. New*zu entfernen:

```
more /c /s < clients.new
type clients.new | more /c /s
```

Geben Sie Folgendes ein, um die aktuelle Zeilennummer an der **Eingabeaufforderung anzuzeigen** :

```
more =
```

**Der Eingabeaufforderung** wird die aktuelle Zeilennummer hinzugefügt.`-- More [Line: 24] --`

Geben Sie Folgendes ein, um eine bestimmte Anzahl von Zeilen an **der Eingabeaufforderung** anzuzeigen:

```
more p
```

Wenn Sie die Eingabeaufforderung anfordern, werden Sie wie folgt aufgefordert **, die Anzahl** der anzuzeigenden Zeilen anzuzeigen: `-- More -- Lines:` . Geben Sie die Anzahl der anzuzeigenden Zeilen ein, und drücken Sie dann die EINGABETASTE. Der Bildschirm wird so geändert, dass nur diese Anzahl von Zeilen angezeigt wird.

Um eine bestimmte Anzahl von Zeilen an der Eingabeaufforderung zu **über** springen, geben Sie Folgendes ein:

```
more s
```

Wenn Sie die Eingabeaufforderung anfordern, werden Sie wie folgt zur **Eingabe der Anzahl** der zu über springenden Zeilen aufgefordert: `-- More -- Lines:` . Geben Sie die Anzahl der zu über springenden Zeilen ein, und drücken Sie die EINGABETASTE. Der Bildschirm wird geändert, um anzuzeigen, dass diese Zeilen übersprungen werden.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
