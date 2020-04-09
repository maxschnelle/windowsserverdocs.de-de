---
title: list
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57b6c8d0-872e-4dba-9715-1db8ab892e98
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d60c42b868a1e9a26e3168e4b489573f9f87e179
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841103"
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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Writer|Listet Writer auf. Syntax und Parameter finden Sie unter [Auflisten von Writern](list-writers.md) .|
|schattet|Listet persistente und vorhandene nicht persistente Schatten Kopien auf. Informationen zu Syntax und Parametern finden Sie unter [list shadows](list-shadows.md) .|
|Anbieter|Listet derzeit registrierte Schattenkopieanbieter auf. Informationen zu Syntax und Parametern finden Sie unter [List Providers](list-providers.md) .|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um alle Schatten Kopien aufzulisten, geben Sie Folgendes ein:
```
list shadows all
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)