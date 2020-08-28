---
title: Suchen
description: Referenz Artikel für den Find-Befehl, der nach einer Text Zeichenfolge in Dateien sucht und die angegebene Text Zeichenfolge in der Datei anzeigt.
ms.topic: reference
ms.assetid: 2ca66b22-3b7c-4166-8503-eb75fc53ab46
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34eb1f1cf3071147878f421307a91de921678cfc
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036537"
---
# <a name="find"></a>Suchen

Sucht in einer Datei oder in Dateien nach einer Text Zeichenfolge und zeigt Textzeilen an, die die angegebene Zeichenfolge enthalten.

## <a name="syntax"></a>Syntax

```
find [/v] [/c] [/n] [/i] [/off[line]] <string> [[<drive>:][<path>]<filename>[...]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /v | Zeigt alle Zeilen an, die das angegebene nicht enthalten `<string>` . |
| /C | Zählt die Zeilen, die das angegebene enthalten, `<string>` und zeigt die Summe an. |
| /n | Vor jeder Zeile mit der Zeilennummer der Datei. |
| /i | Gibt an, dass bei der Suche keine Groß-/Kleinschreibung beachtet wird |
| [/OFF [Zeile]] | Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist. |
| `<string>` | Erforderlich. Gibt die Gruppe von Zeichen (in Anführungszeichen eingeschlossen) an, nach denen Sie suchen möchten. |
| `[<drive>:][<path>]<filename>` | Gibt den Speicherort und den Namen der Datei an, in der nach der angegebenen Zeichenfolge gesucht werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie **/i**nicht verwenden, sucht dieser Befehl nach genau dem, was Sie für die *Zeichenfolge*angeben. Dieser Befehl behandelt z. b. die Zeichen `a` und `A` anders. Wenn Sie **/i**verwenden, wird die Suche jedoch nicht zwischen Groß-und Kleinschreibung unterschieden, und Sie behandelt `a` und `A` als dasselbe Zeichen.

- Wenn die Zeichenfolge, nach der Sie suchen möchten, Anführungszeichen enthält, müssen Sie für jedes in der Zeichenfolge enthaltene Anführungszeichen doppelte Anführungszeichen verwenden (z. b. "" diese Zeichenfolge enthält Anführungszeichen "").

- Wenn Sie einen Dateinamen weglassen, fungiert dieser Befehl als Filter und übernimmt Eingaben aus der Standardeingabe Quelle (normalerweise die Tastatur, eine Pipe (|) oder eine umgeleitete Datei) und zeigt dann alle Zeilen an, die eine *Zeichenfolge*enthalten.

- Sie können Parameter und Befehlszeilenoptionen **für den Befehl Suchen in** beliebiger Reihenfolge eingeben.

- Sie können keine Platzhalter (**&#42;** und **?**) in Dateinamen oder Erweiterungen verwenden, die Sie bei der Verwendung dieses Befehls angeben. Wenn Sie in einem Satz von Dateien, die Sie mit Platzhaltern angeben, nach einer Zeichenfolge suchen möchten, können Sie diesen Befehl in einem **for** -Befehl verwenden.

- Wenn Sie **/c** und **/v** in derselben Befehlszeile verwenden, zeigt dieser Befehl die Anzahl der Zeilen an, die die angegebene Zeichenfolge nicht enthalten. Wenn Sie " **/c** " und " **/n** " in derselben Befehlszeile angeben, ignoriert " **Find** " **/n**.

- Mit diesem Befehl werden Wagen Rückläufe nicht erkannt. Wenn Sie diesen Befehl verwenden, um in einer Datei, die Wagen Rückläufe enthält, nach Text zu suchen, müssen Sie die Such Zeichenfolge auf Text beschränken, der Zwischenwagen Rückgaben (d. h. eine Zeichenfolge, die wahrscheinlich nicht durch einen Wagen Rücklauf unterbrochen wird) gefunden wird. Beispielsweise meldet dieser Befehl keine Entsprechung für die Zeichen folgen-Steuerdatei, wenn ein Wagen Rücklauf zwischen den Wörtern "Tax" und "file" auftritt.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Zeilen aus *Pencil.AD* anzuzeigen, die den zeichenfolgenstift- *schärzer*enthalten

```
find pencil sharpener pencil.ad
```

Um den Text zu finden, "die Analysten haben das jeweilige Papier zur Diskussion geführt. Es handelt sich nicht um einen abschließenden Bericht. " Geben Sie in der *report.doc* -Datei Folgendes ein:

```
find ""The scientists labeled their paper for discussion only. It is not a final report."" report.doc
```

Wenn Sie nach einem Satz von Dateien suchen möchten, können Sie **den Befehl Suchen im Befehl** **for** verwenden. Geben Sie Folgendes ein, um das aktuelle Verzeichnis nach Dateien mit der Erweiterung. bat zu durchsuchen, die die Eingabe Zeichenfolge enthalten:

```
for %f in (*.bat) do find PROMPT %f
```

Um die Festplatte zum Suchen und Anzeigen der Dateinamen auf Laufwerk C zu suchen, die die Zeichenfolge-CPU enthalten, verwenden Sie die Pipe (|), um die Ausgabe des **dir** -Befehls wie folgt an den **Suchbefehl weiterzuleiten** :

```
dir c:\ /s /b | find CPU
```

Da **bei** Such Suchvorgängen die Groß-/Kleinschreibung beachtet wird und **dir** die Großbuchstaben Ausgabe erzeugt, müssen Sie entweder die Zeichen folgen-CPU in Großbuchstaben eingeben oder die Befehlszeilenoption **/i** with **Find**verwenden.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [for-Befehl](for.md)