---
title: Überprüfen
description: Windows-Befehls Thema zur Überprüfung, das **cmd** mitteilt, ob die Dateien ordnungsgemäß auf einen Datenträger geschrieben werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a0777999a604a23e2de83eda6b89c926cb241c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830053"
---
# <a name="verify"></a>Überprüfen



Weist **cmd** an, zu überprüfen, ob Ihre Dateien ordnungsgemäß auf einen Datenträger geschrieben wurden. Bei Verwendung ohne **Parameter zeigt die** aktuelle Einstellung an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
verify [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[on \| off]|Schaltet die **Überprüfung** ein oder aus.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die aktuelle **Verify** -Einstellung anzuzeigen:
```
verify
```
Geben Sie Folgendes ein, um die Einstellung **überprüfen** für zu aktivieren:
```
Verify on
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)