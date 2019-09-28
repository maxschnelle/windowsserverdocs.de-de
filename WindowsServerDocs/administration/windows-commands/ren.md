---
title: ren
description: Erfahren Sie, wie Sie eine Datei oder ein Verzeichnis mit dem Befehl "ren" umbenennen.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2ba3f6a13dc03c0b6a5561be9f0f692546a25149
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384578"
---
# <a name="ren"></a>ren

Benennt Dateien oder Verzeichnisse um. Dieser Befehl ist mit dem Befehl **Rename** identisch.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<laufwerk >:] [\< Pfad >] \<dateiname1 >|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die Sie umbenennen möchten. *FileName1* kann Platzhalter Zeichen ( **&#42;** und **?** ) enthalten.|
|\<dateiname2 >|Gibt den neuen Namen für die Datei an. Mit Platzhalter Zeichen können Sie neue Namen für mehrere Dateien angeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Beim Umbenennen von Dateien können Sie kein neues Laufwerk oder einen neuen Pfad angeben.
- Sie können den Befehl " **ren** " nicht zum Umbenennen von Dateien auf mehreren Laufwerken oder zum Verschieben von Dateien in ein anderes Verzeichnis verwenden.
- Sie können Platzhalter Zeichen ( **&#42;** und **?** ) in beiden *filename* -Parametern verwenden. Zeichen, die durch Platzhalter Zeichen in *FileName2* dargestellt werden, sind mit den entsprechenden Zeichen in *FileName1*identisch.
- *FileName2* muss ein eindeutiger Dateiname sein. Wenn *FileName2* mit einem vorhandenen Dateinamen übereinstimmt, zeigt **ren** die folgende Meldung an:  
  ```
  Duplicate file name or file not found
  ```

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Dateinamen Erweiterungen von. txt im aktuellen Verzeichnis in doc-Erweiterungen zu ändern:
```
ren *.txt *.doc 
```
Um den Namen eines Verzeichnisses von Chap10 zu part10 zu ändern, geben Sie Folgendes ein:
```
ren chap10 part10 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)