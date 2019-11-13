---
title: dir
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edcbf69b-eaa4-466e-b210-3dd8892f4d93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b073b0557cd011f6742a8a8e532165f53b0a6974
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377876"
---
# <a name="dir"></a>dir



Zeigt eine Liste der Dateien und Unterverzeichnisse eines Verzeichnisses an. Bei Verwendung ohne Parameter zeigt **dir** die Volumebezeichnung und Seriennummer des Datenträgers an, gefolgt von einer Liste der Verzeichnisse und Dateien auf dem Datenträger (einschließlich ihrer Namen und Datum und Uhrzeit der letzten Änderung). Für Dateien zeigt **dir** die Namenserweiterung und die Größe in Bytes an. **Außerdem werden** die Gesamtzahl der aufgeführten Dateien und Verzeichnisse, die kumulative Größe und der freie Speicherplatz (in Bytes) angezeigt, der auf dem Datenträger verbleiben.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
dir [<Drive>:][<Path>][<FileName>] [...] [/p] [/q] [/w] [/d] [/a[[:]<Attributes>]][/o[[:]<SortOrder>]] [/t[[:]<TimeField>]] [/s] [/b] [/l] [/n] [/x] [/c] [/4]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [<Path>]|Gibt das Laufwerk und das Verzeichnis an, für die eine Auflistung angezeigt werden soll.|
|[\<Dateiname >]|Gibt eine bestimmte Datei oder Gruppe von Dateien an, für die eine Auflistung angezeigt werden soll.|
|/p|Zeigt jeweils einen Bildschirm der Auflistung an. Drücken Sie eine beliebige Taste auf der Tastatur, um den nächsten Bildschirm anzuzeigen.|
|/q|Zeigt Dateibesitz Informationen an.|
|/w|Zeigt die Auflistung im breiten Format an, mit bis zu fünf Dateinamen oder Verzeichnisnamen in jeder Zeile.|
|/d|Zeigt die Auflistung im gleichen Format wie **/w**an, aber die Dateien sind nach Spalte sortiert.|
|/a [[:]\<Attribute >]|Zeigt nur die Namen dieser Verzeichnisse und Dateien mit den von Ihnen angegebenen Attributen an. Wenn Sie **/a**weglassen, **werden** die Namen aller Dateien angezeigt, mit Ausnahme von ausgeblendeten Dateien und Systemdateien. Wenn Sie **/a** ohne Angabe von *Attributen*verwenden, werden in **dir** die Namen aller Dateien angezeigt, einschließlich ausgeblendeter Dateien und Systemdateien.</br>In der folgenden Liste werden die einzelnen Werte beschrieben, die Sie für *Attribute*verwenden können. Verwenden eines Doppelpunkts (:) ist optional. Verwenden Sie eine beliebige Kombination dieser Werte, und trennen Sie die Werte nicht durch Leerzeichen.</br>**d-** Verzeichnisse</br>ausgeblendete Dateien</br>**s** -System Dateien</br>**l** -Analyse Punkte</br>schreibgeschützte **r** -Dateien</br>**Dateien,** die für die Archivierung bereit sind</br>indizierte Dateien **sind nicht Inhalts**</br>**-** Präfix "Not"|
|/o [[:]\<sortor der->]|Sortiert die Ausgabe nach *sortor*, wobei es sich um eine beliebige Kombination der folgenden Werte handeln kann:</br>**n** nach Name (alphabetisch)</br>**e** nach Erweiterung (alphabetisch)</br>**g** Gruppen Verzeichnisse zuerst</br>**s** nach Größe (zuerst die kleinste)</br>**d** nach Datum/Uhrzeit (älteste erste)</br>**-** Präfix in umgekehrter Reihenfolge</br>Hinweis: die Verwendung eines Doppelpunkts ist optional. Mehrere Werte werden in der Reihenfolge verarbeitet, in der Sie Sie auflisten. Trennen Sie mehrere Werte nicht durch Leerzeichen.</br>Wenn *SortOrder* nicht angegeben wird, listet **dir/o** die Verzeichnisse in alphabetischer Reihenfolge auf, gefolgt von den Dateien, die auch in alphabetischer Reihenfolge sortiert sind.|
|/t [[:]\<TimeField >]|Gibt an, welches Zeit Feld angezeigt oder für die Sortierung verwendet werden soll. In der folgenden Liste werden die einzelnen Werte beschrieben, die Sie für *TimeField*verwenden können:</br>**c** -Erstellung</br>**Letzter Zugriff**</br>**w** zuletzt geschrieben|
|/s|Listet jedes Vorkommen des angegebenen Datei namens innerhalb des angegebenen Verzeichnisses und aller Unterverzeichnisse auf.|
|/b|Zeigt eine leere Liste von Verzeichnissen und Dateien ohne zusätzliche Informationen an. **/b** überschreibt **/w**.|
|/l|Zeigt unsortierte Verzeichnisnamen und Dateinamen in Kleinbuchstaben an.|
|/n|Zeigt ein langes Listenformat mit Dateinamen ganz rechts auf dem Bildschirm an.|
|/x|Zeigt die Kurznamen an, die für nicht-8dot3-Dateinamen generiert wurden. Die Anzeige ist identisch mit der Anzeige für **/n**, aber der Kurzname wird vor dem langen Namen eingefügt.|
|/c|Zeigt das Tausender Trennzeichen in Dateigrößen an. Hierbei handelt es sich um das standardmäßige Verhalten. Verwenden Sie **/-c** , um Trennzeichen auszublenden.|
|/4|Zeigt Jahre im vierstelligen Format an.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Wenn *Sie mehrere Dateinamen Parameter* verwenden möchten, trennen Sie die einzelnen Dateinamen durch ein Leerzeichen, Komma oder Semikolon.
- Sie können Platzhalter Zeichen ( **&#42;** oder **?** ) verwenden, um ein oder mehrere Zeichen eines Datei namens darzustellen und eine Teilmenge von Dateien oder Unterverzeichnissen anzuzeigen.

  **Sternchen (\*):** Verwenden Sie das Sternchen als Ersatz für eine beliebige Zeichenfolge, z. b.:  
  - **dir \*. txt** listet alle Dateien im aktuellen Verzeichnis mit Erweiterungen auf, die mit ". txt" beginnen, z. b. txt,. txt1,. txt_old.
  - **dir Read\*. txt** listet alle Dateien im aktuellen Verzeichnis auf, die mit "Read" beginnen, und mit Erweiterungen, die mit ". txt" beginnen, z. b. txt,. txt1 oder. txt_old.
  - **dir Read\*.\\** * listet alle Dateien im aktuellen Verzeichnis auf, die mit "Read" mit einer beliebigen Erweiterung beginnen.

  Der Platzhalter Platzhalter verwendet immer eine kurze Zuordnung von Dateinamen, sodass Sie möglicherweise unerwartete Ergebnisse erhalten. Das folgende Verzeichnis enthält z. b. zwei Dateien (t. txt2 und T97. txt): 
 
  ```
  C:\test>dir /x
  Volume in drive C has no label.
  Volume Serial Number is B86A-EF32
    
  Directory of C:\test
    
  11/30/2004  01:40 PM <DIR>  .
  11/30/2004  01:40 PM <DIR> ..
  11/30/2004  11:05 AM 0 T97B4~1.TXT t.txt2
  11/30/2004  01:16 PM 0 t97.txt
  ```  

  Sie erwarten möglicherweise, dass die Eingabe von **dir T97\\** * die Datei T97. txt zurückgibt. Bei der Eingabe von **dir T97\\** * werden jedoch beide Dateien zurückgegeben, da das Sternchen-Platzhalter Zeichen mit der Kurznamen Zuordnung T97B4 ~ 1. txt mit der Datei t. txt2 zu T97. txt übereinstimmt. Ebenso werden bei der Eingabe von **del T97\\** * beide Dateien gelöscht.

  **Fragezeichen (?):** Verwenden Sie das Fragezeichen als Ersatz für ein einzelnes Zeichen in einem Namen. Geben Sie z. b. **dir Read???. txt** listet alle Dateien im aktuellen Verzeichnis mit der Erweiterung ". txt" auf, die mit "Read" beginnen und bis zu drei Zeichen gefolgt sind. Hierzu gehören Read. txt, Read1. txt, Read12. txt, Read123. txt und Readme1. txt, jedoch nicht Readme12. txt.
- Angeben von Datei Anzeige Attributen

  Wenn Sie **/a** mit mehr als einem Wert in *Attributen* **verwenden, werden** nur die Namen der Dateien mit allen angegebenen Attributen angezeigt. Wenn Sie z. b. **/a** mit **r** und **-h** als Attribute verwenden (entweder mithilfe von **/a: r-h** oder **/AR-h**), werden in **dir** nur die Namen der schreibgeschützten Dateien angezeigt, die nicht ausgeblendet sind.
- Angeben der Dateinamen Sortierung

  Wenn Sie mehr als einen *sortor* -Wert angeben, sortiert **dir** die Dateinamen nach dem ersten Kriterium, dann nach dem zweiten Kriterium usw. Wenn Sie z. b. **/o** mit den **e** -und **-s-** Werten für *SortOrder* (mithilfe von **/o: e-s** oder **/OE-s**) verwenden, sortiert **dir** die Namen von Verzeichnissen und Dateien nach Erweiterung mit dem größten ersten und zeigt dann das Endergebnis an. Die alphabetische Sortierung nach Erweiterung bewirkt, dass Dateinamen ohne Erweiterungen zuerst angezeigt werden, dann Verzeichnisnamen und dann Dateinamen mit Erweiterungen.
- Verwenden von Umleitungs Symbolen und Pipes

  Wenn Sie das Umleitungs Symbol ( **>** ) verwenden, um die **dir** -Ausgabe an eine Datei oder eine Pipe ( **|** ) zu senden, um die **dir** -Ausgabe an einen anderen Befehl zu senden, verwenden Sie **/a:-d** und **/b** , um nur die Dateinamen aufzulisten. Sie können *filename* mit **/b** und **/s** verwenden, um anzugeben, dass **dir** das aktuelle Verzeichnis und seine Unterverzeichnisse nach allen Dateinamen durchsuchen soll, die dem *Datei*Namen entsprechen. **Dir** listet nur den Laufwerk Buchstaben, den Verzeichnisnamen, den Dateinamen und die Dateinamenerweiterung (ein Pfad pro Zeile) für jeden gefundenen Dateinamen auf. Bevor Sie eine Pipe verwenden, um die **dir** -Ausgabe an einen anderen Befehl zu senden, sollten Sie die Temp-Umgebungsvariable in der Datei "Autoexec. NT" festlegen.
- Der Befehl **dir** mit unterschiedlichen Parametern ist über die Wiederherstellungskonsole verfügbar.

## <a name="examples"></a>Beispiele

Stellen Sie sicher, dass das Stammverzeichnis das aktuelle Verzeichnis ist, um alle Verzeichnisse nacheinander anzuzeigen, in alphabetischer Reihenfolge und nach jedem Bildschirm anzuhalten, und geben Sie dann Folgendes ein:

```
dir /s/w/o/p
```

**Dir** listet das Stammverzeichnis, die Unterverzeichnisse und die Dateien im Stammverzeichnis, einschließlich Erweiterungen, auf. In **dir** werden die Namen und Dateinamen der Unterverzeichnisse in den einzelnen Unterverzeichnissen in der Struktur aufgeführt.

Um das vorherige Beispiel so zu ändern, dass **dir** die Dateinamen und-Erweiterungen anzeigt, die Verzeichnisnamen jedoch ausgelassen werden, geben Sie Folgendes ein:

```
dir /s/w/o/p/a:-d
```

Zum Drucken einer Verzeichnisliste geben Sie Folgendes ein:

```
dir > prn
```

Wenn Sie **PRN**angeben, wird die Verzeichnisliste an den Drucker gesendet, der mit dem LPT1-Port verbunden ist. Wenn Ihr Drucker an einen anderen Port angefügt ist, müssen Sie **PRN** durch den Namen des richtigen Ports ersetzen.

Sie können die Ausgabe des **dir** -Befehls auch in eine Datei umleiten, indem Sie **PRN** durch einen Dateinamen ersetzen. Sie können auch einen Pfad eingeben. Geben Sie beispielsweise Folgendes ein, um die **dir** -Ausgabe an die Datei "dir. doc" im Verzeichnis "Records" zu leiten:

```
dir > \records\dir.doc
```

Wenn dir. doc nicht vorhanden ist, wird es von **dir** erstellt, es sei denn, das Verzeichnis "Records" ist nicht vorhanden. In diesem Fall wird die folgende Meldung angezeigt:

`File creation error`

Geben Sie Folgendes ein, um eine Liste aller Dateinamen mit der Erweiterung ". txt" in allen Verzeichnissen auf Laufwerk C anzuzeigen:

```
dir c:\*.txt /w/o/s/p
```

**Dir** zeigt eine alphabetisch sortierte Liste der übereinstimmenden Dateinamen in jedem Verzeichnis an, und es wird jedes Mal angehalten, wenn der Bildschirm aufgefüllt wird, bis Sie eine beliebige Taste drücken, um den Vorgang fortzusetzen.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)