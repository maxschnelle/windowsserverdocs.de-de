---
title: ren
description: Erfahren Sie, wie Sie eine Datei oder ein Verzeichnis mit dem Befehl "ren" umbenennen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 235497b09f44f9077b7f622f7f2b68a0bc49af86
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836043"
---
# <a name="ren"></a>ren

Benennt Dateien oder Verzeichnisse um. Dieser Befehl ist mit dem Befehl **Rename** identisch.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [\<Pfad >]\<FileName1 >|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die Sie umbenennen möchten. *FileName1* kann Platzhalter Zeichen ( **&#42;** und **?** ) enthalten.|
|\<FileName2 >|Gibt den neuen Namen für die Datei an. Mit Platzhalter Zeichen können Sie neue Namen für mehrere Dateien angeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Beim Umbenennen von Dateien können Sie kein neues Laufwerk oder einen neuen Pfad angeben.
- Sie können den Befehl " **ren** " nicht zum Umbenennen von Dateien auf mehreren Laufwerken oder zum Verschieben von Dateien in ein anderes Verzeichnis verwenden.
- Sie können Platzhalter Zeichen ( **&#42;** und **?** ) in beiden *filename* -Parametern verwenden. Zeichen, die durch Platzhalter Zeichen in *FileName2* dargestellt werden, sind mit den entsprechenden Zeichen in *FileName1*identisch.
- *FileName2* muss ein eindeutiger Dateiname sein. Wenn *FileName2* mit einem vorhandenen Dateinamen übereinstimmt, zeigt **ren** die folgende Meldung an:  
  ```
  Duplicate file name or file not found
  ```

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um alle Dateinamen Erweiterungen von. txt im aktuellen Verzeichnis in doc-Erweiterungen zu ändern:
```
ren *.txt *.doc 
```
Um den Namen eines Verzeichnisses von Chap10 zu part10 zu ändern, geben Sie Folgendes ein:
```
ren chap10 part10 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)