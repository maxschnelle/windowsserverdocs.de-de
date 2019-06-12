---
title: find
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ca66b22-3b7c-4166-8503-eb75fc53ab46
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b13a2fe573ffc81fa5c85d8fd28e9ab13ca4342
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439341"
---
# <a name="find"></a>find



Sucht nach einer Textzeichenfolge in eine Datei oder Dateien, und zeigt Textzeilen, die die angegebene Zeichenfolge enthalten.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
find [/v] [/c] [/n] [/i] [/off[line]] "<String>" [[<Drive>:][<Path>]<FileName>[...]]
```

## <a name="parameters"></a>Parameter

|           Parameter           |                                              Beschreibung                                               |
|-------------------------------|--------------------------------------------------------------------------------------------------------|
|              /v               |                    Zeigt alle Zeilen, die nicht dem angegebenen enthalten \<Zeichenfolge >.                     |
|              /c               |              Zählt die Zeilen, die den angegebenen enthalten \<Zeichenfolge >, und zeigt die Summe.              |
|              /n               |                            Vor jede Zeile mit dem die Nummer der Zeile der Datei steht.                             |
|              /i               |                            Gibt an, dass es sich bei der Suche nicht beachtet werden.                            |
|         [/off[line]]          |                        Dateien, die das Attribut "offline" festgelegt ist, werden nicht übersprungen werden.                        |
|          "\<String>"          | Erforderlich. Gibt die Gruppe von Zeichen (in Anführungszeichen eingeschlossen), denen Sie suchen möchten. |
| [\<Drive>:][<Path>]<FileName> |        Gibt den Speicherort und Namen der Datei, in dem für die angegebene Zeichenfolge gesucht werden soll.        |
|              /?               |                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                  |

## <a name="remarks"></a>Hinweise

-   Eine Zeichenfolge anzugeben

    Wenn Sie nicht verwenden **/i**, **finden** sucht nach genau angeben *Zeichenfolge*. Z. B. die **finden** Befehl behandelt, die Zeichen "a" und "A" unterschiedlich. Bei Verwendung von **/i**jedoch **finden** nicht Groß-/ Kleinschreibung, und es behandelt "a" und "A" als dasselbe Zeichen.

    Wenn die Zeichenfolge, die Sie suchen möchten Anführungszeichen enthält, müssen Sie die doppelten Anführungszeichen verwenden, für jedes Anführungszeichen, die innerhalb der Zeichenfolge ("" "String" und"enthält beispielsweise Anführungszeichen").
-   Mithilfe von **finden** als Filter

    Wenn Sie einen Dateinamen ein, weglassen **finden** fungiert als Filter, nehmen Eingabe, aus der standardmäßigen Eingabequelle (in der Regel auf der Tastatur, einen senkrechten Strich (|) oder eine umgeleitete Datei) und zeigen Sie anschließend alle Zeilen, enthalten *Zeichenfolge*.
-   Reihenfolge der Befehlssyntax

    Können Sie eingeben, Parameter und den Befehlszeilenoptionen für die **finden** Befehl in beliebiger Reihenfolge.
-   Verwenden von Platzhaltern

    Können keine Platzhalter ( **&#42;** und **?** ) im Dateinamen oder Erweiterungen, die Sie angeben, mit der **finden** Befehl. Um nach einer Zeichenfolge in einen Satz von Dateien zu suchen, die Sie mit Platzhaltern angeben, können Sie die **finden** Befehl innerhalb einer **für** Befehl.
-   Mithilfe von **/v** oder **/n** mit   **/c**

    Bei Verwendung von **/c** und **/v** in der gleichen Befehlszeile **finden** zeigt die Anzahl der Zeilen, die nicht die angegebene Zeichenfolge enthalten. Bei Angabe von **/c** und **/n** in der gleichen Befehlszeile **finden** ignoriert **/n**.
-   Mithilfe von **finden** Wagenrücklauf zurückgibt

    Die **finden** Wagenrückläufe Befehl nicht erkannt. Bei Verwendung von **finden** um nach Text in einer Datei zu suchen, die harte Zeilenumbrüche enthält, müssen Sie begrenzen die Suchzeichenfolge für Text, der von Wagenrücklaufzeichen (d. h. eine Zeichenfolge, die nicht von einem Wagenrücklauf unterbrochen wird) befinden. Z. B. **finden** eine Übereinstimmung für die Zeichenfolge "Steuern der Datei" gibt keine Auskunft über ein Wagenrücklaufzeichen tritt zwischen den Wörtern "Tax" und "Datei".

## <a name="BKMK_examples"></a>Beispiele für

Um alle Zeilen aus Pencil.ad anzuzeigen, die die Zeichenfolge "Bleistiftspitzer" enthalten, geben Sie Folgendes ein:
```
find "Pencil Sharpener" pencil.ad
```
Um eine Zeichenfolge zu suchen, die Text in Anführungszeichen enthält, müssen Sie die gesamte Zeichenfolge in Anführungszeichen setzen. Dann müssen Sie zwei Anführungszeichen für jedes Anführungszeichen, die innerhalb der Zeichenfolge verwenden. "Die Zahnarzt"für nur Diskussion."gefunden. Es ist keinen abschließenden Bericht." Report.doc, Typ:
```
find "The scientists labeled their paper ""for discussion only."" It is not a final report." report.doc
```
Wenn Sie einen Satz von Dateien suchen möchten, können Sie mithilfe der **finden** Befehl innerhalb der **für** Befehl. Um das aktuelle Verzeichnis für Dateien zu suchen, die die Erweiterung enthalten bat- und, die den "PROMPT", String-Datentyp:
```
for %f in (*.bat) do find "PROMPT" %f 
```
Verwenden Sie zum Suchen Ihrer VHD-Datei zum Suchen und Anzeigen von Dateinamen auf Laufwerk C, die die Zeichenfolge "CPU" enthalten, den senkrechten Strich (|), leiten Sie die Ausgabe des der **Dir** Befehl die **finden** -Befehls wie folgt:
```
dir c:\ /s /b | find "CPU" 
```
Da **finden** Groß-/Kleinschreibung und **Dir** Ausgabe Großbuchstaben verwendet, müssen Sie entweder Geben Sie die Zeichenfolge "CPU" in Großbuchstaben oder der **/i** Befehlszeilen mit Option **finden**.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)