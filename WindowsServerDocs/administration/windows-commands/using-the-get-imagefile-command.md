---
title: Mithilfe des Befehls Get-ImageFile
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6bbe5ece95d1f9821a27b96e56bc34576a0f5f33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827621"
---
# <a name="using-the-get-imagefile-command"></a>Mithilfe des Befehls Get-ImageFile



Ruft Informationen über die Bilder enthalten, die in einer Windows-Abbilddatei (WIM) ab.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ ImageFile:\<Pfad des WIM-Datei >|Gibt den vollständigen Pfad und Namen der WIM-Datei an.|
|[/Detailed]|Gibt alle Metadaten zu Bildern von jedes Image zurück. Wenn diese Option nicht verwendet wird, ist das Standardverhalten, um nur die Image-Name, Beschreibung und Dateinamen zurückzugeben.|

## <a name="BKMK_examples"></a>Beispiele für

Um Informationen zu einem Bild anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Get-ImageFile /ImageFile:"C:\temp\install.wim"
```
Um ausführliche Informationen anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:"\\Server\Share\My Folder \install.wim" /Detailed
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)