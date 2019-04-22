---
title: list
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aacc93e1c7a16a7327ddbd17515f19cf41a5b458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825541"
---
# <a name="list"></a>list



Listen-Writer, Schattenkopien und gegenwärtig registrierten Volumeschattenkopie-Anbieter, die auf dem System sind. Wenn Sie ohne Angabe von Parametern **Liste** zeigt die Hilfe an der Eingabeaufforderung.

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
|Schreiber|Listen-Writer. Finden Sie unter [List Writers](list-writers.md) für die Syntax und Parameter.|
|Zeichnen von Schatten|Listet dauerhaft ist und vorhandene nicht persistenter Schattenkopien. Finden Sie unter [Liste Shadows](list-shadows.md) für die Syntax und Parameter.|
|Anbieter|Listet die registrierten derzeit Volumeschattenkopie-Anbieter. Finden Sie unter [Liste von Anbietern](list-providers.md) für die Syntax und Parameter.|

## <a name="BKMK_examples"></a>Beispiele für

Um alle Schattenkopien aufzulisten, geben Sie Folgendes ein:
```
list shadows all
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)