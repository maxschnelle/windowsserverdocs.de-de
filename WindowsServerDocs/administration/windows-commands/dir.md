---
title: dir
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: acd3b4bb0342dfb8dc651ce7c31e85f1e77a2569
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222968"
---
# <a name="dir"></a>dir



Zeigt eine Liste der Dateien und Unterverzeichnisse des Verzeichnisses. Wenn Sie ohne Angabe von Parametern **Dir** zeigt Volumebezeichnung des Datenträgers und die Seriennummer, gefolgt von einer Liste von Verzeichnissen und Dateien auf dem Datenträger (einschließlich ihrer Namen und das Datum und die jeweils die zuletzt geändert wurde). Für Dateien **Dir** zeigt die Erweiterung und die Größe in Bytes an. **Dir** auch zeigt die Gesamtanzahl der Dateien und Verzeichnisse aufgelistet, die kumulierte Größe und der freie Speicherplatz (in Byte) auf dem Datenträger verbleibenden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
dir [<Drive>:][<Path>][<FileName>] [...] [/p] [/q] [/w] [/d] [/a[[:]<Attributes>]][/o[[:]<SortOrder>]] [/t[[:]<TimeField>]] [/s] [/b] [/l] [/n] [/x] [/c] [/4]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive>:][<Path>]|Gibt an, das Laufwerk und Verzeichnis, für die eine Liste angezeigt werden sollen.|
|[\<Dateiname >]|Gibt an, eine bestimmte Datei oder eine Gruppe von Dateien, die für die eine Liste angezeigt werden sollen.|
|/p|Zeigt jeweils ein Bildschirm mit der Auflistung an. Drücken Sie eine beliebige Taste, um dem nächsten Bildschirm zu sehen, auf der Tastatur.|
|/q|Zeigt den Besitz von Dateiinformationen an.|
|/w|Zeigt die Liste im breiten Format, mit bis zu fünf Datei- oder Verzeichnisnamen in jeder Zeile.|
|/d|Zeigt die Auflistung in das gleiche Format wie **/w**, aber die Dateien nach Spalte sortiert sind.|
|/ a [[:]\<Attribute >]|Zeigt nur die Namen der Verzeichnisse und Dateien mit den Attributen, die Sie angeben. Wenn Sie weglassen **/a**, **Dir** zeigt die Namen aller Dateien mit Ausnahme von ausgeblendete Dateien und Systemdateien. Bei Verwendung von **/a** ohne *Attribute*, **Dir** zeigt die Namen aller Dateien, einschließlich der ausgeblendete Dateien und Systemdateien.</br>Die folgende Liste beschreibt alle Werte, mit denen Sie für *Attribute*. Verwenden einen Doppelpunkt (:)) ist optional. Verwenden Sie eine beliebige Kombination der folgenden Werte ein, und trennen Sie die Werte nicht durch Leerzeichen.</br>**d** Verzeichnisse</br>**h** auflisten versteckter Dateien</br>**s** Systemdateien</br>**l** Analysepunkte</br>**R** schreibgeschützte Dateien</br>**eine** Dateien archiviert</br>**ich** Inhalte nicht indizierte Dateien</br>**-** Präfix, d. h. "not"|
|/ o [[:]\<SortOrder >]|Sortiert die Ausgabe gemäß *SortOrder*, dies kann eine beliebige Kombination der folgenden Werte sein:</br>**n** anhand des Namens (alphabetisch)</br>**e** nach Erweiterung (alphabetisch)</br>**g** zuerst Gruppe von Verzeichnissen</br>**s** nach Größe (kleinste zuerst)</br>**d** von Datum/Uhrzeit (das älteste zuerst)</br>**-** Präfix für Reihenfolge umkehren</br>Hinweis: Die Verwendung eines Doppelpunkts ist optional. Mehrere Werte werden in der Reihenfolge verarbeitet, in denen Sie auflisten. Trennen Sie mehrere Werte nicht durch Leerzeichen.</br>Wenn *SortOrder* nicht angegeben ist, **Dir/o** führt die Verzeichnisse in alphabetischer Reihenfolge an, gefolgt von den Dateien, die auch in alphabetischer Reihenfolge sortiert werden.|
|/ t [[:]\<Zeitfeld >]|Gibt an, welches Zeitfeld, um anzuzeigen, oder verwenden Sie für die Sortierung. In der folgende Liste werden die Werte Sie können beschrieben *Zeitfeld*:</br>**c** erstellen</br>**eine** Letzter Zugriff</br>**w** des letzten Schreibvorgangs|
|/s|Listet jedes Vorkommen des dem angegebenen Dateinamen im angegebenen Verzeichnis und alle Unterverzeichnisse.|
|/b|Zeigt eine bare-Liste von Verzeichnissen und Dateien, ohne zusätzliche Informationen. **/ b** überschreibt **/w**.|
|/l|Zeigt nicht sortierte, Verzeichnis- und Dateinamen in Kleinbuchstaben.|
|/n|Zeigt ein Format lange Liste mit Dateinamen am rechten Rand des Bildschirms.|
|/x|Zeigt die Kurznamen für nicht-8.3-Dateinamen generiert. Die Anzeige ist identisch mit der Anzeige für **/n**, aber der Kurzname wird vor den langen Namen eingefügt.|
|/c|Zeigt das Tausendertrennzeichen in der Dateigröße. Dies ist das Standardverhalten. Verwendung **/-c** Trennzeichen ausblenden.|
|/4|Zeigt die Jahre im vierstelligen Format.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Verwenden Sie mehrere *FileName* Parameter trennen Sie den Namen der Dateien durch ein Leerzeichen, Komma oder Semikolon.
-   Sie können Platzhalterzeichen verwenden (**&#42;** oder **?** ), um ein oder mehrere Zeichen, der einen Dateinamen und eine Teilmenge der Dateien oder Unterverzeichnisse anzuzeigen.

    **Sternchen (\*):** Verwenden Sie das Sternchen als Ersatz für eine beliebige Zeichenfolge von Zeichen, z. B.:  
    -   **Dir \*.txt** Listet alle Dateien im aktuellen Verzeichnis mit Erweiterungen, die mit txt, z. B. txt, .txt1, .txt_old beginnen.
    -   **Lesen Sie Dir\*.txt** Listet alle Dateien im aktuellen Verzeichnis, die beginnen mit "Read" und Erweiterungen, die mit txt, z. B. txt, .txt1 oder .txt_old beginnen.
    -   **Lesen Sie Dir\*.\***  Listet alle Dateien im aktuellen Verzeichnis, die mit "s" beginnen mit einer beliebigen Erweiterung.

    Der Sternchen-Platzhalter verwendet immer kurze Dateinamen Namen zuordnen, damit Sie möglicherweise unerwartete Ergebnisse erhalten. Das folgende Verzeichnis enthält beispielsweise zwei Dateien (t.txt2 und t97.txt):  
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
    Sie erwarten wahrscheinlich, dass mit **Dir t97\***  würde die Datei t97.txt zurückgeben. Allerdings eingeben **Dir t97\***  beiden Dateien an und gibt zurück, da es sich bei der Sternchen-Platzhalter die Datei t.txt2 zu t97.txt entspricht, mithilfe der Zuordnung Kurznamen T97B4~1.TXT. Auf ähnliche Weise eingeben **del t97\***  beide Dateien gelöscht.

    **Fragezeichen (?):** Verwenden Sie das Fragezeichen als Ersatz für ein einzelnes Zeichen in einen Namen ein. Geben Sie z. B. **Dir lesen Zuweisen von gruppenlizenzen finden. TXT** Listet alle Dateien im aktuellen Verzeichnis mit der Erweiterung TXT, die beginnen mit "Read", und von bis zu drei Zeichen gefolgt sind. Dies schließt Read.txt, Read1.txt, Read12.txt, Read123.txt, und Readme1.txt, aber nicht Readme12.txt.
-   Angeben der Attribute der Datei anzeigen

    Bei Verwendung von **/a** mit mehr als ein Wert in *Attribute*, **Dir** zeigt die Namen der nur die Dateien mit den angegebenen Attributen. Angenommen, Sie verwenden **/a** mit **r** und **-h** als Attribute (indem Sie entweder **/ a: R-h** oder **/ar** ), **Dir** nur zeigt die Namen der schreibgeschützten Dateien, die nicht ausgeblendet werden.
-   Angeben der Sortierreihenfolge von Dateien

    Bei Angabe von mehr als eine *SortOrder* Wert **Dir** sortiert die Dateinamen, nach dem ersten Kriterium aus, und klicken Sie dann durch das zweite Kriterium, und So weiter. Angenommen, Sie verwenden **/o** mit der **e** und **-s** Werte für *SortOrder* (indem Sie entweder **OE-s**oder **/oe-s**), **Dir** sortiert die Namen von Verzeichnissen und Dateien nach Erweiterung, mit dem größten ersten und zeigt dann das endgültige Ergebnis. Die alphabetische Sortierung nach Erweiterung bewirkt, dass Dateinamen ohne Erweiterungen zuerst angezeigt werden und Verzeichnisnamen, und klicken Sie dann Dateinamen mit der Erweiterung.
-   Mithilfe der Umleitungssymbole und pipes

    Bei Verwendung der Umleitungssymbol ( **>** ) zum Senden von **Dir** Ausgabe in eine Datei oder einen senkrechten Strich ( **|** ) zum Senden von **Dir**Ausgabe an einen anderen Befehl verwenden **z.** und **/b** nur Dateinamen auflisten. Können Sie *FileName* mit **/b** und **/s** an, dass **Dir** besteht darin, das aktuelle Verzeichnis und seinen Unterverzeichnissen für alle Dateien suchen Diese Übereinstimmung nennt *FileName*. **Dir** Listet nur den Laufwerkbuchstaben, Verzeichnisname, Dateiname und Dateierweiterung (ein Pfad pro Zeile), für jede Datei sucht nach Namen. Bevor Sie eine Pipe, zum Senden von verwenden **Dir** Ausgabe an einen anderen Befehl, Sie sollten legen Sie die TEMP-Umgebungsvariable in Ihrer Datei.
-   Die **Dir** -Befehl, mit verschiedenen Parametern finden Sie in der Wiederherstellungskonsole.

## <a name="examples"></a>Beispiele

Klicken Sie zum Anzeigen von allen Verzeichnissen eine nach dem anderen, in alphabetischer Reihenfolge, klicken Sie im breiten Format und nach jedem Bildschirm anhalten stellen Sie sicher, dass das Root-Verzeichnis im aktuellen Verzeichnis ist, und geben:
```
dir /s/w/o/p
```
**Dir** enthält das Stammverzeichnis, Unterverzeichnisse und Dateien in das Stammverzeichnis, einschließlich der Erweiterungen. Klicken Sie dann **Dir** Listet die Namen der Unterverzeichnisse und den Dateinamen in den einzelnen Unterverzeichnissen in der Struktur.

Im vorherige Beispiel ändern, damit **Dir** zeigt den Dateinamen und Erweiterungen, lässt aber die Namen der Verzeichnisse, Typ:
```
dir /s/w/o/p/a:-d
```
Um eine Verzeichnisliste zu drucken, geben Sie Folgendes ein:
```
dir > prn
```
Beim Angeben von **Prn**, Verzeichnisliste wird gesendet, an den Drucker, die an den LPT1 Port verbunden ist. Wenn der Drucker an einen anderen Port verbunden ist, müssen Sie ersetzen **Prn** durch den Namen der richtige Port.

Sie können auch Ausgabe umleiten der **Dir** Befehl in eine Datei und Ersetzen Sie dabei **Prn** mit einem Dateinamen. Sie können auch einen Pfad eingeben. Z. B. zum direkten **Dir** Ausgabe in der Datei dir.doc im Verzeichnis, Typ:
```
dir > \records\dir.doc
```
Wenn dir.doc nicht vorhanden ist, **Dir** erstellt, es sei denn, das Datensätze-Verzeichnis nicht vorhanden ist. In diesem Fall wird die folgende angezeigt:

`File creation error`

Um eine Liste aller Dateinamen mit der Erweiterung TXT in allen Verzeichnissen auf Laufwerk C anzuzeigen, geben Sie Folgendes ein:
```
dir c:\*.txt /w/o/s/p
```
**Dir** angezeigt, das im breiten Format eine alphabetisch sortierte Liste der entsprechenden Datei benannt wird, in jedem Verzeichnis, und er hält jedes Mal, den Bildschirm ausfüllt, bis Sie eine beliebige Taste, um den Vorgang fortzusetzen drücken.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)