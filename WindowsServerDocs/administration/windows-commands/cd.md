---
title: cd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5f907b6162e6767820e23222e287b933397397d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861101"
---
# <a name="cd"></a>cd



Zeigt den Namen des ab oder ändert das aktuelle Verzeichnis. Wenn nur ein Laufwerkbuchstabe verwendet (z. B. `cd C:`), **cd** zeigt die Namen des aktuellen Verzeichnisses in das angegebene Laufwerk. Wenn Sie ohne Angabe von Parametern **cd** zeigt das aktuelle Laufwerk und Verzeichnis.

> [!NOTE]
> Dieser Befehl ist identisch mit der **"chdir"** Befehl.

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
|/d|Ändert das aktuelle Laufwerk als auch für das aktuelle Verzeichnis für ein Laufwerk an.|
|\<Laufwerk >:|Gibt das Laufwerk zum Anzeigen oder ändern (falls abweichend vom aktuellen Laufwerk).|
|\<Pfad >|Gibt den Pfad zum Verzeichnis, das Sie anzeigen oder ändern möchten.|
|[..]|Gibt an, dass Sie in den übergeordneten Ordner ändern möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Wenn befehlserweiterungen aktiviert sind, gelten die folgenden Bedingungen für die **cd** Befehl:
-   Zeichenfolge des aktuellen Verzeichnisses wird konvertiert, um die gleiche Groß-/Kleinschreibung als die Namen auf dem Datenträger zu verwenden. Z. B. `cd C:\TEMP` das aktuelle Verzeichnis wird auf C:\Temp festgelegt werden, wenn dies der Fall, auf dem Datenträger ist.
-   Leerzeichen als Trennzeichen und daher nicht behandelt *Pfad* darf Leerzeichen enthalten, ohne die Anführungszeichen einschließen. Zum Beispiel:  
    ```
    cd username\programs\start menu
    ```  
    ist identisch:  
    ```
    cd "username\programs\start menu"
    ```  
    Die Anführungszeichen sind erforderlich, aber wenn Erweiterungen deaktiviert sind.

Um befehlserweiterungen deaktivieren möchten, geben Sie Folgendes ein:
```
cmd /e:off
```

## <a name="BKMK_examples"></a>Beispiele für

Das Stammverzeichnis ist am Anfang der Directory-Hierarchie für ein Laufwerk. Um zum Stammverzeichnis zurückzukehren, geben Sie Folgendes ein:
```
cd\
```
Um das Standardverzeichnis auf einem Laufwerk zu ändern, die sich von dem unterscheidet, die Sie auf, geben Sie Folgendes ein:
```
cd [<Drive>:\[<Directory>]]
```
Um die Änderung in das Verzeichnis zu überprüfen, geben Sie Folgendes ein:
```
cd [<Drive>:]
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)