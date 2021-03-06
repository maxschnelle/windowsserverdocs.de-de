---
title: Verschieben
description: Referenz Artikel für den Move-Befehl, mit dem eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis verschoben werden.
ms.topic: reference
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: cd68c7bcfa1f33eeb977a46a1687bbbab678420f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640565"
---
# <a name="move"></a>Verschieben

Verschiebt eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis.

> [!IMPORTANT]
> Das Verschieben verschlüsselter Dateien auf ein Volume, das Verschlüsselndes Dateisystem (EFS)-Ergebnisse nicht unterstützt, führt zu einem Fehler. Sie müssen die Dateien zunächst entschlüsseln oder auf ein Volume verschieben, das EFS unterstützt.

## <a name="syntax"></a>Syntax

```
move [{/y|-y}] [<source>] [<target>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /y | Beendet die Aufforderung zur Bestätigung, dass Sie eine vorhandene Zieldatei überschreiben möchten. Dieser Parameter kann in der COPYCMD-Umgebungsvariablen voreingestellt sein. Sie können diese Voreinstellung überschreiben, indem Sie den **-y-** Parameter verwenden. Der Standardwert ist die Eingabeaufforderung vor dem Überschreiben von Dateien, es sei denn, der Befehl wird innerhalb eines Batch Skripts ausgeführt. |
| -y | Startet die Aufforderung zur Bestätigung, dass Sie eine vorhandene Zieldatei überschreiben möchten. |
| `<source>` | Gibt den Pfad und den Namen der zu verschiebenden Dateien an. Zum Verschieben oder Umbenennen eines Verzeichnisses muss die *Quelle* der aktuelle Verzeichnispfad und-Name sein. |
| `<target>` | Gibt den Pfad und den Namen zum Verschieben von Dateien an. Um ein Verzeichnis zu verschieben oder umzubenennen, sollte das *Ziel* der gewünschte Verzeichnispfad und-Name sein. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie alle Dateien mit der Erweiterung. xls aus dem Verzeichnis *\Data* in das Verzeichnis *\ Second_Q \Reports* verschieben möchten, geben Sie Folgendes ein:

```
move \data\*.xls \second_q\reports\
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
