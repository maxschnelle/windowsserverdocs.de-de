---
title: compact
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 068111b293a3eb3987b14744a1bfcf2fde26bced
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826031"
---
# <a name="compact"></a>compact



Die Komprimierung von Dateien oder Verzeichnisse auf NTFS-Partitionen ändert oder zeigt. Wenn Sie ohne Angabe von Parametern **compact** zeigt den Komprimierungsstatus der das aktuelle Verzeichnis und die darin enthaltenen Dateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
compact [/c | /u] [/s[:<Dir>]] [/a] [/i] [/f] [/q] [<FileName>[...]]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/c|Komprimiert das angegebene Verzeichnis oder Datei an.|
|/u|Dekomprimiert das angegebene Verzeichnis oder Datei an.|
|/s[:\<Dir>]|Wendet die **compact** Befehl auf alle Unterverzeichnisse des angegebenen Verzeichnisses (oder das aktuelle Verzeichnis, wenn keine Angabe erfolgt).|
|/a|Zeigt ausgeblendete Dateien oder Systemdateien.|
|/i|Fehler werden ignoriert.|
|/f|Erzwingt, dass Komprimierung oder dekomprimierung des angegebenen Verzeichnisses oder der Datei. **/ f** wird verwendet, bei dem eine Datei, die teilweise komprimiert wurde, wenn Sie der Vorgang nach einem Systemabsturz unterbrochen wurde. Um die Datei in seiner Gesamtheit komprimiert zu erzwingen, verwenden die **/c** und **/f** Parameter, und geben Sie die teilweise komprimierte Datei.|
|/q|Gibt nur die wichtige Informationen an.|
|\<FileName>|Gibt an, die Datei oder das Verzeichnis. Sie können mehrere Dateinamen, und die **&#42;** und **?** Platzhalterzeichen enthalten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **compact** Befehl ist die Befehlszeilenversion des die Komprimierungsfunktion des NTFS-Dateisystems. Der Komprimierungsstatus eines Verzeichnisses gibt an, ob Dateien automatisch komprimiert werden, wenn sie zu dem Verzeichnis hinzugefügt werden. Festlegen des Komprimierungsstatus eines Verzeichnisses wird nicht unbedingt den Komprimierungsstatus der Dateien geändert, die bereits im Verzeichnis sind.
-   Sie können keine **compact** , Lese-, Schreib- oder Mount-Volumes, die mit DriveSpace oder DoubleSpace komprimiert wurden.
-   Sie können keine **compact** Dateizuordnungstabelle (FAT) oder FAT32-Partitionen zu komprimieren.

## <a name="BKMK_examples"></a>Beispiele für

Um den Komprimierungsstatus der im aktuellen Verzeichnis, seine Unterverzeichnisse und vorhandene Dateien festzulegen, geben Sie Folgendes ein:
```
compact /c /s 
```
Geben Sie Folgendes ein, um den Komprimierungsstatus der Dateien und Unterverzeichnisse im aktuellen Verzeichnis ohne eine Änderung des Komprimierungsstatus des aktuellen Verzeichnisses selbst festzulegen:
```
compact /c /s *.*
```
Geben Sie Folgendes ein, um ein Volume, aus dem Stammverzeichnis des Volumes, komprimieren:
```
compact /c /i /s:\
```

> [!NOTE]
> In diesem Beispiel wird der Komprimierungsstatus aller Verzeichnisse (einschließlich der Root-Verzeichnis auf dem Datenträger) und komprimiert jede Datei auf dem Volume. Die **/i** Parameter verhindert, dass Fehlermeldungen Komprimierungsprozess unterbrechen.

Geben Sie Folgendes ein, um alle Dateien mit der Dateinamenerweiterung des BMP-Datei im Verzeichnis \Tmp und allen Unterverzeichnissen des \Tmp, zu komprimieren, ohne die komprimierte Attribut der Verzeichnisse ändern:
```
compact /c /s:\tmp *.bmp
```
Um vollständige Komprimierung der Datei Zebra.bmp, zu erzwingen, die während eines Systemabsturzes teilweise komprimiert wurde, geben Sie Folgendes ein:
```
compact /c /f zebra.bmp
```
Um das komprimierte Attribut aus dem Verzeichnis C:\Tmp, ohne Änderung des Komprimierungsstatus von Dateien in dieses Verzeichnis zu entfernen, geben Sie Folgendes ein:
```
compact /u c:\tmp
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)