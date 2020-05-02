---
title: Verschieben
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1df37753239fea5d5ba9ba22256706a47d4c6a2f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723913"
---
# <a name="move"></a>Verschieben



Verschiebt eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis.



## <a name="syntax"></a>Syntax

```
move [{/y | /-y}] [<Source>] [<Target>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/y|Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|/-y|Bewirkt, dass die Aufforderung bestätigt, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|\<Quell>|Gibt den Pfad und den Namen der zu verschiebenden Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Quelle* der aktuelle Verzeichnispfad und-Name sein.|
|\<Target>|Gibt den Pfad und den Namen zum Verschieben von Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Ziel* der gewünschte Verzeichnispfad und-Name sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Die Befehlszeilenoption **/y** kann in der COPYCMD-Umgebungsvariablen voreingestellt sein. Sie können dies mit **/-y** in der Befehlszeile überschreiben. Der Standardwert ist die Eingabeaufforderung vor dem Überschreiben von Dateien, es sei denn, der **Kopier** Befehl wird innerhalb eines Batch Skripts ausgeführt.
-   Das Verschieben verschlüsselter Dateien auf ein Volume, das Verschlüsselndes Dateisystem (EFS) nicht unterstützt, führt zu einem Fehler. Entschlüsseln Sie zuerst die Dateien, oder verschieben Sie die Dateien auf ein Volume, das EFS unterstützt.

## <a name="examples"></a>Beispiele

Wenn Sie alle Dateien mit der Erweiterung. xls aus dem Verzeichnis \Data in das Verzeichnis \ Second_Q \Reports verschieben möchten, geben Sie Folgendes ein:
```
move \data\*.xls \second_q\reports\ 
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)