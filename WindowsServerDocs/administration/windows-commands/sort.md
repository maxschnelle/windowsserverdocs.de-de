---
title: sort
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 77116469-4790-4442-8a21-9fa73b65ef9f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d38beef74156d9d57b947883c542c2c7e971e00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854751"
---
# <a name="sort"></a>sort



Liest die Eingabe, werden Daten sortiert und schreibt die Ergebnisse aus, auf dem Bildschirm, in eine Datei oder ein anderes Gerät.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sort [/r] [/+<N>] [/m <Kilobytes>] [/l <Locale>] [/rec <Characters>] [[<Drive1>:][<Path1>]<FileName1>] [/t [<Drive2>:][<Path2>]] [/o [<Drive3>:][<Path3>]<FileName3>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/r|Kehrt die Reihenfolge der Sortierung (d. h. die Sortierungen von Z bis A und 9, 0).|
|/+\<N>|Gibt die Zeichenposition, in denen **Sortierreihenfolge** jeden Vergleich beginnt. *N* kann eine beliebige gültige ganze Zahl sein.|
|/m \<Kilobytes>|Gibt die Menge des Hauptspeichers für die Verwendung für die Sortierung in Kilobyte (KB) an.|
|/l \<Locale>|Überschreibt die Sortierreihenfolge der Zeichen, die von der Standard-Gebietsschema des Systems (d. h. die Sprache und Land/Region, die während der Installation aktiviert) definiert werden.|
|/ REC \<Zeichen >|Gibt die maximale Anzahl von Zeichen in einem Datensatz oder eine Zeile der Eingabedatei (der Standardwert ist 4.096 und der Höchstwert ist 65.535).|
|[\<Laufwerk1 >:] [\<Path1 >]\<Dateiname1 >|Gibt die Datei sortiert werden soll. Wenn kein Dateiname angegeben wird, ist die Standardeingabe sortiert. Gibt die Datei ist schneller als das Umleiten von derselben Datei als Eingabe.|
|/ t [\<Laufwerk2 >:] [\<Path2 >]|Gibt den Pfad des Verzeichnisses zum Speichern der **Sortierreihenfolge** Befehl der Speicher arbeiten, wenn die Daten nicht in den Hauptspeicher passen. Standardmäßig wird das temporäre Systemverzeichnis verwendet.|
|/ o [\<Laufwerk3 >:] [\<Pfad3 >]\<Datei3 >|Gibt die Datei, in die sortierten Daten gespeichert werden. Wenn nicht angegeben, werden die Daten an die Standardausgabe geschrieben. Angeben der Ausgabedatei ist schneller als die Umleitung der Standardausgabe in die gleiche Datei.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Mithilfe der **/+** Befehlszeilenoption

    Standardmäßig beginnt der Vergleich am ersten Zeichen der einzelnen Zeilen. Die **/+** Befehlszeilenoption startet Vergleiche mit dem Zeichen, die angegeben wird *N*. Z. B. `/+3` gibt an, dass jeder Vergleich mit dem dritten Zeichen jeder Zeile beginnen soll. Zeilen mit weniger als *N* Zeichen vor den anderen Zeilen sortieren.
-   Mithilfe der **/m** Befehlszeilenoption

    Der verwendete Arbeitsspeicher ist immer mindestens 160 KB. Wenn die Speichergröße angegeben wird, wird die genaue angegebene Betrag verwendet, für die Sortierung (muss mindestens 160 KB sein), unabhängig davon, wie viel Arbeitsspeicher verfügbar ist.

    Die standardmäßige maximale Arbeitsspeichergröße, wenn keine Größe angegeben wurde ist andernfalls 90 Prozent des verfügbaren Arbeitsspeichers, wenn die ein- und Ausgabe-Dateien sind oder 45 Prozent der Hauptspeicher. In der Regel die Standardeinstellung bietet die beste Leistung.
-   Mithilfe der **/l** Befehlszeilenoption

    Derzeit ist die einzige alternative für das Standardgebietsschema Gebietsschema "C", das schneller als das Sortieren von natürlicher Sprache (sortiert Zeichen entsprechend ihren binären Codierungen) ist.
-   Mit der Umleitungssymbolen mit der **Sortierreihenfolge** Befehl

    Können Sie das Pipe-Symbol (**|**) zum Weiterleiten von Eingabedaten in der **Sortierreihenfolge** Befehl von einem anderen Befehl oder sortierte Ausgabe an einen anderen Befehl weiterleiten. Sie können Eingabe-und Ausgabedateien angeben, indem Sie die Umleitungssymbole (**<** oder **>**). Es kann schneller und effizienter (vor allem bei großen Dateien) sein, um die Eingabedatei direkt anzugeben (gemäß *Dateiname1* in der Befehlssyntax), und geben Sie dann auf die Ausgabe mithilfe der **/o** der Parameter.
-   Groß-/Kleinschreibung

    Die **Sortierreihenfolge** Befehl unterscheidet nicht zwischen Groß-und Kleinbuchstaben.
-   Beschränkungen hinsichtlich der Dateigröße

    Die **Sortierreihenfolge** Befehl gibt es keine Beschränkung für die Dateigröße.
-   Sortierreihenfolge

    Das Sortieren-Programm verwendet die Sortierreihenfolge-Sequence-Tabelle, die die Einstellungen für Land/Region-Code und Codepage-entspricht. Größer als ASCII-Code 127 Zeichen sortiert auf Basis der Informationen in der Country.sys-Datei oder einer anderen Datei, die gemäß der **Land** Befehl in der config-Datei.
-   Speicherauslastung

    Wenn die Sortierung in die maximale Speichergröße passt (Standard oder gemäß der **/m** Parameter), die Sortierung erfolgt in einem einzelnen Durchlauf. Andernfalls wird die Sortierung erfolgt in zwei separaten sortieren und Zusammenführen-Durchläufe, und die Mengen von Arbeitsspeicher, die beide Durchläufe zum sind gleich. Wenn zwei Durchläufe ausgeführt werden, werden die teilweise sortierten Daten in einer temporären Datei auf dem Datenträger gespeichert. Wenn nicht genügend Arbeitsspeicher zum Ausführen der Sortierung in zwei Durchgängen vorhanden ist, wird ein Laufzeitfehler ausgegeben. Wenn die **/m** Befehlszeilenoption verwendet, um anzugeben, mehr Speicher als tatsächlich verfügbar ist, eine Verringerung der Leistung oder ein Laufzeitfehler auftreten kann.

## <a name="BKMK_examples"></a>Beispiele für

**Sortieren einer Datei**

Zum Sortieren und in umgekehrter Reihenfolge der Zeilen in einer Datei namens Expenses.txt anzuzeigen, geben Sie Folgendes ein:

`sort /r expenses.txt`

**Sortieren die Ausgabe eines Befehls**

Um eine große Datei Maillist.txt für den Text "Jones" und zum Sortieren der Ergebnisse der Suche, verwenden Sie den senkrechten Strich (|), leiten Sie die Ausgabe des eine **finden** Befehl die **Sortierreihenfolge** Befehl wie folgt:

`find "Jones" maillist.txt | sort`

Der Befehl erzeugt eine sortierte Liste von Zeilen, die den angegebenen Text enthalten.

**Sortieren von Tastatureingaben**

Um Tastatureingaben zu sortieren, und die Ergebnisse alphabetisch auf dem Bildschirm angezeigt, können Sie zuerst die **Sortierreihenfolge** Befehl ohne Parameter wie folgt:

`sort`

Klicken Sie dann geben Sie den Text an, dem sortiert werden sollen, und drücken Sie die EINGABETASTE am Ende jeder Zeile. Wenn Sie die Vorgabe abgeschlossen haben, drücken Sie STRG + Z, und drücken Sie dann die EINGABETASTE. Die **Sortierreihenfolge** Befehl zeigt den Text, die Sie eingegeben haben, alphabetisch sortiert.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)