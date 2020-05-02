---
ms.assetid: 6c6ff819-f349-4aea-b0be-1f637f631736
title: Wim
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 12a9965515ef26e0cbccb2d20d25f66b54b23b8a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720064"
---
# <a name="fsutil-wim"></a>Wim
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10

Stellt Funktionen zum Ermitteln und Verwalten von Dateien mit Windows-Abbildern (WIM) bereit.

## <a name="syntax"></a>Syntax

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------------|---------------|
|EnumFiles|Listet WIM-gestützte Dateien auf.|
|\<Laufwerks Name>|Gibt den Namen des Laufwerks an.|
|\<Datenquellen>|Gibt die Datenquelle an.|
|enumwims|Listet die unterstützten WIM-Dateien auf.|
|QueryFile|Fragt ab, ob die Datei durch WIM unterstützt wird, und zeigt ggf. Details zur WIM-Datei an.|
|\<Dateiname>|Gibt den Dateinamen an.|
|removewim|Entfernt eine WIM-Datei aus Unterstützungs Dateien.|




### <a name="examples"></a>Beispiele

Zum Auflisten der Dateien für Laufwerk C: Geben Sie aus der Datenquelle 0 Folgendes ein:

```
fsutil wim enumfiles C: 0
```

Geben Sie Folgendes ein, um die zugrunde liegenden WIM-Dateien für Laufwerk C: aufzuzählen:

```
fsutil wim enumwims C:
```

Um festzustellen, ob eine Datei durch WIM unterstützt wird, geben Sie Folgendes ein:

```
fsutil wim C:\Windows\Notepad.exe
```

Geben Sie Folgendes ein, um die WIM-Datei aus den Unterstützungs Dateien für Volume C: und Data Source 2 zu entfernen:

```
fsutil wim removewims C: 2
```

### <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)