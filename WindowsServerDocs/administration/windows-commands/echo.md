---
title: echo
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e6e9c3c79cc8006efba0c97a574e3d6d94a6f7e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845243"
---
# <a name="echo"></a>echo



Zeigt Meldungen an oder aktiviert oder deaktiviert die Funktion zum Wiederholen von Befehlen. Bei Verwendung ohne Parameter zeigt **Echo** die aktuelle ECHO-Einstellung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
echo [<Message>]
echo [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[on \| off]|Aktiviert oder deaktiviert die Funktion zum Wiederholen von Befehlen. Die Befehls Echo Prüfung ist standardmäßig aktiviert.|
|\<Meldung >|Gibt den Text an, der auf dem Bildschirm angezeigt werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Der Befehl **Echo** *Message* ist besonders nützlich, wenn **Echo** deaktiviert ist. Um eine Meldung anzuzeigen, die mehrere Zeilen lang ist, ohne Befehle anzuzeigen, können Sie nach dem Befehl **echo off** im Batch Programm mehrere **Echo** *Message* -Befehle einschließen.
-   Wenn **Echo** ausgeschaltet ist, wird die Eingabeaufforderung nicht im Eingabe Aufforderungs Fenster angezeigt. Geben Sie **Echo on** ein, um die Eingabeaufforderung anzuzeigen.
-   Wenn Sie in einer Batchdatei verwendet werden, haben **Echo on** und **echo off** keine Auswirkung auf die Einstellung an der Eingabeaufforderung.
-   Um zu verhindern, dass ein bestimmter Befehl in einer Batchdatei wiederholt wird, fügen Sie vor dem Befehl ein @-Zeichen ein. Um zu verhindern, dass alle Befehle in einer Batchdatei wiedergegeben werden, schließen Sie den Befehl **echo off** am Anfang der Datei ein.
-   Um eine Pipe ( **|** ) oder ein Umleitungs Zeichen ( **<** oder **>** ) anzuzeigen, wenn Sie **Echo**verwenden, verwenden Sie ein Caretzeichen (^) direkt vor der Pipe oder dem Umleitungs Zeichen (z. b. **^|** , **^>** oder **^<** ). Zum Anzeigen einer Einfügemarke geben Sie zwei Einfügemarke in Folge ( **^^** ) ein.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle **Echo** Einstellung anzuzeigen:

```
echo
```

Geben Sie Folgendes ein, um eine leere Zeile auf dem Bildschirm wiederzugeben:

```
echo.
```

> [!NOTE]
> Fügen Sie kein Leerzeichen vor dem Zeitraum ein. Andernfalls wird der Zeitraum anstelle einer leeren Zeile angezeigt.

Geben Sie Folgendes ein, um das Echo von Befehlen an der Eingabeaufforderung zu verhindern:

```
echo off 
```

> [!NOTE]
> Wenn **Echo** ausgeschaltet ist, wird die Eingabeaufforderung nicht im Eingabe Aufforderungs Fenster angezeigt. Geben Sie **Echo on**ein, um die Eingabeaufforderung erneut anzuzeigen.

Um zu verhindern, dass alle Befehle in einer Batchdatei (einschließlich des Befehls **echo off** ) auf dem Bildschirm angezeigt werden, geben Sie in der ersten Zeile der Batchdatei Folgendes ein:

```
@echo off
```

Sie können den **Echo** -Befehl als Teil einer **if** -Anweisung verwenden. Wenn Sie z. b. das aktuelle Verzeichnis nach einer Datei mit der Dateinamenerweiterung ". rpt" Durchsuchen und eine Nachricht mit einer solchen Datei wiedergeben möchten, geben Sie Folgendes ein:

```
if exist *.rpt echo The report has arrived.
```

Die folgende Batchdatei durchsucht das aktuelle Verzeichnis nach Dateien mit der Dateinamenerweiterung ". txt" und zeigt eine Meldung an, die die Ergebnisse der Suche anzeigt:

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

Wenn beim Ausführen der Batchdatei keine txt-Dateien gefunden werden, wird die folgende Meldung angezeigt:

```
This directory contains no text files.
```

Wenn txt-Dateien beim Ausführen der Batchdatei gefunden werden, wird die folgende Ausgabe angezeigt (in diesem Beispiel wird angenommen, dass die Dateien file1. txt, file2. txt und datei3. txt vorhanden sind):

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
