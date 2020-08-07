---
title: Echo
description: Referenz Artikel für den Befehl echo, der Nachrichten anzeigt oder das Befehls Echo Feature aktiviert oder deaktiviert.
ms.topic: article
ms.assetid: fb9fcd0f-5e73-4504-aa95-78204e1a79d3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff1b196a26b43eb51d5da613e0ac596d26c65d05
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890725"
---
# <a name="echo"></a>Echo

Zeigt Meldungen an oder aktiviert oder deaktiviert die Funktion zum Wiederholen von Befehlen. Bei Verwendung ohne Parameter zeigt **Echo** die aktuelle ECHO-Einstellung an.

## <a name="syntax"></a>Syntax

```
echo [<message>]
echo [on | off]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [ein \| ] | Aktiviert oder deaktiviert die Funktion zum Wiederholen von Befehlen. Die Befehls Echo Prüfung ist standardmäßig aktiviert. |
| `<message>` | Gibt den Text an, der auf dem Bildschirm angezeigt werden soll. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Der `echo <message>` Befehl ist besonders nützlich, wenn **Echo** ausgeschaltet ist. Um eine Meldung anzuzeigen, die mehrere Zeilen lang ist, ohne Befehle anzuzeigen, können Sie mehrere `echo <message>` Befehle nach dem Befehl **echo off** in das Batch-Programm einschließen.

- Wenn **Echo** ausgeschaltet ist, wird die Eingabeaufforderung nicht im Eingabe Aufforderungs Fenster angezeigt. Geben Sie **Echo on** ein, um die Eingabeaufforderung anzuzeigen.

- Wenn Sie in einer Batchdatei verwendet werden, wirkt sich **Echo on** und **echo off** nicht auf die Einstellung an der Eingabeaufforderung aus.

- Um zu verhindern, dass ein bestimmter Befehl in einer Batchdatei wiederholt wird, fügen Sie eine `@` Anmeldung vor dem Befehl ein. Um zu verhindern, dass alle Befehle in einer Batchdatei wiedergegeben werden, schließen Sie den Befehl **echo off** am Anfang der Datei ein.

- Um eine Pipe ( `|` ) oder ein Umleitungs Zeichen ( `<` oder) anzuzeigen `>` , wenn Sie **Echo**verwenden, verwenden Sie eine Einfügemarke ( `^` ) direkt vor der Pipe oder dem Umleitungs Zeichen. Beispielsweise, `^|` `^>` oder `^<` ). Wenn Sie ein Caretzeichen anzeigen möchten, geben Sie zwei Einfügemarke in Folge ( `^^` ) ein.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle **Echo** Einstellung anzuzeigen:

```
echo
```

Geben Sie Folgendes ein, um eine leere Zeile auf dem Bildschirm wiederzugeben:

```
echo.
```

> [!NOTE]
> Fügen Sie vor dem-Zeitraum kein Leerzeichen ein. Andernfalls wird der Zeitraum anstelle einer leeren Zeile angezeigt.

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

Wenn txt-Dateien beim Ausführen der Batchdatei gefunden werden, wird die folgende Ausgabe angezeigt (in diesem Beispiel wird davon ausgegangen, dass die Dateien File1.txt, File2.txt und File3.txt vorhanden sind):

```
This directory contains the following text files:
File1.txt
File2.txt
File3.txt
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
