---
title: ren
description: Erfahren Sie, wie Sie eine Datei oder ein Verzeichnis mit dem Befehl Ren umbenennen.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 34c761cb08916d277f8f7f1c58d57a05ed2c8daf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441810"
---
# <a name="ren"></a>ren

Umbenennen von Dateien oder Verzeichnisse. Dieser Befehl ist identisch mit der **umbenennen** Befehl.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [\<Pfad >]\<Dateiname1 >|Gibt den Speicherort und Namen der Datei oder den Satz von Dateien, die Sie umbenennen möchten. *Dateiname1* kann Platzhalterzeichen enthalten ( **&#42;** und **?** ).|
|\<FileName2>|Gibt den neuen Namen für die Datei an. Sie können Platzhalterzeichen verwenden, um neue Namen für mehrere Dateien anzugeben.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Sie können kein neues Laufwerk oder einen Pfad angeben, beim Umbenennen von Dateien.
- Sie können keine der **Ren** -Befehl zum Umbenennen von Dateien auf Laufwerken oder zum Verschieben von Dateien in ein anderes Verzeichnis.
- Sie können Platzhalterzeichen verwenden ( **&#42;** und **?** ) in einem *FileName* Parameter. Zeichen, die mit Platzhalterzeichen in dargestellt werden *Dateiname2* identisch mit den entsprechenden Zeichen in *Dateiname1*.
- *Dateiname2* muss ein eindeutigen Dateinamen. Wenn *Dateiname2* entspricht den Dateinamen einer vorhandenen **Ren** wird die folgende Meldung angezeigt:  
  ```
  Duplicate file name or file not found
  ```

## <a name="BKMK_examples"></a>Beispiele für

Um alle TXT-Datei Namespaceerweiterungen im aktuellen Verzeichnis in doc-Erweiterungen zu ändern, geben Sie Folgendes ein:
```
ren *.txt *.doc 
```
Um den Namen eines Verzeichnisses aus Chap10 in Teil10 ändern möchten, geben Sie Folgendes ein:
```
ren chap10 part10 
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)