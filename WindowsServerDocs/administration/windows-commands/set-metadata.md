---
title: Metadaten festlegen
description: Referenz Artikel für Set Metadata, der den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung festlegt, die zum Übertragen von Schatten Kopien von einem Computer auf einen anderen verwendet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50c9ceebf072db2e7cefada1601accc97b5d0f7f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937092"
---
# <a name="set-metadata"></a>Metadaten festlegen

Legt den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung fest, mit der Schatten Kopien von einem Computer auf einen anderen übertragen werden Bei Verwendung ohne Parameter zeigt **Set Metadata** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Drive>:][<Path>]|Gibt den Speicherort zum Erstellen der Metadatendatei an.|
|\<MetaData.cab>|Gibt den Namen der CAB-Datei zum Speichern von Metadaten für die Schatten Erstellung an.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)