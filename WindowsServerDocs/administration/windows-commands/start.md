---
title: start
description: Referenz Artikel für den Start-Befehl, der ein separates Eingabe Aufforderungs Fenster startet, um ein angegebenes Programm oder einen Befehl auszuführen.
ms.topic: reference
ms.assetid: 0173f9b3-5cd7-4edb-b01e-d02193b4fadc
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6c154cd0c3cab4520f64c77d2ecc920dfc8bdcc9
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718267"
---
# <a name="start"></a>start

Startet ein separates Eingabe Aufforderungs Fenster, um ein angegebenes Programm oder einen Befehl auszuführen.

## <a name="syntax"></a>Syntax

```
start [<title>] [/d <path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <hexaffinity>] [/wait] [/elevate] [/b] [<command> [<parameter>... ] | <program> [<parameter>... ]]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<title>` | Gibt den Titel an, der in der Titelleiste des **Eingabe** Aufforderungs Fensters angezeigt werden soll. |
| /d `<path>` | Gibt das Start Verzeichnis an. |
| /i | Übergibt die Cmd.exe Start Umgebung an das neue **Eingabe** Aufforderungs Fenster. Wenn **/i** nicht angegeben ist, wird die aktuelle Umgebung verwendet. |
| `{/min | /max}` | Gibt an, dass das neue **Eingabe** Aufforderungs Fenster minimiert (**/Min**) oder maximiert (**/Max**) werden soll. |
| `{/separate | /shared}` | Startet 16-Bit-Programme in einem separaten Speicherbereich (**/separate**) oder gemeinsam genutzten Speicherplatz (**/Shared**). Diese Optionen werden auf 64-Bit-Plattformen nicht unterstützt. |
| `{/low | /normal | /high | /realtime | /abovenormal | belownormal}` | Startet eine Anwendung in der angegebenen Prioritäts Klasse. |
| /affinity `<hexaffinity>` | Wendet die angegebene Prozessor Affinitäts Maske (als hexadezimal Zahl ausgedrückt) auf die neue Anwendung an. |
| /Wait | Startet eine Anwendung und wartet darauf, dass Sie beendet wird. |
| /elevate | Führt die Anwendung als Administrator aus. |
| /b | Startet eine Anwendung, ohne ein neues **Eingabe** Aufforderungs Fenster zu öffnen. Strg + c-Behandlung wird ignoriert, es sei denn, die Anwendung aktiviert die Strg + c-Verarbeitung. Verwenden Sie Strg + Pause, um die Anwendung zu unterbrechen. |
| `[<command> [<parameter>... ] | <program> [<parameter>... ]]` | Gibt den zu Startbefehl oder das Programm an. |
| `<parameter>` | Gibt Parameter an, die an den Befehl oder das Programm übergeben werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Sie können nicht ausführbare Dateien über Ihre Datei Zuordnung ausführen, indem Sie den Namen der Datei als Befehl eingeben.

- Wenn Sie einen Befehl ausführen, der die Zeichenfolge cmd als erstes Token ohne Erweiterung oder Pfad Qualifizierer enthält, wird cmd durch den Wert der COMSPEC-Variablen ersetzt. Dadurch wird verhindert, dass Benutzer **cmd** aus dem aktuellen Verzeichnis auswählen.

- Wenn Sie eine GUI-Anwendung (32-Bit Graphical User Interface) ausführen, wartet **cmd** nicht darauf, dass die Anwendung beendet wird, bevor Sie zur Eingabeaufforderung zurückkehrt. Dieses Verhalten tritt nicht auf, wenn Sie die Anwendung über ein Befehls Skript ausführen.

- Wenn Sie einen Befehl ausführen, der ein erstes Token verwendet, das keine Erweiterung enthält, verwendet Cmd.exe den Wert der Umgebungsvariablen PATHEXT, um zu bestimmen, welche Erweiterungen nach und in welcher Reihenfolge gesucht werden sollen. Der Standardwert für die PATHEXT-Variable lautet:

  ```
  .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
  ```

  Beachten Sie, dass die Syntax mit der PATH-Variablen identisch ist, mit Semikolons (;) Trennen der einzelnen Erweiterungen.

- Wenn bei der Suche nach einer ausführbaren Datei keine Übereinstimmung mit einer Erweiterung vorhanden ist, prüft **Start** , ob der Name mit einem Verzeichnisnamen übereinstimmt. Wenn dies der Fall ist, wird **starten** geöffnet Explorer.exe für diesen Pfad.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Programm *myapp* an der Eingabeaufforderung zu starten und die Verwendung des aktuellen **Eingabe** Aufforderungs Fensters beizubehalten:

```
start Myapp
```

Geben Sie Folgendes ein, um das Hilfethema **Start** Befehlszeile in einem separaten, maximierten **Eingabe** Aufforderungs Fenster anzuzeigen:

```
start /max start /?
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
