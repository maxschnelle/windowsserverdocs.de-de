---
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
title: Fsutil-wim
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c9186721ce4d3a549964e420cbc16d4893a1859d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826041"
---
# <a name="fsutil-wim"></a>Fsutil-wim
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10

Stellt Funktionen zur Erkennung und Verwaltung von Windows-Image-WIM-gesicherten Dateien bereit.

## <a name="syntax"></a>Syntax

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|EnumFiles|Listet unterstützt WIM-Dateien.|
|\<Laufwerkname >|Gibt den Namen des Laufwerks an.|
|\<Datenquelle >|Gibt die Datenquelle an.|
|enumwims|Listet die WIM-Dateien sichern.|
|queryfile|Abfragen, wenn die Datei von WIM-Datei unterstützt wird und wenn dies der Fall ist, Details über die WIM-Datei zeigt.|
|\<filename>|Gibt den Dateinamen an.|
|removewim|Entfernt eine WIM-Datei von Sicherungsdateien an.|




### <a name="examples"></a>Beispiele

Um die Dateien für Laufwerk C: aus der Datenquelle 0 aufzulisten, geben Sie Folgendes ein:

```
fsutil wim enumfiles C: 0
```

Zum Auflisten von WIM-Dateien für Laufwerk C: Sichern, geben Sie Folgendes ein:

```
fsutil wim enumwims C:
```

Um festzustellen, ob eine Datei von WIM-Datei unterstützt wird, geben Sie Folgendes ein:

```
fsutil wim C:\Windows\Notepad.exe
```

Um die WIM-Datei aus den Sicherungsdateien für Volume "c:" und die Datenquelle 2 zu entfernen, geben Sie Folgendes ein:

```
fsutil wim removewims C: 2
```

### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)