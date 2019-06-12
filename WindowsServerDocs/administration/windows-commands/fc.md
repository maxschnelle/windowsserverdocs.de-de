---
title: fc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 485fc3d8-b7c5-496d-87be-0011112f27d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7ccc3d268b58bfa5e848f2336f4315baae8b4e1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439311"
---
# <a name="fc"></a>fc



Vergleicht zwei Dateien oder Dateigruppen, und zeigt die Unterschiede zwischen ihnen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fc /a [/c] [/l] [/lb<N>] [/n] [/off[line]] [/t] [/u] [/w] [/<NNNN>] [<Drive1>:][<Path1>]<FileName1> [<Drive2>:][<Path2>]<FileName2>
fc /b [<Drive1:>][<Path1>]<FileName1> [<Drive2:>][<Path2>]<FileName2>
```

## <a name="parameters"></a>Parameter

|            Parameter             |                                                                                                                                     Beschreibung                                                                                                                                      |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                /a                |                                                 Kürzt die Ausgabe des einen ASCII-Vergleich. Anstatt alle Zeilen, die unterschiedlich sind, **fc** zeigt nur die erste und letzte Zeile für jeden Satz von unterschieden.                                                  |
|                /b                |             Vergleicht die beiden Dateien im binären Modus byteweise und versucht nicht, die Dateien zu synchronisieren, nach einer fehlenden Übereinstimmung suchen. Dies ist der Standardmodus für das Vergleichen von Dateien, die die folgenden Dateierweiterungen aufweisen: .exe, .com, .sys, .obj, .lib oder bin.              |
|                /c                |                                                                                                                               Die Groß-/Kleinschreibung wird ignoriert.                                                                                                                               |
|                /l                |               Vergleicht die Dateien im ASCII-Modus, Zeile für Zeile und versucht, die Dateien zu synchronisieren, nach einer fehlenden Übereinstimmung suchen. Dies ist der Standardmodus für das Vergleichen von Dateien, mit Ausnahme der Dateien mit folgenden Erweiterungen: .exe, .com, .sys, .obj, .lib oder bin.                |
|             /lb\<N>              |                         Legt die Anzahl der Zeilen für die interne Branchen-Puffer zu *N*. Die standardmäßige Länge des Puffers Zeile beträgt 100 Zeilen. Wenn die Dateien, die Sie vergleichen, mehr als 100 aufeinander folgende unterschiedliche Zeilen haben **fc** bricht den Vergleich ab.                         |
|                /n                |                                                                                                                Zeigt die Zeilennummern während eines ASCII-Vergleichs an.                                                                                                                 |
|            /off[line]            |                                                                                                               Dateien, die das Attribut "offline" festgelegt ist, werden nicht übersprungen werden.                                                                                                               |
|                /t                |                                                                    Verhindert, dass **fc** von Tabstopps in Leerzeichen konvertiert. Das Standardverhalten ist, Registerkarten als Leerzeichen, mit beendet wird, an jede achte Zeichenposition zu behandeln.                                                                    |
|                /u                |                                                                                                                        Dateien werden als Unicode-Textdateien verglichen.                                                                                                                         |
|                /w                |         Komprimiert Leerzeichen (d. h. Registerkarten und Leerzeichen) während des Vergleichs an. Enthält eine Zeile viele aufeinander folgende Leerzeichen oder Tabstopps, **/w** behandelt diese Zeichen als ein einzelnes Leerzeichen. Bei Verwendung mit **/w**, **fc** Leerraum am Anfang und Ende einer Zeile ignoriert.         |
|             /\<NNNN>             | Gibt die Anzahl der aufeinander folgenden Zeilen, die folgenden keine Übereinstimmung gefunden,, bevor übereinstimmen muss **fc** neu synchronisiert werden die Dateien als identisch betrachtet. Wenn die Anzahl der übereinstimmenden Zeilen in den Dateien ist kleiner als *NNNN*, **fc** zeigt die übereinstimmenden Zeilen als Unterschiede. Der Standardwert ist 2. |
| [\<Drive1>:][<Path1>]<FileName1> |                                                                                        Gibt den Speicherort und Namen der ersten Datei oder den Satz von Dateien, verglichen werden soll. *Dateiname1* ist erforderlich.                                                                                        |
| [\<Drive2>:][<Path2>]<FileName2> |                                                                                       Gibt den Speicherort und Namen der zweiten Datei oder den Satz von Dateien, verglichen werden soll. *Dateiname2* ist erforderlich.                                                                                        |
|                /?                |                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                         |

## <a name="remarks"></a>Hinweise

-   Dieser Befehl ist Implemeted von c:\WINDOWS\fc.exe. Sie können diesen Befehl in PowerShell verwenden, aber Achten Sie darauf, dass Sie die vollständige ausführbare Datei (fc.exe) ausgeschrieben, da "fc" ein Alias für die Format-Custom ist.

-   Unterschiede zwischen Dateien für einen Vergleich der ASCII-berichterstellung

    Bei Verwendung von **fc** für ein ASCII-Vergleich, **fc** zeigt die Unterschiede zwischen zwei Dateien in der folgenden Reihenfolge:  
    -   Name der ersten Datei
    -   Zeilen aus *Dateiname1* unterscheiden, die die Dateien
    -   Erste Zeile in beiden Dateien übereinstimmen
    -   Name der zweiten Datei
    -   Zeilen aus *Dateiname2* , die sich unterscheiden.
    -   Erste übereinstimmende Zeile
-   Mithilfe von **/b** für binäre Vergleiche

    **/ b** zeigt Konflikte, die während der einen binären Vergleich, in der folgenden Syntax gefunden werden:

    `\<XXXXXXXX: YY ZZ>`

    Der Wert des *XXXXXXXX* gibt an, die hexadezimale relative Adresse für das Paar von Bytes, gemessen ab dem Anfang der Datei. Adressen beginnen bei "00000000" fest. Die Hexadezimalwerte für *YY* und *ZZ* darstellen der nicht übereinstimmenden Bytes von *Dateiname1* und *Dateiname2*bzw.
-   Verwenden von Platzhalterzeichen

    Sie können Platzhalterzeichen verwenden ( **&#42;** und **?** ) in *Dateiname1* und *Dateiname2*. Bei Verwendung ein Platzhalters in *Dateiname1*, **fc** vergleicht die angegebenen Dateien in die Datei oder einen Satz von Dateien, die anhand des *Dateiname2*. Bei Verwendung ein Platzhalters in *Dateiname2*, **fc** verwendet den entsprechenden Wert von *Dateiname1*.
-   Arbeiten mit dem Arbeitsspeicher

    Beim Vergleichen von ASCII-Dateien, **fc** verwendet einen internen Puffer (groß genug für 100 Zeilen) als Speicher. Wenn die Dateien größer als der Puffer, sind **fc** vergleicht, was in den Puffer geladen werden kann. Wenn **fc** findet keine Übereinstimmung in der geladenen Teile der Dateien, beendet und wird die folgende Meldung angezeigt:

    `Resynch failed. Files are too different.`

    Beim Vergleich von Binärdateien, die größer als der verfügbare Arbeitsspeicher ist, sind **fc** vergleicht die beiden Dateien vollständig zu überlagern die Teile im Arbeitsspeicher mit den nächsten Teilen auf den Datenträger. Die Ausgabe ist identisch, die für Dateien, die vollständig in den Arbeitsspeicher passen.

## <a name="BKMK_examples"></a>Beispiele für

Um einen ASCII-Vergleich der beiden Textdateien, Monat.ber und Verkauf.ber, und die Ergebnisse in abgekürztem Format angezeigt, geben Sie Folgendes ein:
```
fc /a monthly.rpt sales.rpt 
```
Geben Sie Folgendes ein, um einen binären Vergleich von zwei Batchdateien, Gewinn.bat und Earnings.bat, machen:
```
fc /b profits.bat earnings.bat
```
Die Ergebnisse wie folgt aussehen:
```
00000002: 72 43
00000004: 65 3A
0000000E: 56 92
...
...
...
000005E8: 00 6E
FC: Earnings.bat longer than Profits.bat
```
Falls die Gewinn.bat und Earnings.bat Dateien identisch sind **fc** wird die folgende Meldung angezeigt:
```
Comparing files Profits.bat and Earnings.bat
FC: no differences encountered
```
Um alle bat-Datei im aktuellen Verzeichnis mit der Datei neu.bat vergleichen möchten, geben Sie Folgendes ein:
```
fc *.bat new.bat
```
Um die Datei neu.bat auf Laufwerk C mit der Datei neu.bat auf Laufwerk D: vergleichen möchten, geben Sie Folgendes ein:
```
fc c:new.bat d:*.bat
```
Um jedes Batch-Datei im Stammverzeichnis auf Laufwerk C in die Datei mit dem gleichen Namen in das Stammverzeichnis von Laufwerk D: vergleichen möchten, geben Sie Folgendes ein:
```
fc c:*.bat d:*.bat
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
