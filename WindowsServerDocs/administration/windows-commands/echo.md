---
title: echo
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfe6c936ee5606e286aab076bea08db04b8b6500
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811163"
---
# <a name="echo"></a>echo



Zeigt an, oder aktiviert oder deaktiviert den Befehl wiederholen-Funktion. Wenn Sie ohne Angabe von Parametern **Echo** zeigt die aktuelle Einstellung für den Echo.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
echo [<Message>]
echo [on | off]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[auf \| deaktiviert]|Aktiviert oder deaktiviert den Befehl mit dem Feature ausgeben. Befehlsanzeige ist standardmäßig aktiviert.|
|\<Meldung >|Gibt den Text auf dem Bildschirm angezeigt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **Echo** *Nachricht* Befehl ist besonders nützlich, wenn **Echo** ist deaktiviert. Eine Meldung angezeigt, die mehrere Zeilen lang ist, ohne dass alle Befehle, Sie können enthalten mehrere **Echo** *Nachricht* Befehle nach der **echo deaktiviert** Befehl in Ihrer Batch-Anwendung.
-   Wenn **Echo** deaktiviert ist, die Eingabeaufforderung wird im Eingabeaufforderungsfenster Befehl nicht angezeigt. Geben Sie zum Anzeigen der Eingabeaufforderung **echo auf.**
-   Wenn in einer Batchdatei verwendet **auf echo** und **echo deaktiviert** wirken sich nicht auf die Einstellung an der Eingabeaufforderung.
-   Um zu verhindern, einen bestimmten Befehl in einer Batchdatei ausgeben, fügen Sie ein at-Zeichen (@) vor dem Befehl. Um zu verhindern, dass alle Befehle in einer Batchdatei ausgeben, enthalten die **echo deaktiviert** Befehl am Anfang der Datei.
-   Zum Anzeigen einer Pipes ( **|** ) oder Umleitungszeichen ( **<** oder **>** ) bei Verwendung **Echo**, verwenden Sie ein Caretzeichen (^) unmittelbar vor dem Zeichen Pipe oder einer Umleitung (beispielsweise **^|** , **^>** , oder **^<** ). Geben Sie zum Anzeigen einer Einfügemarke in Folge zwei Caretzeichen ( **^^** ).

## <a name="examples"></a>Beispiele

Zeigt das aktuelle **Echo** Einstellung:

```
echo
```

Um eine leere Zeile auf dem Bildschirm wiederzugeben, geben Sie Folgendes ein:

```
echo.
```

> [!NOTE]
> Fügen Sie vor dem Punkt kein Leerzeichen ein. Andernfalls wird die Periode anstelle einer leeren Zeile angezeigt.

Um zu verhindern, dass Anzeigen von Befehlen an der Eingabeaufforderung, geben:

```
echo off 
```

> [!NOTE]
> Wenn **Echo** deaktiviert ist, die Eingabeaufforderung wird im Eingabeaufforderungsfenster Befehl nicht angezeigt. Um die Befehlszeile erneut anzuzeigen, geben **auf echo**.

Um zu verhindern, dass alle Befehle in einer Batchdatei (einschließlich der **echo deaktiviert** Befehl) auf dem Bildschirm, in der ersten Zeile des Dateityps Batch angezeigt:

```
@echo off
```

Können Sie die **Echo** Befehl als Teil einer **Wenn** Anweisung. Z. B. um das aktuelle Verzeichnis für jede Datei mit der Erweiterung. rpt und zur Wiedergabe einer Nachricht zu suchen, wenn eine solche Datei gefunden wird, geben Sie ein:

```
if exist *.rpt echo The report has arrived.
```

Die folgende Batchdatei durchsucht das aktuelle Verzeichnis für Dateien mit der Dateinamenerweiterung %% amp;quot;.txt%%amp;quot; und zeigt eine Meldung angezeigt, die Ergebnisse der Suche:

```
@echo off
if not exist *.txt (
echo This directory contains no text files.
) else (
   echo This directory contains the following text files:
   echo.
   dir /b *.txt
   )
```

Wenn keine TXT-Dateien gefunden werden, wenn die Batchdatei ausgeführt wird, wird die folgende Meldung angezeigt:

```
This directory contains no text files.
```

Die folgende Ausgabe zeigt an, wenn TXT-Dateien gefunden werden, wenn die Batchdatei ausgeführt wird (in diesem Beispiel gehen Sie die Dateien File1.txt und File2.txt, File3.txt vorhanden sind):

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
