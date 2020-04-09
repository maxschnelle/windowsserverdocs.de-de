---
title: move
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: efd0cd0716c564a9570647820056ab9c38e41274
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839373"
---
# <a name="move"></a>move



Verschiebt eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
move [{/y | /-y}] [<Source>] [<Target>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/y|Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|/-y|Bewirkt, dass die Aufforderung bestätigt, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|> der \<Quelle|Gibt den Pfad und den Namen der zu verschiebenden Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Quelle* der aktuelle Verzeichnispfad und-Name sein.|
|\<Ziel >|Gibt den Pfad und den Namen zum Verschieben von Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Ziel* der gewünschte Verzeichnispfad und-Name sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die Befehlszeilenoption **/y** kann in der COPYCMD-Umgebungsvariablen voreingestellt sein. Sie können dies mit **/-y** in der Befehlszeile überschreiben. Der Standardwert ist die Eingabeaufforderung vor dem Überschreiben von Dateien, es sei denn, der **Kopier** Befehl wird innerhalb eines Batch Skripts ausgeführt.
-   Das Verschieben verschlüsselter Dateien auf ein Volume, das Verschlüsselndes Dateisystem (EFS) nicht unterstützt, führt zu einem Fehler. Entschlüsseln Sie zuerst die Dateien, oder verschieben Sie die Dateien auf ein Volume, das EFS unterstützt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Wenn Sie alle Dateien mit der Erweiterung. xls aus dem Verzeichnis \Data in das Verzeichnis \ Second_Q \Reports verschieben möchten, geben Sie Folgendes ein:
```
move \data\*.xls \second_q\reports\ 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)