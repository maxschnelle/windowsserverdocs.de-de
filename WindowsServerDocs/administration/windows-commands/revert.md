---
title: umzukehren
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7dae609e4615868b03e4b5ea9a681f553aa0667
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835753"
---
# <a name="revert"></a>umzukehren



setzt ein Volume auf eine angegebene Schatten Kopie zurück. Dies wird nur für Schatten Kopien im Client zugänglichen Kontext unterstützt. Diese Schatten Kopien sind persistent und können nur vom Systemanbieter erstellt werden. Bei Verwendung ohne Parameter zeigt **Revert** die Hilfe an der Eingabeaufforderung an.

## <a name="syntax"></a>Syntax

```
revert <ShadowCopyID>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<shadowcopyid >|Gibt die Schattenkopiekennung an, auf der das Volume wieder hergestellt wird|

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)