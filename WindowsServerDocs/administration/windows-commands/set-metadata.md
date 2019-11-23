---
title: Metadaten festlegen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac73a4131d3f4065cd1aeae873734b079ad664e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370950"
---
# <a name="set-metadata"></a>Metadaten festlegen



Legt den Namen und den Speicherort der Metadatendatei für die Schatten Erstellung fest, mit der Schatten Kopien von einem Computer auf einen anderen übertragen werden Bei Verwendung ohne Parameter zeigt **Set Metadata** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[\<Laufwerk >:] [<Path>]|Gibt den Speicherort zum Erstellen der Metadatendatei an.|
|\<Metadata. cab >|Gibt den Namen der CAB-Datei zum Speichern von Metadaten für die Schatten Erstellung an.|

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)