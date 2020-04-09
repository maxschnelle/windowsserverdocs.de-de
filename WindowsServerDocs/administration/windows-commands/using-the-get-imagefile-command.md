---
title: Get-ImageFile
description: Windows-Befehls Artikel für Get-ImageFile, der Informationen zu den in einer Windows-Abbild Datei (WIM) enthaltenen Images abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef1cf2b9eec6739690d286c32d26dd84b07e348c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830993"
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
|/ImageFile:\<WIM-Dateipfad >|Gibt den vollständigen Pfad und den Dateinamen der WIM-Datei an.|
|/Detailed|Gibt alle Bild Metadaten aus jedem Bild zurück. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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