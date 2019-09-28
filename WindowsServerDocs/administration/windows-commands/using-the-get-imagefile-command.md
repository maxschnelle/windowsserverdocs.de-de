---
title: Verwenden des Befehls Get-ImageFile
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c8136585e04caca02ab16c7b4ca11a825cf400d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392133"
---
# <a name="using-the-get-imagefile-command"></a>Verwenden des Befehls Get-ImageFile



Ruft Informationen zu den in einer Windows-Abbild Datei (WIM) enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ImageFile: @no__t 0wim-Dateipfad >|Gibt den vollständigen Pfad und den Dateinamen der WIM-Datei an.|
|/Detailed|Gibt alle Bild Metadaten aus jedem Bild zurück. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einem Bild anzuzeigen:
```
WDSUTIL /Get-ImageFile /ImageFile:"C:\temp\install.wim"
```
Geben Sie Folgendes ein, um ausführliche Informationen anzuzeigen:
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:"\\Server\Share\My Folder \install.wim" /Detailed
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)