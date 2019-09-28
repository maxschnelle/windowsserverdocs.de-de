---
title: move
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fde290a8-d385-450f-8987-ee837fed667d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4302a3403f73892500c3f9deb608e9489c7e91ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373527"
---
# <a name="move"></a>move



Verschiebt eine oder mehrere Dateien aus einem Verzeichnis in ein anderes Verzeichnis.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
move [{/y | /-y}] [<Source>] [<Target>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/y|Unterdrückt die Eingabeaufforderung, um zu bestätigen, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|/-y|Bewirkt, dass die Aufforderung bestätigt, dass Sie eine vorhandene Zieldatei überschreiben möchten.|
|> der @no__t 0quelle|Gibt den Pfad und den Namen der zu verschiebenden Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Quelle* der aktuelle Verzeichnispfad und-Name sein.|
|\<target >|Gibt den Pfad und den Namen zum Verschieben von Dateien an. Wenn Sie ein Verzeichnis verschieben oder umbenennen möchten, sollte *Ziel* der gewünschte Verzeichnispfad und-Name sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die Befehlszeilenoption **/y** kann in der COPYCMD-Umgebungsvariablen voreingestellt sein. Sie können dies mit **/-y** in der Befehlszeile überschreiben. Der Standardwert ist die Eingabeaufforderung vor dem Überschreiben von Dateien, es sei denn, der **Kopier** Befehl wird innerhalb eines Batch Skripts ausgeführt.
-   Das Verschieben verschlüsselter Dateien auf ein Volume, das Verschlüsselndes Dateisystem (EFS) nicht unterstützt, führt zu einem Fehler. Entschlüsseln Sie zuerst die Dateien, oder verschieben Sie die Dateien auf ein Volume, das EFS unterstützt.

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie alle Dateien mit der Erweiterung. xls aus dem Verzeichnis \Data in das Verzeichnis \Second_Q\Reports verschieben möchten, geben Sie Folgendes ein:
```
move \data\*.xls \second_q\reports\ 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)