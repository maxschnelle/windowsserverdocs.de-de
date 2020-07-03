---
title: Get-ImageFile
description: Referenz Artikel zu Get-ImageFile, der Informationen zu den Bildern abruft, die in einer Windows-Abbild Datei (WIM-Datei) enthalten sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 127b5282b74020f002c7ccc55663fc2571584582
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932218"
---
# <a name="get-imagefile"></a>Get-ImageFile

Ruft Informationen zu den in einer Windows-Abbild Datei (WIM) enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ImageFile:\<WIM file path>|Gibt den vollständigen Pfad und den Dateinamen der WIM-Datei an.|
|/Detailed|Gibt alle Bild Metadaten aus jedem Bild zurück. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einem Bild anzuzeigen:
```
WDSUTIL /Get-ImageFile /ImageFile:C:\temp\install.wim
```
Geben Sie Folgendes ein, um ausführliche Informationen anzuzeigen:
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:\\Server\Share\My Folder \install.wim /Detailed
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)