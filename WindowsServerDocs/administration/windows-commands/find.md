---
title: Suchen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca66b22-3b7c-4166-8503-eb75fc53ab46
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3cd731ef64912644965ef6bb96d060a46f0a6067
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725626"
---
# <a name="find"></a>Suchen



Sucht in einer Datei oder in Dateien nach einer Text Zeichenfolge und zeigt Textzeilen an, die die angegebene Zeichenfolge enthalten.



## <a name="syntax"></a>Syntax

```
find [/v] [/c] [/n] [/i] [/off[line]] <String> [[<Drive>:][<Path>]<FileName>[...]]
```

### <a name="parameters"></a>Parameter

|           Parameter           |                                              BESCHREIBUNG                                               |
|-------------------------------|--------------------------------------------------------------------------------------------------------|
|              /v               |                    Zeigt alle Zeilen an, die nicht die angegebene \<Zeichenfolge> enthalten.                     |
|              /C               |              Zählt die Zeilen, die die angegebene \<Zeichenfolge enthalten>und zeigt die Summe an.              |
|              /n               |                            Vor jeder Zeile mit der Zeilennummer der Datei.                             |
|              /i               |                            Gibt an, dass bei der Suche keine Groß-/Kleinschreibung beachtet wird                            |
|         [/OFF [Zeile]]          |                        Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist.                        |
|          \<Zeichen folgen>          | Erforderlich. Gibt die Gruppe von Zeichen (in Anführungszeichen eingeschlossen) an, nach denen Sie suchen möchten. |
| [\<Laufwerk>:] [<Path>]<FileName> |        Gibt den Speicherort und den Namen der Datei an, in der nach der angegebenen Zeichenfolge gesucht werden soll.        |
|              /?               |                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                  |

## <a name="remarks"></a>Bemerkungen

-   Angeben einer Zeichenfolge

    Wenn Sie **/i**nicht verwenden, suchen Sie nach genau den **Informationen** , die Sie für die *Zeichenfolge*angeben. Der **Find** -Befehl behandelt z. b. die Zeichen a und einen anders. Wenn Sie **/i**verwenden, wird bei der **Suche** die Groß-/Kleinschreibung jedoch nicht beachtet, und ein und ein werden als dasselbe Zeichen behandelt.

    Wenn die Zeichenfolge, nach der Sie suchen möchten, Anführungszeichen enthält, müssen Sie für jedes in der Zeichenfolge enthaltene Anführungszeichen doppelte Anführungszeichen verwenden (diese Zeichenfolge enthält z. b. Anführungszeichen).
-   Verwenden von " **Suchen** als Filter"

    Wenn Sie einen Dateinamen weglassen, wird die **Suche** als Filter durchgesetzt, wobei Eingaben aus der Standardeingabe Quelle (in der Regel die Tastatur, eine Pipe (|) oder eine umgeleitete Datei) und dann alle Zeilen angezeigt werden, die eine *Zeichenfolge*enthalten.
-   Reihenfolge Befehlssyntax

    Sie können Parameter und Befehlszeilenoptionen **für den Befehl Suchen in** beliebiger Reihenfolge eingeben.
-   Verwenden von Platzhaltern

    Sie können keine Platzhalter (**&#42;** und **?**) in Dateinamen oder Erweiterungen verwenden, die Sie mit dem Befehl **Suchen** angeben. Wenn Sie in einem Satz von Dateien, die Sie mit Platzhaltern angeben, nach einer Zeichenfolge suchen möchten, können **Sie den Befehl** suchen in einem **for** -Befehl verwenden.
-   Verwenden von **/v** oder **/n** mit **/c**

    Wenn Sie **/c** und **/v** in derselben Befehlszeile verwenden, zeigt **Find** die Anzahl der Zeilen an, die die angegebene Zeichenfolge nicht enthalten. Wenn Sie " **/c** " und " **/n** " in derselben Befehlszeile angeben, ignoriert " **Find** " **/n**.
-   Verwenden von " **Find** with Wagen Returns"

    Der **Find** -Befehl erkennt keine Wagen Rückläufe. Wenn Sie suchen **verwenden,** um in einer Datei, die Wagen Rückläufe enthält, nach Text zu suchen, müssen Sie die Such Zeichenfolge auf Text beschränken, der Zwischenwagen Rückgaben (d. h. eine Zeichenfolge, die wahrscheinlich nicht durch einen Wagen Rücklauf unterbrochen wird) gefunden wird. Beispielsweise meldet **Find** keine Entsprechung für die Zeichen folgen-Steuerdatei, wenn ein Wagen Rücklauf zwischen den Wörtern "Tax" und "file" auftritt.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Zeilen aus Pencil.AD anzuzeigen, die den zeichenfolgenstift-schärzer enthalten
```
find Pencil Sharpener pencil.ad
```
Um eine Zeichenfolge zu suchen, die Text in Anführungszeichen enthält, müssen Sie die gesamte Zeichenfolge in Anführungszeichen einschließen. Anschließend müssen Sie für jedes in der Zeichenfolge enthaltene Anführungszeichen zwei Anführungszeichen verwenden. Zum Ermitteln der Analysten mit der Bezeichnung für die Diskussion. Es handelt sich nicht um einen abschließenden Bericht. Geben Sie in "Report. doc" Folgendes ein:
```
find The scientists labeled their paper for discussion only. It is not a final report. report.doc
```
Wenn Sie nach einem Satz von Dateien suchen möchten, können Sie den Befehl Suchen **im Befehl** **for** verwenden. Geben Sie Folgendes ein, um das aktuelle Verzeichnis nach Dateien mit der Erweiterung. bat zu durchsuchen, die die Eingabe Zeichenfolge enthalten:
```
for %f in (*.bat) do find PROMPT %f 
```
Um die Festplatte zum Suchen und Anzeigen der Dateinamen auf Laufwerk C zu suchen, die die Zeichenfolge-CPU enthalten, verwenden Sie die Pipe (|), um die Ausgabe des **dir** -Befehls wie folgt an den **Suchbefehl weiterzuleiten** :
```
dir c:\ /s /b | find CPU 
```
Da **bei** Such Suchvorgängen die Groß-/Kleinschreibung beachtet wird und **dir** die Großbuchstaben Ausgabe erzeugt, müssen Sie entweder die Zeichen folgen-CPU in Großbuchstaben eingeben oder die Befehlszeilenoption **/i** with **Find**verwenden.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)