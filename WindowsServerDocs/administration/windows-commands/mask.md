---
title: Chel
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2f0dc83d7d9f7204f56e95c62b7cfad991f539ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373709"
---
# <a name="mask"></a>Chel



entfernt Hardware Schatten Kopien, die mithilfe des **Import** -Befehls importiert wurden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
mask <ShadowSetID>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Shadow-TID|Entfernt Schatten Kopien, die zur angegebenen Schattenkopiesatz-ID gehören.|

## <a name="remarks"></a>Hinweise

-   Anstelle von *Shadow* TID*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="BKMK_examples"></a>Beispiele

Um die importierte Schatten Kopie% Import_1% zu entfernen, geben Sie Folgendes ein:
```
mask %Import_1%
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)