---
title: list
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b6c8d0-872e-4dba-9715-1db8ab892e98
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91b42925fc822b10157bb488167d06fe82cfe1e3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374697"
---
# <a name="list"></a>list



Listet Writer, Schatten Kopien oder derzeit registrierte Schattenkopieanbieter auf, die sich auf dem System befinden. Bei Verwendung ohne Parameter zeigt **List** die Hilfe an der Eingabeaufforderung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
list writers [metadata | detailed | status]
list shadows {all | set <SetID> | id <ShadowID>}
list providers
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Writer|Listet Writer auf. Syntax und Parameter finden Sie unter [Auflisten von Writern](list-writers.md) .|
|Schattet|Listet persistente und vorhandene nicht persistente Schatten Kopien auf. Informationen zu Syntax und Parametern finden Sie unter [list shadows](list-shadows.md) .|
|Anbieter|Listet derzeit registrierte Schattenkopieanbieter auf. Informationen zu Syntax und Parametern finden Sie unter [List Providers](list-providers.md) .|

## <a name="BKMK_examples"></a>Beispiele

Um alle Schatten Kopien aufzulisten, geben Sie Folgendes ein:
```
list shadows all
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)