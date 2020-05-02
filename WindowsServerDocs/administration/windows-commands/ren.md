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
ms.openlocfilehash: 21ce37795af3080245633938e96f891f7a485d53
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722421"
---
# <a name="ren"></a>ren

Benennt Dateien oder Verzeichnisse um. Dieser Befehl ist mit dem Befehl **Rename** identisch.



## <a name="syntax"></a>Syntax

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[\<Laufwerk>:] [\<Pfad>] \<FileName1>|Gibt den Speicherort und den Namen der Datei oder des Satzes von Dateien an, die Sie umbenennen möchten. *FileName1* kann Platzhalter Zeichen (**&#42;** und **?**) enthalten.|
|\<FileName2>|Gibt den neuen Namen für die Datei an. Mit Platzhalter Zeichen können Sie neue Namen für mehrere Dateien angeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

- Beim Umbenennen von Dateien können Sie kein neues Laufwerk oder einen neuen Pfad angeben.
- Sie können den Befehl " **ren** " nicht zum Umbenennen von Dateien auf mehreren Laufwerken oder zum Verschieben von Dateien in ein anderes Verzeichnis verwenden.
- Sie können Platzhalter Zeichen (**&#42;** und **?**) in beiden *filename* -Parametern verwenden. Zeichen, die durch Platzhalter Zeichen in *FileName2* dargestellt werden, sind mit den entsprechenden Zeichen in *FileName1*identisch.
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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)