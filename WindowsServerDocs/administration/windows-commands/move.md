---
title: Verschieben
description: Referenz Thema für den Move-Befehl, mit dem eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis verschoben werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 283ee793769d991c1932eb2271c5117354bdf6a4
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354501"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
