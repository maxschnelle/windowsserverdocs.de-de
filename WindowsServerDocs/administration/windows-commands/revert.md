---
title: Umzukehren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3243f13a4997824d9fff7c874ce26d56325fefa4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371450"
---
# <a name="revert"></a>Umzukehren



setzt ein Volume auf eine angegebene Schatten Kopie zurück. Dies wird nur für Schatten Kopien im Client zugänglichen Kontext unterstützt. Diese Schatten Kopien sind persistent und können nur vom Systemanbieter erstellt werden. Bei Verwendung ohne Parameter zeigt **Revert** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
revert <ShadowCopyID>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<shadocopyid >|Gibt die Schattenkopiekennung an, auf der das Volume wieder hergestellt wird|

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)