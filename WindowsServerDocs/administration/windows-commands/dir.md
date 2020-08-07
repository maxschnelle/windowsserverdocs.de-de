---
title: dir
description: Referenz Artikel für den Befehl dir, mit dem eine Liste der Dateien und Unterverzeichnisse eines Verzeichnisses angezeigt wird.
ms.topic: article
ms.assetid: edcbf69b-eaa4-466e-b210-3dd8892f4d93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51d36f0f5498c5c853df2d6663f52411037c13d4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890985"
---
# <a name="dir"></a>dir

Zeigt eine Liste der Dateien und Unterverzeichnisse eines Verzeichnisses an. Bei Verwendung ohne Parameter zeigt dieser Befehl die Volumebezeichnung und Seriennummer des Datenträgers an, gefolgt von einer Liste der Verzeichnisse und Dateien auf dem Datenträger (einschließlich ihrer Namen und Datum und Uhrzeit der letzten Änderung). Für Dateien zeigt dieser Befehl die Namen Erweiterung und die Größe in Bytes an. Mit diesem Befehl werden außerdem die Gesamtzahl der aufgelisteten Dateien und Verzeichnisse, die kumulative Größe und der freie Speicherplatz (in Bytes) angezeigt, der auf dem Datenträger verbleiben.

Der Befehl **dir** kann auch in der Windows-Wiederherstellungskonsole mithilfe verschiedener Parameter ausgeführt werden. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
dir [<drive>:][<path>][<filename>] [...] [/p] [/q] [/w] [/d] [/a[[:]<attributes>]][/o[[:]<sortorder>]] [/t[[:]<timefield>]] [/s] [/b] [/l] [/n] [/x] [/c] [/4] [/r]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `[<drive>:][<path>]` | Gibt das Laufwerk und das Verzeichnis an, für die eine Auflistung angezeigt werden soll. |
| `[<filename>]` | Gibt eine bestimmte Datei oder Gruppe von Dateien an, für die eine Auflistung angezeigt werden soll. |
| /p | Zeigt jeweils einen Bildschirm der Auflistung an. Drücken Sie eine beliebige Taste, um den nächsten Bildschirm anzuzeigen. |
| /q | Zeigt Dateibesitz Informationen an. |
| /w | Zeigt die Auflistung im breiten Format an, mit bis zu fünf Dateinamen oder Verzeichnisnamen in jeder Zeile. |
| /d | Zeigt die Auflistung im gleichen Format wie **/w**an, aber die Dateien sind nach Spalte sortiert. |
| /a [[:] `<attributes>` ] | Zeigt nur die Namen dieser Verzeichnisse und Dateien mit den angegebenen Attributen an. Wenn Sie diesen Parameter nicht verwenden, zeigt der Befehl die Namen aller Dateien mit Ausnahme von ausgeblendeten und Systemdateien an. Wenn Sie diesen Parameter ohne Angabe von *Attributen*verwenden, zeigt der Befehl die Namen aller Dateien an, einschließlich ausgeblendeter Dateien und Systemdateien. Die Liste der möglichen *Attribut* Werte lautet:<ul><li>**d** -Verzeichnisse</li><li>**h** -ausgeblendete Dateien</li><li>**s** -System Dateien</li><li>**l** -Analyse Punkte</li><li>**r** -schreibgeschützte Dateien</li><li>**a** -Dateien, die für die Archivierung bereit sind</li><li>**i** nicht mit Inhalt indizierte Dateien</li></ul>Sie können eine beliebige Kombination dieser Werte verwenden, die Werte jedoch nicht mithilfe von Leerzeichen trennen. Optional können Sie einen Doppelpunkt (:) Trennzeichen, oder Sie können einen Bindestrich (-) als Präfix verwenden, um "Not" zu verwenden. Wenn Sie z. b. das **-s-** Attribut verwenden, werden die Systemdateien nicht angezeigt. |
| /o [[:] `<sortorder>` ] | Sortiert die Ausgabe nach *sortor*, wobei es sich um eine beliebige Kombination der folgenden Werte handeln kann:<ul><li>**n** -alphabetisch nach Name</li><li>**e** -alphabetisch durch Erweiterung</li><li>**g** -Gruppen Verzeichnisse zuerst</li><li>**s** -nach-Größe, kleinste erste</li><li>**d** -nach Datum/Uhrzeit, älteste erste</li><li>Verwenden des **-** Präfixes zum Umkehren der Sortierreihenfolge</li></ul>Mehrere Werte werden in der Reihenfolge verarbeitet, in der Sie Sie auflisten. Trennen Sie mehrere Werte nicht mit Leerzeichen, Sie können jedoch optional einen Doppelpunkt (:) verwenden.<p>Wenn *SortOrder* nicht angegeben wird, listet **dir/o** die Verzeichnisse alphabetisch auf, gefolgt von den Dateien, die ebenfalls alphabetisch sortiert sind. |
| /t [[:] `<timefield>` ] | Gibt an, welches Zeit Feld angezeigt oder für die Sortierung verwendet werden soll. Folgende *TimeField* -Werte sind verfügbar:<ul><li>**c** -Erstellung</li><li>**a** -Letzter Zugriff</li><li>**w** -zuletzt geschrieben</li></ul> |
| /s | Listet jedes Vorkommen des angegebenen Datei namens innerhalb des angegebenen Verzeichnisses und aller Unterverzeichnisse auf. |
| /b | Zeigt eine leere Liste von Verzeichnissen und Dateien ohne zusätzliche Informationen an. Der **/b** -Parameter überschreibt **/w**. |
| /l | Zeigt unsortierte Verzeichnisnamen und Dateinamen unter Verwendung von Kleinbuchstaben an. |
| /n | Zeigt ein langes Listenformat mit Dateinamen ganz rechts auf dem Bildschirm an. |
| /x | Zeigt die Kurznamen an, die für nicht-8dot3-Dateinamen generiert wurden. Die Anzeige ist identisch mit der Anzeige für **/n**, aber der Kurzname wird vor dem langen Namen eingefügt. |
| /C | Zeigt das Tausender Trennzeichen in Dateigrößen an. Dies ist das Standardverhalten. Verwenden Sie **/c** , um Trennzeichen auszublenden. |
| /4 | Zeigt Jahre im vierstelligen Format an. |
| /r | Zeigt Alternative Datenströme der Datei an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn *Sie mehrere Dateinamen Parameter* verwenden möchten, trennen Sie die einzelnen Dateinamen durch ein Leerzeichen, Komma oder Semikolon.

