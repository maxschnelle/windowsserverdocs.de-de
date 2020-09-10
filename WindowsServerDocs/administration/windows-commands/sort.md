---
title: sort
description: Referenz Artikel für Sort, bei dem die Eingabe gelesen, Daten sortiert und die Ergebnisse auf den Bildschirm, in eine Datei oder auf ein anderes Gerät geschrieben werden.
ms.topic: reference
ms.assetid: 77116469-4790-4442-8a21-9fa73b65ef9f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c0809f6a44ee25507f944ce2882305c44215b8f1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640914"
---
# <a name="sort"></a>sort

Liest Eingaben, sortiert Daten und schreibt die Ergebnisse auf den Bildschirm, in eine Datei oder auf ein anderes Gerät.



## <a name="syntax"></a>Syntax

```
sort [/r] [/+<N>] [/m <Kilobytes>] [/l <Locale>] [/rec <Characters>] [[<Drive1>:][<Path1>]<FileName1>] [/t [<Drive2>:][<Path2>]] [/o [<Drive3>:][<Path3>]<FileName3>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/r|Kehrt die Sortierreihenfolge um (d. h., sortiert von Z bis A und zwischen 9 und 0).|
|/+\<N>|Gibt die Zeichen Positionsnummer an, an der der **Sortier** Vorgang beginnt. *N* kann eine beliebige gültige ganze Zahl sein.|
|/m \<Kilobytes>|Gibt die Größe des Hauptspeichers an, der für die Sortierung in Kilobyte (KB) verwendet werden soll.|
|/l \<Locale>|Überschreibt die Sortierreihenfolge von Zeichen, die vom Standard Gebiets Schema des Systems definiert werden (d. h. die Sprache und das Land/die Region, die während der Installation ausgewählt wurden)|
|/rec \<Characters>|Gibt die maximale Anzahl von Zeichen in einem Datensatz oder eine Zeile der Eingabedatei an (der Standardwert ist 4.096 und der Höchstwert 65.535).|
|[\<Drive1>:][\<Path1>]\<FileName1>|Gibt die Datei an, die sortiert werden soll. Wenn kein Dateiname angegeben wird, wird die Standardeingabe sortiert. Die Angabe der Eingabedatei ist schneller als das Umleiten derselben Datei als Standardeingabe.|
|/t [ \<Drive2> :] [ \<Path2> ]|Gibt den Pfad des Verzeichnisses an, in dem der Arbeitsspeicher des **Sortier** Befehls enthalten sein soll, wenn die Daten nicht in den Hauptspeicher passen. Standardmäßig wird das temporäre System Verzeichnis verwendet.|
|/o [ \<Drive3> :] [ \<Path3> ]\<FileName3>|Gibt die Datei an, in der die sortierte Eingabe gespeichert werden soll. Wenn kein Wert angegeben ist, werden die Daten in die Standardausgabe geschrieben. Die Angabe der Ausgabedatei ist schneller als das Umleiten der Standardausgabe in dieselbe Datei.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Verwenden der **/+** Befehlszeilenoption

    Standardmäßig beginnen Vergleiche mit dem ersten Zeichen jeder Zeile. Die **/+** Befehlszeilenoption startet Vergleiche mit dem durch *N*angegebenen Zeichen. `/+3` Gibt z. b. an, dass jeder Vergleich mit dem dritten Zeichen jeder Zeile beginnen soll. Zeilen mit weniger als *N* Zeichen, die vor anderen Zeilen sortiert werden.
-   Verwenden der Befehlszeilenoption **/m**

    Der verwendete Arbeitsspeicher beträgt immer mindestens 160 KB. Wenn die Arbeitsspeicher Größe angegeben wird, wird der genaue angegebene Betrag für die Sortierung verwendet (muss mindestens 160 KB betragen), unabhängig davon, wie viel Hauptspeicher verfügbar ist.

    Der Standardwert für die maximale Arbeitsspeicher Größe, wenn keine Größe angegeben wird, ist 90 Prozent des verfügbaren Hauptspeichers, wenn sowohl die Eingabe als auch die Ausgabedateien sind, andernfalls 45 Prozent des Hauptspeichers. Die Standardeinstellung ergibt in der Regel die beste Leistung.
-   Verwenden der Befehlszeilenoption **/l**

    Derzeit ist die einzige Alternative zum Standard Gebiets Schema das C-Gebiets Schema, das schneller ist als das Sortieren in natürlicher Sprache (es sortiert Zeichen gemäß Ihren binären Codierungen).
-   Verwenden von Umleitungs Symbolen mit dem **Sort** -Befehl

    Sie können das Pipe-Symbol ( **|** ) verwenden, um Eingabedaten von einem anderen Befehl an den **Sortier** Befehl weiterzuleiten oder um die sortierte Ausgabe an einen anderen Befehl weiterzuleiten. Eingabe-und Ausgabedateien können mithilfe von Umleitungs Symbolen ( **<** oder **>** ) angegeben werden. Sie kann schneller und effizienter (insbesondere bei großen Dateien) sein, um die Eingabedatei direkt anzugeben (wie von *FileName1* in der Befehlssyntax definiert), und dann die Ausgabedatei mit dem **/o** -Parameter anzugeben.
-   Groß- und Kleinschreibung

    Der **Sort** -Befehl unterscheidet nicht zwischen Groß-und Kleinbuchstaben.
-   Grenzwerte für die Dateigröße

    Der **Sortier** Befehl hat keine Beschränkung auf die Dateigröße.
-   Sortierreihenfolge

    Das Sortierungs Programm verwendet die Sortierungs Sequenz Tabelle, die dem Code für Land/Region und den Code Page Einstellungen entspricht. Zeichen, die größer als ASCII-Code 127 sind, werden basierend auf Informationen in der Country.sys-Datei oder in einer alternativen Datei sortiert, die durch den **Country** -Befehl in Ihrer config. NT-Datei angegeben wird.
-   Speicherauslastung

    Wenn die Sortierung innerhalb der maximalen Arbeitsspeicher Größe (standardmäßig festgelegt oder im **/m** -Parameter festgelegt) passt, wird die Sortierung in einem einzelnen Durchlauf ausgeführt. Andernfalls wird die Sortierung in zwei separaten Sortier-und Zusammenführungen durchgeführt, und die für beide Durchlauf verwendeten Speichermengen sind gleich. Wenn zwei Durchläufen ausgeführt werden, werden die teilweise sortierten Daten in einer temporären Datei auf dem Datenträger gespeichert. Wenn nicht genügend Arbeitsspeicher vorhanden ist, um die Sortierung in zwei Durchläufen auszuführen, wird ein Laufzeitfehler ausgegeben. Wenn die Befehlszeilenoption **/m** verwendet wird, um mehr Arbeitsspeicher anzugeben, als tatsächlich verfügbar ist, kann eine Leistungsminderung oder ein Laufzeitfehler auftreten.

## <a name="examples"></a>Beispiele

**Sortieren einer Datei**

Geben Sie Folgendes ein, um die Zeilen in einer Datei namens Expenses.txt in umgekehrter Reihenfolge zu sortieren und anzuzeigen:

`sort /r expenses.txt`

**Sortieren der Ausgabe von einem Befehl**

Um eine große Datei mit dem Namen "Maillist.txt" nach dem Text Jones zu durchsuchen und die Ergebnisse der Suche zu sortieren, verwenden Sie die Pipe (|), um die Ausgabe eines **Find** -Befehls wie folgt an den **Sortier** Befehl weiterzuleiten:

`find Jones maillist.txt | sort`

Der Befehl erzeugt eine sortierte Liste von Zeilen, die den angegebenen Text enthalten.

**Sortieren von Tastatureingaben**

Wenn Sie Tastatureingaben sortieren und die Ergebnisse alphabetisch auf dem Bildschirm anzeigen möchten, können Sie zuerst den **Sortier** Befehl ohne Parameter wie folgt verwenden:

`sort`

Geben Sie dann den gewünschten Text ein, und drücken Sie die EINGABETASTE am Ende jeder Zeile. Wenn Sie mit der Eingabe von Text fertig sind, drücken Sie STRG + Z, und drücken Sie dann die EINGABETASTE. Der **Sortier** Befehl zeigt den eingegebenen Text an, der alphabetisch sortiert ist.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)