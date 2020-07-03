---
title: fc
description: Referenz Artikel für den FC-Befehl, der zwei Dateien oder Datei Sätze vergleicht und die Unterschiede zwischen Ihnen anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 485fc3d8-b7c5-496d-87be-0011112f27d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d9e12853d2634f7e7bcbd976b6c301f8e02c0dc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930480"
---
# <a name="fc"></a>fc

Vergleicht zwei Dateien oder Sätze von Dateien und zeigt die Unterschiede zwischen diesen an.

## <a name="syntax"></a>Syntax

```
fc /a [/c] [/l] [/lb<n>] [/n] [/off[line]] [/t] [/u] [/w] [/<nnnn>] [<drive1>:][<path1>]<filename1> [<drive2>:][<path2>]<filename2>
fc /b [<drive1:>][<path1>]<filename1> [<drive2:>][<path2>]<filename2>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /a | Kürzt die Ausgabe eines ASCII-Vergleichs. Anstatt alle Zeilen anzuzeigen, die unterschiedlich sind, zeigt **FC** nur die erste und letzte Zeile für jeden Satz von Unterschieden an. |
| /b | Vergleicht die beiden Dateien im binären Modus, Byte nach Byte, und versucht nicht, die Dateien erneut zu synchronisieren, nachdem eine Übereinstimmung gefunden wurde. Dies ist der Standardmodus zum Vergleichen von Dateien, die die folgenden Dateierweiterungen aufweisen:. exe,. com,. sys,. obj,. lib oder. bin. |
| /C | Ignoriert den Großbuchstaben. |
| /l | Vergleicht die Dateien im ASCII-Modus (zeilenweise) und versucht, die Dateien erneut zu synchronisieren, nachdem eine Übereinstimmung gefunden wurde. Dies ist der Standardmodus zum Vergleichen von Dateien, mit Ausnahme von Dateien mit den folgenden Dateierweiterungen:. exe,. com,. sys,. obj,. lib oder. bin. |
| /lb`<n>` | Legt die Anzahl der Zeilen für den internen Zeilen Puffer auf *N*fest. Die Standardlänge des Zeilen Puffers beträgt 100 Zeilen. Wenn die zu vergleichenden Dateien mehr als 100 aufeinander folgende Zeilen aufweisen, bricht **FC** den Vergleich ab. |
| /n | Zeigt die Zeilennummern während eines ASCII-Vergleichs an. |
| /Off [Zeile] | Überspringt keine Dateien, für die das Offline-Attribut festgelegt ist. |
| /t | Verhindert, dass der **FC** Tabstopps in Leerzeichen umwandelt. Das Standardverhalten besteht darin, Tabstopps als Leerzeichen zu behandeln, wobei an der Position des achten Zeichens angehalten wird. |
| /U | Vergleicht Dateien als Unicode-Textdateien. |
| /w | Komprimiert Leerraum (d. h. Registerkarten und Leerzeichen) während des Vergleichs. Wenn eine Zeile viele aufeinander folgende Leerzeichen oder Registerkarten enthält, behandelt **/w** diese Zeichen als einzelnes Leerzeichen. Bei Verwendung mit **/w**ignoriert **FC** den Leerraum am Anfang und am Ende einer Zeile. |
| /`<nnnn>` | Gibt die Anzahl der aufeinander folgenden Zeilen an, die nach einem Konflikt übereinstimmen müssen, bevor **FC** die Dateien für die erneute Synchronisierung berücksichtigt. Wenn die Anzahl der übereinstimmenden Zeilen in den Dateien kleiner als *nnnn*ist, zeigt **FC** die übereinstimmenden Zeilen als Unterschiede an. Der Standardwert ist 2. |
| `[<drive1>:][<path1>]<filename1>` | Gibt den Speicherort und den Namen der ersten zu vergleichenden Datei oder Gruppe von Dateien an. *filename1* ist erforderlich. |
| `[<drive2>:][<path2>]<filename2>` | Gibt den Speicherort und den Namen der zweiten Datei oder Gruppe von Dateien an, die verglichen werden sollen. *filename2* ist erforderlich. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Dieser Befehl wird durch c:\WINDOWS\fc.exe implementiert. Sie können diesen Befehl in PowerShell verwenden, aber achten Sie darauf, die vollständige ausführbare Datei (fc.exe) zu benennen, da "FC" auch ein Alias für Format-Custom ist.

- Wenn Sie **FC** für einen ASCII-Vergleich verwenden, zeigt **FC** die Unterschiede zwischen zwei Dateien in der folgenden Reihenfolge an:

  - Name der ersten Datei

  - Zeilen aus *filename1* , die sich zwischen den Dateien unterscheiden.

  - Erste Zeile, die in beiden Dateien übereinstimmen soll

  - Name der zweiten Datei

  - Zeilen aus *filename2* , die unterschiedlich sind

  - Erste Zeile für Übereinstimmung

- **/b** zeigt Konflikte an, die während eines binären Vergleichs in der folgenden Syntax gefunden werden:

    `\<XXXXXXXX: YY ZZ>`

    Der Wert von *xxxxxxxx* gibt die relative hexadezimal Adresse für das Bytepaar an, gemessen ab dem Anfang der Datei. Adressen beginnen bei 00000000. Die hexadezimalen Werte für *yy* und *ZZ* stellen die nicht übereinstimmenden Bytes aus *filename1* bzw. *filename2*dar.

- Sie können Platzhalter Zeichen (**&#42;** und **?**) in *filename1* und *filename2*verwenden. Wenn Sie in *filename1*einen Platzhalter verwenden, vergleicht **FC** alle angegebenen Dateien mit der Datei oder dem Satz von Dateien, die von *filename2*angegeben werden. Wenn Sie in *filename2*einen Platzhalter verwenden, verwendet **FC** den entsprechenden Wert von *filename1*.

- Beim Vergleichen von ASCII-Dateien verwendet **FC** einen internen Puffer (groß genug zum Speichern von 100 Zeilen) als Speicher. Wenn die Dateien größer sind als der Puffer, vergleicht **FC** , was er in den Puffer laden kann. Wenn der **FC** keine Entsprechung in den geladenen Teilen der Dateien findet, wird er beendet und zeigt die folgende Meldung an:

    `Resynch failed. Files are too different.`

    Beim Vergleich von Binärdateien, die größer als der verfügbare Arbeitsspeicher sind, vergleicht **FC** beide Dateien vollständig und überlagert die Teile im Speicher mit den nächsten Teilen des Datenträgers. Die Ausgabe ist identisch mit der Ausgabe für Dateien, die vollständig in den Arbeitsspeicher passen.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen ASCII-Vergleich von zwei Textdateien ( *monatlich. rpt* und *Sales. rpt*) zu erstellen und die Ergebnisse in abgekürzten Format anzuzeigen:

```
fc /a monthly.rpt sales.rpt
```

Geben Sie Folgendes ein, um einen binären Vergleich von zwei Batch Dateien ( *profits.bat* und *earnings.bat*vorzunehmen:

```
fc /b profits.bat earnings.bat
```

Ähnliche Ergebnisse wie die folgenden werden angezeigt:

```
00000002: 72 43
00000004: 65 3A
0000000E: 56 92
000005E8: 00 6E
FC: earnings.bat longer than profits.bat
```

Wenn die profits.bat-und earnings.bat Dateien identisch sind, zeigt **FC** die folgende Meldung an:

```
Comparing files profits.bat and earnings.bat
FC: no differences encountered
```

Wenn Sie jede bat-Datei im aktuellen Verzeichnis mit der Datei *new.bat*vergleichen möchten, geben Sie Folgendes ein:

```
fc *.bat new.bat
```

Wenn Sie die Datei *new.bat* auf Laufwerk C mit der Datei *new.bat* auf Laufwerk D vergleichen möchten, geben Sie Folgendes ein:

```
fc c:new.bat d:*.bat
```

Geben Sie Folgendes ein, um die einzelnen Batch Dateien im Stammverzeichnis auf Laufwerk C mit der Datei mit demselben Namen im Stammverzeichnis auf Laufwerk D zu vergleichen:

```
fc c:*.bat d:*.bat
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
