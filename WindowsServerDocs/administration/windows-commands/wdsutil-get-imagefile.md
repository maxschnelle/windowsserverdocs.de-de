---
title: Get-ImageFile
description: Referenz Artikel zu Get-ImageFile, der Informationen zu den Bildern abruft, die in einer Windows-Abbild Datei (WIM-Datei) enthalten sind.
ms.topic: reference
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 41183f92d75736afc32dfbbee9d31871b3ef24f9
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524335"
---
# <a name="get-imagefile"></a>Get-ImageFile

Ruft Informationen zu den in einer Windows-Abbild Datei (WIM) enthaltenen Bildern ab.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/ImageFile:\<WIM file path>|Gibt den vollständigen Pfad und den Dateinamen der WIM-Datei an.|
|/Detailed|Gibt alle Bild Metadaten aus jedem Bild zurück. Wenn diese Option nicht verwendet wird, besteht das Standardverhalten darin, nur den Bildnamen, die Beschreibung und den Dateinamen zurückzugeben.|

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu einem Bild anzuzeigen:
```
wdsutil /Get-ImageFile /ImageFile:C:\temp\install.wim
```
Geben Sie Folgendes ein, um ausführliche Informationen anzuzeigen:
```
wdsutil /Verbose /Get-ImageFile /ImageFile:\\Server\Share\My Folder \install.wim /Detailed
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)