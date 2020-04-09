---
title: cd
description: Windows-Befehls Thema für CD, in dem der Name des aktuellen Verzeichnisses angezeigt oder geändert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d62f529ab6c45957f0fdea24358a2f13151adb6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848223"
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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/d|Ändert das aktuelle Laufwerk und das aktuelle Verzeichnis für ein Laufwerk.|
|\<Laufwerk >:|Gibt das anzuzeigende oder zu ändernde Laufwerk an (wenn sich das aktuelle Laufwerk unterscheidet).|
|\<Pfad >|Gibt den Pfad zu dem Verzeichnis an, das Sie anzeigen oder ändern möchten.|
|[..]|Gibt an, dass Sie in den übergeordneten Ordner wechseln möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Wenn Befehls Erweiterungen aktiviert sind, gelten die folgenden Bedingungen für den Befehl **CD** :
- Die aktuelle Verzeichnis Zeichenfolge wird so konvertiert, dass Sie dieselbe Groß-/Kleinschreibung wie die Namen auf dem Datenträger Beispielsweise wird `cd C:\TEMP` das aktuelle Verzeichnis auf "c:\temp" festlegen, wenn dies auf dem Datenträger der Fall ist.
- Leerzeichen werden nicht als Trennzeichen behandelt, daher kann der *Pfad* Leerzeichen enthalten, ohne Anführungszeichen einzuschließen. Beispiel:  
  ```
  cd username\programs\start menu
  ```  
  entspricht:  
  ```
  cd username\programs\start menu
  ```  
  Die Anführungszeichen sind jedoch erforderlich, wenn Erweiterungen deaktiviert sind.

Um Befehls Erweiterungen zu deaktivieren, geben Sie Folgendes ein:
```
cmd /e:off
```

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)