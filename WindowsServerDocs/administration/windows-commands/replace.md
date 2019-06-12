---
title: replace
description: Erfahren Sie, wie Sie den Befehl "ersetzen" verwenden, um Dateien zu ersetzen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143661e-d90f-4812-b265-6669b567dd1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 293534a2287fe0219643dacc88926018c37dbdcc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441776"
---
# <a name="replace"></a>replace



Dateien werden ersetzt. Bei Verwendung mit der **/a** Option **ersetzen** fügt neue Dateien in ein Verzeichnis anstelle von vorhandenen Dateien zu ersetzen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/a] [/p] [/r] [/w] 
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/p] [/r] [/s] [/w] [/u] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk1 >:] [\<Path1 >]\<Dateiname >|Gibt den Speicherort und Namen der Quelldatei oder Satz von Dateien. *FileName* ist erforderlich und kann Platzhalterzeichen enthalten ( **&#42;** und **?** ).|
|[\<Laufwerk2 >:] [\<Path2 >]|Gibt den Speicherort der Zieldatei. Sie können keinen Dateinamen für die Dateien angeben, die Sie ersetzen. Wenn Sie kein Laufwerk oder einen Pfad angeben **ersetzen** verwendet das aktuelle Laufwerk und Verzeichnis als Ziel.|
|/a|Fügt neue Dateien in das Zielverzeichnis, anstatt zu vorhandene Dateien zu ersetzen. Sie können keine diese Befehlszeilenoption mit der **/s** oder **/u** Befehlszeilenoption.|
|/p|Fordert Sie zur Bestätigung vor dem Ersetzen einer Zieldatei oder das Hinzufügen einer Quelldatei.|
|/r|Nur-Lese und ungeschützte Dateien ersetzt. Wenn Sie versuchen, eine schreibgeschützte Datei zu ersetzen, aber Sie keinen **/r**, Fehler führt, und der Vorgang gestoppt.|
|/w|Wartet, bis Sie einen Datenträger einzulegen, vor Beginn der Suche nach Quelldateien. Wenn Sie keinen angeben **/w**, **ersetzen** ersetzen oder Hinzufügen von Dateien beginnt, sobald Sie die EINGABETASTE drücken.|
|/s|Durchsucht alle Unterverzeichnisse im Zielverzeichnis und ersetzt die entsprechenden Dateien. Sie können keine **/s** mit der **/a** Befehlszeilenoption. Die **ersetzen** Befehl sucht nicht Unterverzeichnisse, die im angegebenen *Path1*.|
|/u|Ersetzt nur die Dateien in das Zielverzeichnis, die älter als die des Quellverzeichnisses an. Sie können keine **/u** mit der **/a** Befehlszeilenoption.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Als **ersetzen** fügt hinzu oder ersetzt Sie Dateien, die Datei mit dem Namen auf dem Bildschirm angezeigt werden. Nach dem **ersetzen** fertig gestellt wurde, wird eine Zusammenfassungszeile angezeigt, in einem der folgenden Formate:  
  ```
  nnn files added
  nnn files replaced
  no file added
  no file replaced
  ```  
- Wenn Sie Disketten verwenden, und Sie zum Wechseln der Datenträger während müssen der **ersetzen** -Vorgang können Sie angeben der **/w** Befehlszeilenoption, damit **ersetzen** wartet Sie Wechseln Sie die Datenträger.
- Sie können keine **ersetzen** , ausgeblendete Dateien oder Systemdateien zu aktualisieren.
- Die folgende Tabelle zeigt alle Exitcodes und eine Kurzbeschreibung ihrer Bedeutung:  
  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Die **ersetzen** Befehl wurde erfolgreich ersetzt, oder die Dateien hinzugefügt.|
  |1|Die **ersetzen** Befehl hat eine falsche Version von MS-DOS-festgestellt.|
  |2|Die **ersetzen** Befehl die Quelldateien nicht gefunden.|
  |3|Die **ersetzen** Befehl den Quelle oder Ziel-Pfad nicht gefunden.|
  |5|Der Benutzer ist nicht auf die Dateien zugreifen, die Sie ersetzen möchten.|
  |8|Es ist nicht genügend Systemarbeitsspeicher zum Ausführen des Befehls.|
  |11|Der Benutzer verwendet die falsche Syntax in der Befehlszeile an.|

> [!NOTE]
> Sie können die ERRORLEVEL-Parameter verwenden, auf die **Wenn** Befehlszeile in einem Batchprogramm zum Verarbeiten von Exitcodes, die von zurückgegeben werden **ersetzen**.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie Folgendes ein, um alle Versionen einer Datei mit dem Namen Telefon.kun (die in mehreren Verzeichnissen auf Laufwerk C angezeigt), mit der neuesten Version der Datei Telefon.kun von einer Diskette in Laufwerk A zu aktualisieren:

`replace a:\phones.cli c:\ /s`

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)