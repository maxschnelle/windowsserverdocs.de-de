---
title: Metadaten festlegen
description: Windows-Befehls Artikel für Set Metadata, der den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung festlegt, die zum Übertragen von Schatten Kopien von einem Computer auf einen anderen verwendet wird
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5bd728650cf163f98a82ff1e6f88755c4cc1aea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834523"
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
|[\<Laufwerk >:] [<Path>]|Gibt den Speicherort zum Erstellen der Metadatendatei an.|
|\<Metadata. cab >|Gibt den Namen der CAB-Datei zum Speichern von Metadaten für die Schatten Erstellung an.|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)