---
title: cd
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed0942232eb205a8198d4b3d366ca9482af1f4b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379707"
---
# <a name="cd"></a>cd



Zeigt den Namen des aktuellen Verzeichnisses an oder ändert dieses. Wenn Sie nur mit einem Laufwerk Buchstaben (z. b. `cd C:`) verwendet wird, zeigt **CD** die Namen des aktuellen Verzeichnisses auf dem angegebenen Laufwerk an. Bei Verwendung ohne Parameter zeigt **CD** das aktuelle Laufwerk und Verzeichnis an.

> [!NOTE]
> Dieser Befehl ist mit dem **"chdir"** -Befehl identisch.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
cd [/d] [<Drive>:][<Path>]
cd [..]
chdir [/d] [<Drive>:][<Path>]
chdir [..]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Ändert das aktuelle Laufwerk und das aktuelle Verzeichnis für ein Laufwerk.|
|> \<drive:|Gibt das anzuzeigende oder zu ändernde Laufwerk an (wenn sich das aktuelle Laufwerk unterscheidet).|
|\<path >|Gibt den Pfad zu dem Verzeichnis an, das Sie anzeigen oder ändern möchten.|
|[..]|Gibt an, dass Sie in den übergeordneten Ordner wechseln möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Wenn Befehls Erweiterungen aktiviert sind, gelten die folgenden Bedingungen für den Befehl **CD** :
- Die aktuelle Verzeichnis Zeichenfolge wird so konvertiert, dass Sie dieselbe Groß-/Kleinschreibung wie die Namen auf dem Datenträger Beispielsweise würde `cd C:\TEMP` das aktuelle Verzeichnis auf "c:\temp" festlegen, wenn dies auf dem Datenträger der Fall ist.
- Leerzeichen werden nicht als Trennzeichen behandelt, daher kann der *Pfad* Leerzeichen enthalten, ohne Anführungszeichen einzuschließen. Zum Beispiel:  
  ```
  cd username\programs\start menu
  ```  
  entspricht:  
  ```
  cd "username\programs\start menu"
  ```  
  Die Anführungszeichen sind jedoch erforderlich, wenn Erweiterungen deaktiviert sind.

Um Befehls Erweiterungen zu deaktivieren, geben Sie Folgendes ein:
```
cmd /e:off
```

## <a name="BKMK_examples"></a>Beispiele

Das Stammverzeichnis ist der oberste Teil der Verzeichnishierarchie eines Laufwerks. Geben Sie Folgendes ein, um zum Stammverzeichnis zurückzukehren:
```
cd\
```
Geben Sie Folgendes ein, um das Standardverzeichnis auf einem anderen Laufwerk zu ändern:
```
cd [<Drive>:\[<Directory>]]
```
Um die Änderung am Verzeichnis zu überprüfen, geben Sie Folgendes ein:
```
cd [<Drive>:]
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)