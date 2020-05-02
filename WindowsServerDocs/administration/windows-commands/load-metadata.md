---
title: Metadaten laden
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d3132bca86533ec3f2d0a27247bd3c116cf55b6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724465"
---
# <a name="load-metadata"></a>Metadaten laden



Lädt eine Datei "Metadata. cab" vor dem Importieren einer austauschen-Schatten Kopie oder lädt die Writer-Metadaten im Fall einer Wiederherstellung. Bei Verwendung ohne Parameter zeigt die Eingabe **Metadaten** die Hilfe an der Eingabeaufforderung an.



## <a name="syntax"></a>Syntax

```
load metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[\<Laufwerk>:] [<Path>]|Gibt den Speicherort der Metadatendatei an.|
|Metadaten. cab|Gibt die zu ladende Datei "Metadata. cab" an.|

## <a name="remarks"></a>Bemerkungen

-   Sie können den **Import** -Befehl verwenden, um eine austauschen-Schatten Kopie auf Grundlage der Metadaten zu importieren, die durch **Laden von Metadaten**angegeben werden.
-   Dieser Befehl wird vor dem Befehl zum **Wiederherstellen von BEGIN** benötigt, um die ausgewählten Writer und Komponenten für die Wiederherstellung zu laden.

## <a name="examples"></a>Beispiele

Zum Laden einer Metadatendatei namens "Metafile. cab" aus dem Standard Speicherort geben Sie Folgendes ein:
```
load metadata metafile.cab
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)