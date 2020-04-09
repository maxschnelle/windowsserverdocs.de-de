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
ms.openlocfilehash: d4a8f2c008c1a28e498edb7726a8c209e91f41af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843923"
---
# <a name="fsutil-wim"></a>Wim
>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

Stellt Funktionen zum Ermitteln und Verwalten von Dateien mit Windows-Abbildern (WIM) bereit.

## <a name="syntax"></a>Syntax

```
fsutil wim [enumfiles] <drive name> <data source>
fsutil wim [enumwims] <drive name>
fsutil wim [queryfile] <filename>
fsutil wim [removewim] <drive name> <data source>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|EnumFiles|Listet WIM-gestützte Dateien auf.|
|Name des \<Laufwerks >|Gibt den Namen des Laufwerks an.|
|\<Datenquelle >|Gibt die Datenquelle an.|
|enumwims|Listet die unterstützten WIM-Dateien auf.|
|QueryFile|Fragt ab, ob die Datei durch WIM unterstützt wird, und zeigt ggf. Details zur WIM-Datei an.|
|\<Dateiname >|Gibt den Dateinamen an.|
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