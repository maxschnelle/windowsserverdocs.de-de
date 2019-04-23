---
title: Maske
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 353e6080d1f6c548bc907b58655f31d0bce6de8b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858021"
---
# <a name="mask"></a>Maske



Hardwareschattenkopien, die mithilfe von importiert wurden entfernt die **importieren** Befehl.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mask <ShadowSetID>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|ShadowSetID|Entfernt Schattenkopien, die die angegebene ID zur Schatten kopieren festgelegt angehören|

## <a name="remarks"></a>Hinweise

-   Sie können einen vorhandenen Alias oder eine Umgebungsvariable anstelle von *ShadowSetID*. Verwendung **hinzufügen** ohne Parameter, um die vorhandenen Aliase finden Sie unter.

## <a name="BKMK_examples"></a>Beispiele für

Um die importierten Shadow Copy % Import_1 zu entfernen, geben Sie Folgendes ein:
```
mask %Import_1%
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)