- Sie können Platzhalter Zeichen (**&#42;** oder **?**) verwenden, um ein oder mehrere Zeichen eines Datei namens darzustellen und eine Teilmenge von Dateien oder Unterverzeichnissen anzuzeigen.

- Sie können das Platzhalter Zeichen **&#42;** verwenden, um eine beliebige Zeichenfolge zu ersetzen, z. b.:

  - `dir *.txt`Listet alle Dateien im aktuellen Verzeichnis mit Erweiterungen auf, die mit ". txt" beginnen, z. b. txt,. txt1,. txt_old.

  - `dir read *.txt`Listet alle Dateien im aktuellen Verzeichnis auf, die mit "lesen" beginnen, und mit Erweiterungen, die mit ". txt" beginnen, z. b. txt,. txt1 oder. txt_old.

  - `dir read *.*`Listet alle Dateien im aktuellen Verzeichnis auf, die mit dem Lesen mit einer beliebigen Erweiterung beginnen.

  Der Platzhalter Platzhalter verwendet immer eine kurze Zuordnung von Dateinamen, sodass Sie möglicherweise unerwartete Ergebnisse erhalten. Das folgende Verzeichnis enthält z. b. zwei Dateien (t.txt2 und t97.txt):

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

  Sie erwarten möglicherweise, dass `dir t97\*` die Eingabe die Datei t97.txt zurückgibt. `dir t97\*`Bei der Eingabe von werden jedoch beide Dateien zurückgegeben, da das Sternchen-Platzhalter Zeichen mit der Datei t.txt2 t97.txt, indem die Kurzname Map *T97B4 ~1.TXT*verwendet wird. Ebenso werden bei der Eingabe `del t97\*` beide Dateien gelöscht.

- Sie können das Fragezeichen (?) als Ersatz für ein einzelnes Zeichen in einem Namen verwenden. Wenn Sie z. b. eingeben, `dir read???.txt` werden alle Dateien im aktuellen Verzeichnis mit der Erweiterung ". txt" aufgelistet, die mit "Read" beginnen und von bis zu drei Zeichen gefolgt sind. Dies schließt Read.txt, Read1.txt, Read12.txt, Read123.txt und Readme1.txt, aber nicht Readme12.txt ein.

- Wenn Sie **/a** mit mehr als einem Wert in *Attributen*verwenden, werden mit diesem Befehl nur die Namen der Dateien mit allen angegebenen Attributen angezeigt. Wenn Sie z. b. **/a** mit **r** und **-h** als Attribute verwenden (mit `/a:r-h` oder `/ar-h` ), werden mit diesem Befehl nur die Namen der schreibgeschützten Dateien angezeigt, die nicht ausgeblendet sind.

- Wenn Sie mehr als einen *sortor* -Wert angeben, sortiert dieser Befehl die Dateinamen nach dem ersten Kriterium, dann nach dem zweiten Kriterium usw. Wenn Sie z. b. **/o** mit den **e** **-und-s-** Parametern für *SortOrder* (mithilfe von `/o:e-s` oder) verwenden `/oe-s` , sortiert dieser Befehl die Namen von Verzeichnissen und Dateien nach Erweiterung mit dem größten ersten und zeigt dann das Endergebnis an. Die alphabetische Sortierung nach Erweiterung bewirkt, dass Dateinamen ohne Erweiterungen zuerst angezeigt werden, dann Verzeichnisnamen und dann Dateinamen mit Erweiterungen.

- Wenn Sie das Umleitungs Symbol ( `>` ) verwenden, um die Ausgabe dieses Befehls an eine Datei zu senden, oder wenn Sie eine Pipe () verwenden, `|` um die Ausgabe dieses Befehls an einen anderen Befehl zu senden, müssen Sie `/a:-d` und **/b** verwenden, um nur die Dateinamen aufzulisten. Sie können *filename* mit **/b** und **/s** verwenden, um anzugeben, dass dieser Befehl das aktuelle Verzeichnis und die zugehörigen Unterverzeichnisse nach allen Dateinamen durchsuchen soll, die dem *Datei*Namen entsprechen. Mit diesem Befehl werden nur der Laufwerk Buchstabe, der Verzeichnisname, der Dateiname und die Dateinamenerweiterung (ein Pfad pro Zeile) für jeden gefundenen Dateinamen aufgelistet. Bevor Sie eine Pipe verwenden, um die Ausgabe dieses Befehls an einen anderen Befehl zu senden, sollten Sie die *Temp* -Umgebungsvariable in der Datei "Autoexec. NT" festlegen.

## <a name="examples"></a>Beispiele

Stellen Sie sicher, dass das Stammverzeichnis das aktuelle Verzeichnis ist, um alle Verzeichnisse nacheinander anzuzeigen, in alphabetischer Reihenfolge und nach jedem Bildschirm anzuhalten, und geben Sie dann Folgendes ein:

```
dir /s/w/o/p
```

In der Ausgabe werden das Stammverzeichnis, die Unterverzeichnisse und die Dateien im Stammverzeichnis, einschließlich Erweiterungen, aufgelistet. Mit diesem Befehl werden auch die Unterverzeichnis Namen und die Dateinamen in jedem Unterverzeichnis in der Struktur aufgelistet.

Um das vorherige Beispiel so zu ändern, dass **dir** die Dateinamen und-Erweiterungen anzeigt, die Verzeichnisnamen jedoch ausgelassen werden, geben Sie Folgendes ein:

```
dir /s/w/o/p/a:-d
```

Zum Drucken einer Verzeichnisliste geben Sie Folgendes ein:

```
dir > prn
```

Wenn Sie **PRN**angeben, wird die Verzeichnisliste an den Drucker gesendet, der mit dem LPT1-Port verbunden ist. Wenn Ihr Drucker an einen anderen Port angefügt ist, müssen Sie **PRN** durch den Namen des richtigen Ports ersetzen.

Sie können die Ausgabe des **dir** -Befehls auch in eine Datei umleiten, indem Sie **PRN** durch einen Dateinamen ersetzen. Sie können auch einen Pfad eingeben. Geben Sie beispielsweise Folgendes ein, um die **dir** -Ausgabe an die Datei dir.doc im Verzeichnis "Records" weiterzuleiten:

```
dir > \records\dir.doc
```

Wenn dir.doc nicht vorhanden ist, wird Sie von **dir** erstellt, es sei denn, das Verzeichnis " **Records** " ist nicht vorhanden. In diesem Fall wird die folgende Meldung angezeigt:

```
File creation error
```

Geben Sie Folgendes ein, um eine Liste aller Dateinamen mit der Erweiterung ". txt" in allen Verzeichnissen auf Laufwerk C anzuzeigen:

```
dir c:\*.txt /w/o/s/p
```

Der Befehl **dir** zeigt im breiten Format eine alphabetisch sortierte Liste der übereinstimmenden Dateinamen in jedem Verzeichnis an und wird jedes Mal angehalten, wenn der Bildschirm ausgefüllt wird, bis Sie eine Taste drücken, um den Vorgang fortzusetzen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
