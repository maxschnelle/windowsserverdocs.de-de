---
title: move
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d651e586c31ff64664079bdd10ffde3701ec317d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824991"
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
|/y|Unterdrückt die Aufforderung zum bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|/-y|Bewirkt, dass aufgefordert um zu bestätigen, dass eine vorhandene Zieldatei überschrieben werden soll.|
|\<Quelle >|Gibt den Pfad und Namen der Datei oder des zu verschiebenden Dateien an. Wenn Sie ein Verzeichnis, verschieben oder umbenennen möchten *Quelle* muss der aktuelle Verzeichnispfad und Namen.|
|\<Target>|Gibt den Pfad und den Namen des zu verschiebenden Dateien an. Wenn Sie ein Verzeichnis, verschieben oder umbenennen möchten *Ziel* sollte sein, den gewünschten Verzeichnispfad und Namen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **/y** Befehlszeilenoption kann im-y voreingestellt werden. Sie können dies außer Kraft setzen mit **/-y** in der Befehlszeile. Der Standardwert ist, um die Bestätigung vor dem Überschreiben von Dateien, es sei denn, die **Kopie** Befehl in einem Batchskript ausgeführt wird.
-   Verschieben von verschlüsselten Dateien auf einem Volume, die nicht, Encrypting File System (EFS) führt zu einem Fehler unterstützt. Entschlüsseln Sie zunächst die Dateien oder verschieben Sie die Dateien auf einem Volume, die EFS unterstützt.

## <a name="BKMK_examples"></a>Beispiele für

Um alle Dateien mit der Erweiterung aus dem Verzeichnis \Data in das Verzeichnis \Second_Q\Reports verschieben möchten, geben Sie Folgendes ein:
```
move \data\*.xls \second_q\reports\ 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)