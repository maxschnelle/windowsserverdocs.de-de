---
title: replace
description: Erfahren Sie, wie Sie den Replace-Befehl verwenden, um Dateien zu ersetzen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6143661e-d90f-4812-b265-6669b567dd1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d44e4f8383a77582177f4d9b161210207ce46e63
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835903"
---
# <a name="replace"></a>replace



Ersetzt Dateien. Bei Verwendung mit der Option **/a** fügt **Replace** neue Dateien zu einem Verzeichnis hinzu, anstatt vorhandene Dateien zu ersetzen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/a] [/p] [/r] [/w] 
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/p] [/r] [/s] [/w] [/u] 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive1 >:] [\<Path1 >]\<Dateiname >|Gibt den Speicherort und den Namen der Quelldatei oder des Satzes von Dateien an. *Dateiname* ist erforderlich und kann Platzhalter Zeichen **&#42;** (und **?** ) enthalten.|
|[\<drive2 >:] [\<Path2 >]|Gibt den Speicherort der Zieldatei an. Sie können keinen Dateinamen für die Dateien angeben, die Sie ersetzen. Wenn Sie kein Laufwerk oder einen Pfad angeben, wird durch **Replace** das aktuelle Laufwerk und Verzeichnis als Ziel verwendet.|
|/a|Fügt dem Zielverzeichnis neue Dateien hinzu, anstatt vorhandene Dateien zu ersetzen. Sie können diese Befehlszeilenoption nicht mit der Befehlszeilenoption **/s** oder **/u** verwenden.|
|/p|Sie werden zur Bestätigung aufgefordert, bevor Sie eine Zieldatei ersetzen oder eine Quelldatei hinzufügen.|
|/r|Ersetzt schreibgeschützte und ungeschützte Dateien. Wenn Sie versuchen, eine schreibgeschützte Datei zu ersetzen, aber **/r**nicht angeben, wird ein Fehler ausgegeben, und der Ersetzungs Vorgang wird beendet.|
|/w|Wartet darauf, dass Sie vor Beginn der Suche nach Quelldateien einen Datenträger einfügen. Wenn Sie **/w**nicht angeben, ersetzt **Replace** das ersetzen oder Hinzufügen von Dateien sofort, nachdem Sie die EINGABETASTE gedrückt haben.|
|/s|Durchsucht alle Unterverzeichnisse im Zielverzeichnis und ersetzt übereinstimmende Dateien. **/S** kann nicht mit der Befehlszeilenoption **/a** verwendet werden. Der **Replace** -Befehl durchsucht keine Unterverzeichnisse, die in *Path1*angegeben sind.|
|/u|Ersetzt nur die Dateien im Zielverzeichnis, die älter sind als die im Quellverzeichnis. **/U** kann nicht mit der Befehlszeilenoption **/a** verwendet werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Da **Replace** Dateien hinzufügt oder ersetzt, werden die Dateinamen auf dem Bildschirm angezeigt. Nachdem die **Ersetzung** abgeschlossen ist, wird eine Zusammenfassungs Zeile in einem der folgenden Formate angezeigt:  
  ```
  nnn files added
  nnn files replaced
  no file added
  no file replaced
  ```  
- Wenn Sie Disketten verwenden und während des **Ersetzungs** Vorgangs Datenträger wechseln müssen, können Sie die Befehlszeilenoption **/w** angeben, damit **Replace** darauf wartet, dass die Datenträger gewechselt werden.
- Sie können nicht **ersetzen** verwenden, um ausgeblendete Dateien oder Systemdateien zu aktualisieren.
- Die folgende Tabelle zeigt jeden Exitcode und eine kurze Beschreibung seiner Bedeutung:  
  |Exitcode|Beschreibung|
  |---------|-----------|
  |0|Der **Replace** -Befehl hat die Dateien erfolgreich ersetzt oder hinzugefügt.|
  |1|Beim **Replace** -Befehl ist eine falsche Version von MS-DOS aufgetreten.|
  |2|Der Befehl " **Replace** " konnte die Quelldateien nicht finden.|
  |3|Der Befehl zum **ersetzen** konnte den Quell-oder Zielpfad nicht finden.|
  |5|Der Benutzer hat keinen Zugriff auf die Dateien, die Sie ersetzen möchten.|
  |8|Es ist nicht genügend System Arbeitsspeicher vorhanden, um den Befehl auszuführen.|
  |11|Der Benutzer hat die falsche Syntax in der Befehlszeile verwendet.|

> [!NOTE]
> Sie können den ERRORLEVEL-Parameter in der **if** -Befehlszeile in einem Batch Programm verwenden, um Exitcodes zu verarbeiten, die durch **Replace**zurückgegeben werden.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Versionen einer Datei mit dem Namen "Phones. CLI" (die in mehreren Verzeichnissen auf Laufwerk C angezeigt wird) mit der neuesten Version der Datei "Phones. CLI" von einer Diskette in Laufwerk a zu aktualisieren:

`replace a:\phones.cli c:\ /s`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)