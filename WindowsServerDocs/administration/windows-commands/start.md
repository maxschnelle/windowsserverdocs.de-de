---
title: start
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ab7388633681120442544adf4ee0e337d8599854
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441224"
---
# <a name="start"></a>start



Startet, ein separates Fenster der Eingabeaufforderung den Befehl um ein Programm oder den Befehl auszuführen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
start ["<Title>"] [/d <Path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <HexAffinity>] [/wait] [/b {<Command> | <Program>} [<Parameters>]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|"\<Title>"|Gibt den Titel in der Titelleiste der Eingabeaufforderung-Fensters angezeigt.|
|/ d \<Pfad >|Gibt das Startverzeichnis an.|
|/i|Übergibt die Cmd.exe-Startumgebung, an der neuen Eingabeaufforderungsfenster. Wenn **/i** nicht angegeben ist, wird die aktuelle Umgebung verwendet wird.|
|/ Min  \| /max|Gibt an, dass zu minimieren ( **/min**) oder Maximieren ( **/Max.** ) der neuen Eingabeaufforderungsfenster.|
|/ separate \| / shared|16-Bit-Programme in einem separaten Speicher beginnt ( **/separate**) oder shared Memory-Speicher ( **/ shared**). Diese Optionen werden auf 64-Bit-Plattformen nicht unterstützt.|
|/ niedrige \| /normal \| /hoch \| /realtime \| /abovenormal \| /belownormal|Startet eine Anwendung in der angegebenen Priorität-Klasse. Gültige Priorität Klasse Werte **/niedrige**, **/normal**, **/hoch**, **/realtime**, **/abovenormal**, und **/belownormal**.|
|/affinity \<HexAffinity>|Wendet die angegebenen Prozessor-Affinitätsmaske (ausgedrückt als eine hexadezimale Zahl) für die neue Anwendung an.|
|/ Wait|Startet eine Anwendung und wartet darauf, um zu beenden.|
|/b|Startet eine Anwendung ohne ein neues Eingabeaufforderungsfenster zu öffnen. Behandlung von STRG + C wird ignoriert, es sei denn, die Anwendung über STRG + C-Verarbeitung ermöglicht. Verwenden Sie STRG + UNTBR, um die Anwendung zu unterbrechen.|
|/ b \<Befehl > \| \<Programm >|Gibt an, den Befehl oder das Programm zu starten.|
|\<Parameter >|Gibt an, an den Befehl oder das Programm zu übergebenden Parameter.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Sie können nicht ausführbare Dateien über ihre dateizuordnung ausführen, indem Sie den Namen der Datei als Befehl eingeben.
- Beim Ausführen eines Befehls, das die Zeichenfolge "CMD" enthält als das erste Token ohne einen Qualifizierer Erweiterung oder Pfad ist "CMD" durch den Wert für die PATHEXT ersetzt. Dadurch wird verhindert, dass Benutzer aufnahm **Cmd** aus dem aktuellen Verzeichnis.
- Wenn Sie eine 32-Bit-GUI-Benutzeroberfläche (GUI)-Anwendung ausführen **Cmd** wartet nicht für die Anwendung aus, um vor der Rückgabe an der Eingabeaufforderung zu beenden. Dieses Verhalten tritt nicht auf, wenn Sie die Anwendung aus einem Befehlsskript ausführen.
- Wenn Sie einen Befehl, der ein erstes Token verwendet, das keine Erweiterung enthält ausführen, verwendet Cmd.exe den Wert der Umgebungsvariablen PATHEXT, um zu bestimmen, welche Erweiterungen für und in welcher Reihenfolge suchen. Der Standardwert für die Path-Variable ist:  
  ```
  .COM;.EXE;.BAT;.CMD 
  ```  
  Beachten Sie, dass die Syntax der PATH-Variablen werden durch Semikolon getrennt jede Erweiterung identisch ist.
- Bei der Suche nach einer ausführbaren Datei, wenn es keine Übereinstimmung für alle Erweiterungen, **starten** überprüft, wenn der Name den Namen eines Verzeichnisses übereinstimmt. Wenn dies der Fall, **starten** Explorer.exe unter diesem Pfad geöffnet.

## <a name="BKMK_examples"></a>Beispiele für

Starten die Anwendung "MyApp" an der Eingabeaufforderung ein, und behalten die Verwendung des aktuellen Fensters der Eingabeaufforderung, geben Sie Folgendes ein:
```
start myapp 
```
Anzeigen der **starten** befehlszeilenhilfethema in einer separaten maximiert, Fenster "Eingabeaufforderung", Typ:
```
start /max start /?
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
