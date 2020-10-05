---
title: sort
description: Referenz Artikel für den Sortier Befehl, der Eingaben liest, Daten sortiert und die Ergebnisse auf den Bildschirm, in eine Datei oder auf ein anderes Gerät schreibt.
ms.topic: reference
ms.assetid: 77116469-4790-4442-8a21-9fa73b65ef9f
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 721a166123d7611a545ea143152f65b6d1e91865
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718287"
---
# <a name="sort"></a>sort

Liest Eingaben, sortiert Daten und schreibt die Ergebnisse auf den Bildschirm, in eine Datei oder auf ein anderes Gerät.

## <a name="syntax"></a>Syntax

```
sort [/r] [/+<N>] [/m <kilobytes>] [/l <locale>] [/rec <characters>] [[<drive1>:][<path1>]<filename1>] [/t [<drive2>:][<path2>]] [/o [<drive3>:][<path3>]<filename3>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /r | Kehrt die Sortierreihenfolge um (d. h., sortiert von Z bis A und zwischen 9 und 0). |
| `/+<N>` | Gibt die Zeichen Positionsnummer an, an der der **Sortier** Vorgang beginnt. *N* kann eine beliebige gültige ganze Zahl sein. |
| /m `<kilobytes>` | Gibt die Größe des Hauptspeichers an, der für die Sortierung in Kilobyte (KB) verwendet werden soll. |
| /l \<locale> | Überschreibt die Sortierreihenfolge von Zeichen, die vom Standard Gebiets Schema des Systems definiert werden (d. h. die Sprache und das Land/die Region, die während der Installation ausgewählt wurden) |
| /rec `<characters>` | Gibt die maximale Anzahl von Zeichen in einem Datensatz oder eine Zeile der Eingabedatei an (der Standardwert ist 4.096 und der Höchstwert 65.535). |
| `[<drive1>:][<path1>]<filename1>` | Gibt die Datei an, die sortiert werden soll. Wenn kein Dateiname angegeben wird, wird die Standardeingabe sortiert. Die Angabe der Eingabedatei ist schneller als das Umleiten derselben Datei als Standardeingabe. |
| /t `[<drive2>:][<path2>]` | Gibt den Pfad des Verzeichnisses an, in dem der Arbeitsspeicher des **Sortier** Befehls enthalten sein soll, wenn die Daten nicht in den Hauptspeicher passen. Standardmäßig wird das temporäre System Verzeichnis verwendet. |
| /o `[<drive3>:][<path3>]<filename3>` | Gibt die Datei an, in der die sortierte Eingabe gespeichert werden soll. Wenn kein Wert angegeben ist, werden die Daten in die Standardausgabe geschrieben. Die Angabe der Ausgabedatei ist schneller als das Umleiten der Standardausgabe in dieselbe Datei. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Standardmäßig beginnen Vergleiche mit dem ersten Zeichen jeder Zeile. Die **/+** Befehlszeilenoption startet Vergleiche mit dem durch *N*angegebenen Zeichen. `/+3` Gibt z. b. an, dass jeder Vergleich mit dem dritten Zeichen jeder Zeile beginnen soll. Zeilen mit weniger als *N* Zeichen, die vor anderen Zeilen sortiert werden.

- Der verwendete Arbeitsspeicher beträgt immer mindestens 160 KB. Wenn die Arbeitsspeicher Größe angegeben wird, wird der genaue angegebene Betrag für die Sortierung verwendet (muss mindestens 160 KB betragen), unabhängig davon, wie viel Hauptspeicher verfügbar ist.

- Der Standardwert für die maximale Arbeitsspeicher Größe, wenn keine Größe angegeben ist, beträgt 90% des verfügbaren Hauptspeichers, wenn sowohl die Eingabe als auch die Ausgabedateien sind oder andernfalls 45% des Hauptspeichers. Die Standardeinstellung ergibt in der Regel die beste Leistung.

- Derzeit ist die einzige Alternative zum Standard Gebiets Schema das C-Gebiets Schema, das schneller ist als das Sortieren in natürlicher Sprache (es sortiert Zeichen gemäß Ihren binären Codierungen).

- Sie können das Pipe-Symbol ( `|` ) verwenden, um Eingabedaten von einem anderen Befehl an den **Sortier** Befehl weiterzuleiten oder um die sortierte Ausgabe an einen anderen Befehl weiterzuleiten. Eingabe-und Ausgabedateien können mithilfe von Umleitungs Symbolen ( `<` oder `>` ) angegeben werden. Sie kann schneller und effizienter (insbesondere bei großen Dateien) sein, um die Eingabedatei direkt anzugeben (wie von *filename1* in der Befehlssyntax definiert), und dann die Ausgabedatei mit dem **/o** -Parameter anzugeben.

- Der **Sortier** Befehl unterscheidet nicht zwischen Groß-und Kleinbuchstaben und hat keine Beschränkung auf die Dateigröße.

- Das Sortierungs Programm verwendet die Sortierungs Sequenz Tabelle, die dem Code für **Land/Region** und den Code Page Einstellungen entspricht. Zeichen, die größer als ASCII-Code 127 sind, werden basierend auf Informationen in der Country.sys-Datei oder in einer alternativen Datei sortiert, die durch den **Country** -Befehl in Ihrer config. NT-Datei angegeben wird.

- Wenn die Sortierung innerhalb der maximalen Arbeitsspeicher Größe (standardmäßig festgelegt oder im **/m** -Parameter festgelegt) passt, wird die Sortierung in einem einzelnen Durchlauf ausgeführt. Andernfalls wird die Sortierung in zwei separaten Sortier-und Zusammenführungen durchgeführt, und die für beide Durchlauf verwendeten Speichermengen sind gleich. Wenn zwei Durchläufen ausgeführt werden, werden die teilweise sortierten Daten in einer temporären Datei auf dem Datenträger gespeichert. Wenn nicht genügend Arbeitsspeicher vorhanden ist, um die Sortierung in zwei Durchläufen auszuführen, wird ein Laufzeitfehler ausgegeben. Wenn die Befehlszeilenoption **/m** verwendet wird, um mehr Arbeitsspeicher anzugeben, als tatsächlich verfügbar ist, kann eine Leistungsminderung oder ein Laufzeitfehler auftreten.

## <a name="examples"></a>Beispiele

- Wenn Sie in umgekehrter Reihenfolge die Zeilen in einer Datei namens *expenses.txt*sortieren und anzeigen möchten, geben Sie Folgendes ein:

    ```
    sort /r expenses.txt
    ```

- Um eine große Datei mit dem Namen " *maillist.txt* " nach dem Text *Jones*zu durchsuchen und die Ergebnisse der Suche mithilfe der Pipe () zu sortieren, um `|` die Ausgabe eines **Find** -Befehls an den **Sortier** Befehl weiterzuleiten, geben Sie Folgendes ein:

    ```
    find Jones maillist.txt | sort
    ```

    Der Befehl erzeugt eine sortierte Liste von Zeilen, die den angegebenen Text enthalten.

- Wenn Sie Tastatureingaben sortieren und die Ergebnisse alphabetisch auf dem Bildschirm anzeigen möchten, können Sie zuerst den **Sortier** Befehl ohne Parameter verwenden, indem Sie Folgendes eingeben:

    ```
    sort
    ```

    Geben Sie dann den gewünschten Text ein, und drücken Sie die EINGABETASTE am Ende jeder Zeile. Wenn Sie mit der Eingabe von Text fertig sind, drücken Sie STRG + Z, und drücken Sie dann die EINGABETASTE. Der **Sortier** Befehl zeigt den eingegebenen Text an, der alphabetisch sortiert ist.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)