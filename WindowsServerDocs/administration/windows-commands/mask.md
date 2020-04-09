---
title: Maske
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1cb92caacb955449c1baaad411fdbe4cdf05b73
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839643"
---
# <a name="mask"></a>Maske



entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mask <ShadowSetID>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Shadow-TID|Entfernt Schatten Kopien, die zur angegebenen Schattenkopiesatz-ID gehören.|

## <a name="remarks"></a>Hinweise

-   Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um die importierte Schatten Kopie% Import_1% zu entfernen, geben Sie Folgendes ein:
```
mask %Import_1%
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)