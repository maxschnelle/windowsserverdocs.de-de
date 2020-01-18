---
title: Start
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0173f9b3-5cd7-4edb-b01e-d02193b4fadc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 48197b1bc1d1c9f91a6a35b5fb8aad81b229eb6b
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259085"
---
# <a name="start"></a>Start



Startet ein separates Eingabe Aufforderungs Fenster, um ein angegebenes Programm oder einen Befehl auszuführen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
start ["<Title>"] [/d <Path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <HexAffinity>] [/wait] [/elevate] [/b] [<Command> [<Parameter>... ] | <Program> [<Parameter>... ]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|"\<Titel >"|Gibt den Titel an, der in der Titelleiste des Eingabe Aufforderungs Fensters angezeigt werden soll.|
|/d \<Pfad >|Gibt das Start Verzeichnis an.|
|/i|Übergibt die Start Umgebung "cmd. exe" an das neue Eingabe Aufforderungs Fenster. Wenn **/i** nicht angegeben ist, wird die aktuelle Umgebung verwendet.|
|/min \|/Max|Gibt an, dass das neue Eingabe Aufforderungs Fenster minimiert ( **/Min**) oder maximiert ( **/Max**) werden soll.|
|/separate \|/Shared|Startet 16-Bit-Programme in einem separaten Speicherbereich ( **/separate**) oder gemeinsam genutzten Speicherplatz ( **/Shared**). Diese Optionen werden auf 64-Bit-Plattformen nicht unterstützt.|
|/Low \|/normal \|/High \|/Realtime \|/AboveNormal \|/BelowNormal|Startet eine Anwendung in der angegebenen Prioritäts Klasse. Gültige Werte für die Prioritäts Klasse sind **/Low**, **/Normal**, **/High**, **/Realtime**, **/AboveNormal**und **/BelowNormal**.|
|/Affinity \<hexaffinitäts >|Wendet die angegebene Prozessor Affinitäts Maske (als hexadezimal Zahl ausgedrückt) auf die neue Anwendung an.|
|/wait|Startet eine Anwendung und wartet darauf, dass Sie beendet wird.|
|/elevate|Führt die Anwendung als Administrator aus.|
|/b|Startet eine Anwendung, ohne ein neues Eingabe Aufforderungs Fenster zu öffnen. Strg + c-Behandlung wird ignoriert, es sei denn, die Anwendung aktiviert die Strg + c-Verarbeitung. Verwenden Sie Strg + Pause, um die Anwendung zu unterbrechen.|
|\<Befehls > \| \<Programm >|Gibt den zu Startbefehl oder das Programm an.|
|\<Parameter >...|Gibt Parameter an, die an den Befehl oder das Programm übergeben werden sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Sie können nicht ausführbare Dateien durch Ihre Datei Zuordnung ausführen, indem Sie den Namen der Datei als Befehl eingeben.
- Wenn Sie einen Befehl ausführen, der die Zeichenfolge "cmd" als erstes Token ohne Erweiterung oder Pfad Qualifizierer enthält, wird "cmd" durch den Wert der COMSPEC-Variablen ersetzt. Dadurch wird verhindert, dass Benutzer **cmd** aus dem aktuellen Verzeichnis auswählen.
- Wenn Sie eine GUI-Anwendung (32-Bit Graphical User Interface) ausführen, wartet **cmd** nicht, bis die Anwendung beendet wird, bevor Sie zur Eingabeaufforderung zurückkehrt. Dieses Verhalten tritt nicht auf, wenn Sie die Anwendung über ein Befehls Skript ausführen.
- Wenn Sie einen Befehl ausführen, der ein erstes Token verwendet, das keine Erweiterung enthält, verwendet cmd. exe den Wert der Umgebungsvariablen PATHEXT, um zu bestimmen, welche Erweiterungen nach und in welcher Reihenfolge gesucht werden sollen. Der Standardwert für die PATHEXT-Variable lautet:  
  ```
  .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC 
  ```  
  Beachten Sie, dass die Syntax mit der PATH-Variablen identisch ist, wobei die einzelnen Erweiterungen durch Semikolons getrennt werden.
- Wenn bei der Suche nach einer ausführbaren Datei keine Übereinstimmung mit einer Erweiterung vorhanden ist, prüft **Start** , ob der Name mit einem Verzeichnisnamen übereinstimmt. Wenn dies der Fall ist **, öffnen Sie** "Explorer. exe" für diesen Pfad.

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um das Programm MyApp an der Eingabeaufforderung zu starten und die Verwendung des aktuellen Eingabe Aufforderungs Fensters beizubehalten:
```
start myapp 
```
Geben Sie Folgendes ein, um das Hilfethema **Start** Befehlszeile in einem separaten, maximierten Eingabe Aufforderungs Fenster anzuzeigen:
```
start /max start /?
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
