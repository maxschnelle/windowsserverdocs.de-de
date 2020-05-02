---
title: Metadaten festlegen
description: Referenz Thema für Set Metadata, das den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung festlegt, die zum Übertragen von Schatten Kopien von einem Computer auf einen anderen verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 683e54a7efc072d8709d6257771ba6bc5bde206e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721912"
---
# <a name="set-metadata"></a>Metadaten festlegen

Legt den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung fest, mit der Schatten Kopien von einem Computer auf einen anderen übertragen werden Bei Verwendung ohne Parameter zeigt **Set Metadata** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[\<Laufwerk>:] [<Path>]|Gibt den Speicherort zum Erstellen der Metadatendatei an.|
|\<> "Metadata. cab"|Gibt den Namen der CAB-Datei zum Speichern von Metadaten für die Schatten Erstellung an.|

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)