---
title: fc
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 485fc3d8-b7c5-496d-87be-0011112f27d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b358b8c1bf44b5b7942cef05bd09fa8cac850a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844743"
---
# <a name="fc"></a>fc



Vergleicht zwei Dateien oder Sätze von Dateien und zeigt die Unterschiede zwischen diesen an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fc /a [/c] [/l] [/lb<N>] [/n] [/off[line]] [/t] [/u] [/w] [/<NNNN>] [<Drive1>:][<Path1>]<FileName1> [<Drive2>:][<Path2>]<FileName2>
fc /b [<Drive1:>][<Path1>]<FileName1> [<Drive2:>][<Path2>]<FileName2>
```

### <a name="parameters"></a>Parameter

|            Parameter             |                                                                                                                                     Beschreibung                                                                                                                                      |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                /a                |                                                 Kürzt die Ausgabe eines ASCII-Vergleichs. Anstatt alle Zeilen anzuzeigen, die unterschiedlich sind, zeigt **FC** nur die erste und letzte Zeile für jeden Satz von Unterschieden an.                                                  |
|                /b                |             Vergleicht die beiden Dateien im binären Modus, Byte nach Byte, und versucht nicht, die Dateien erneut zu synchronisieren, nachdem eine Übereinstimmung gefunden wurde. Dies ist der Standardmodus zum Vergleichen von Dateien, die die folgenden Dateierweiterungen aufweisen:. exe,. com,. sys,. obj,. lib oder. bin.              |
|                /c                |                                                                                                                               Ignoriert den Großbuchstaben.                                                                                                                               |
|                /l                |               Vergleicht die Dateien im ASCII-Modus (zeilenweise) und versucht, die Dateien erneut zu synchronisieren, nachdem eine Übereinstimmung gefunden wurde. Dies ist der Standardmodus zum Vergleichen von Dateien, mit Ausnahme von Dateien mit den folgenden Dateierweiterungen:. exe,. com,. sys,. obj,. lib oder. bin.                |
|             /LB\<N >              |                         Legt die Anzahl der Zeilen für den internen Zeilen Puffer auf *N*fest. Die Standardlänge des Zeilen Puffers beträgt 100 Zeilen. Wenn die zu vergleichenden Dateien mehr als 100 aufeinander folgende Zeilen aufweisen, bricht **FC** den Vergleich ab.                         |
|                /n                |                                                                                                                Zeigt die Zeilennummern während eines ASCII-Vergleichs an.                                                                                                                 |
|            /Off [Zeile]            |                                                                                                               Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist.                                                                                                               |
|                /t                |                                                                    Verhindert, dass der **FC** Tabstopps in Leerzeichen umwandelt. Das Standardverhalten besteht darin, Tabstopps als Leerzeichen zu behandeln, wobei an der Position des achten Zeichens angehalten wird.                                                                    |
|                /u                |                                                                                                                        Vergleicht Dateien als Unicode-Textdateien.                                                                                                                         |
|                /w                |         Komprimiert Leerraum (d. h. Registerkarten und Leerzeichen) während des Vergleichs. Wenn eine Zeile viele aufeinander folgende Leerzeichen oder Registerkarten enthält, behandelt **/w** diese Zeichen als einzelnes Leerzeichen. Bei Verwendung mit **/w**ignoriert **FC** den Leerraum am Anfang und am Ende einer Zeile.         |
|             /\<nnnn >             | Gibt die Anzahl der aufeinander folgenden Zeilen an, die nach einem Konflikt übereinstimmen müssen, bevor **FC** die Dateien für die erneute Synchronisierung berücksichtigt. Wenn die Anzahl der übereinstimmenden Zeilen in den Dateien kleiner als *nnnn*ist, zeigt **FC** die übereinstimmenden Zeilen als Unterschiede an. Der Standardwert ist 2. |
| [\<Drive1 >:] [<Path1>]<FileName1> |                                                                                        Gibt den Speicherort und den Namen der ersten zu vergleichenden Datei oder Gruppe von Dateien an. *FileName1* ist erforderlich.                                                                                        |
| [\<drive2 >:] [<Path2>]<FileName2> |                                                                                       Gibt den Speicherort und den Namen der zweiten Datei oder Gruppe von Dateien an, die verglichen werden sollen. *FileName2* ist erforderlich.                                                                                        |
|                /?                |                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                         |

## <a name="remarks"></a>Hinweise

-   Dieser Befehl wird durch c:\windows\fc.exe implementiert. Sie können diesen Befehl in PowerShell verwenden, aber achten Sie darauf, die vollständige ausführbare Datei (FC. exe) zu benennen, da "FC" ein Alias für Format-Custom ist.

-   Melden von Unterschieden zwischen Dateien für einen ASCII-Vergleich

    Wenn Sie **FC** für einen ASCII-Vergleich verwenden, zeigt **FC** die Unterschiede zwischen zwei Dateien in der folgenden Reihenfolge an:  
    -   Name der ersten Datei
    -   Zeilen aus *FileName1* , die sich zwischen den Dateien unterscheiden.
    -   Erste Zeile, die in beiden Dateien übereinstimmen soll
    -   Name der zweiten Datei
    -   Zeilen aus *FileName2* , die unterschiedlich sind
    -   Erste Zeile für Übereinstimmung
-   Verwenden von **/b** für binäre Vergleiche

    **/b** zeigt Konflikte an, die während eines binären Vergleichs in der folgenden Syntax gefunden werden:

    `\<XXXXXXXX: YY ZZ>`

    Der Wert von *xxxxxxxx* gibt die relative hexadezimal Adresse für das Bytepaar an, gemessen ab dem Anfang der Datei. Adressen beginnen bei 00000000. Die hexadezimalen Werte für *yy* und *ZZ* stellen die nicht übereinstimmenden Bytes aus *FileName1* bzw. *FileName2*dar.
-   Verwenden von Platzhalter Zeichen

    Sie können Platzhalter Zeichen ( **&#42;** und **?** ) in *FileName1* und *FileName2*verwenden. Wenn Sie in *FileName1*einen Platzhalter verwenden, vergleicht **FC** alle angegebenen Dateien mit der Datei oder dem Satz von Dateien, die von *FileName2*angegeben werden. Wenn Sie in *FileName2*einen Platzhalter verwenden, verwendet **FC** den entsprechenden Wert von *FileName1*.
-   Arbeiten mit Arbeitsspeicher

    Beim Vergleichen von ASCII-Dateien verwendet **FC** einen internen Puffer (groß genug zum Speichern von 100 Zeilen) als Speicher. Wenn die Dateien größer sind als der Puffer, vergleicht **FC** , was er in den Puffer laden kann. Wenn der **FC** keine Entsprechung in den geladenen Teilen der Dateien findet, wird er beendet und zeigt die folgende Meldung an:

    `Resynch failed. Files are too different.`

    Beim Vergleich von Binärdateien, die größer als der verfügbare Arbeitsspeicher sind, vergleicht **FC** beide Dateien vollständig und überlagert die Teile im Speicher mit den nächsten Teilen des Datenträgers. Die Ausgabe ist identisch mit der Ausgabe für Dateien, die vollständig in den Arbeitsspeicher passen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um einen ASCII-Vergleich von zwei Textdateien (monatlich. rpt und Sales. rpt) zu erstellen und die Ergebnisse in abgekürzten Format anzuzeigen:
```
fc /a monthly.rpt sales.rpt 
```
Geben Sie Folgendes ein, um einen binären Vergleich von zwei Batch Dateien (Profit. bat und Gewinn. bat) vorzunehmen:
```
fc /b profits.bat earnings.bat
```
Ähnliche Ergebnisse wie die folgenden werden angezeigt:
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
Wenn die Dateien "Profit. bat" und "Profit. bat" identisch sind, zeigt **FC** die folgende Meldung an:
```
Comparing files Profits.bat and Earnings.bat
FC: no differences encountered
```
Wenn Sie jede bat-Datei im aktuellen Verzeichnis mit der Datei "New. bat" vergleichen möchten, geben Sie Folgendes ein:
```
fc *.bat new.bat
```
Geben Sie Folgendes ein, um die Datei New. bat auf Laufwerk C mit der Datei New. bat auf Laufwerk D zu vergleichen:
```
fc c:new.bat d:*.bat
```
Geben Sie Folgendes ein, um die einzelnen Batch Dateien im Stammverzeichnis auf Laufwerk C mit der Datei mit demselben Namen im Stammverzeichnis auf Laufwerk D zu vergleichen:
```
fc c:*.bat d:*.bat
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
