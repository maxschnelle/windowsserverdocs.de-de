---
title: Kontext festlegen
description: Referenz Artikel für den festgelegten Kontext, der den Kontext für die Erstellung von Schatten Kopien festlegt.
ms.topic: reference
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7c89c0da8b63cef5b534163c5dbc1a0bee0cddbf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637750"
---
# <a name="set-contex"></a>Festlegen des Verbindungs Punkts

Legt den Kontext für die Erstellung von Schatten Kopien fest. Wenn Sie ohne Parameter verwendet wird, wird in der Eingabeaufforderung " **Kontext** anzeigen" angezeigt.



## <a name="syntax"></a>Syntax

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|clientbarrierefreiheits|Gibt an, dass die Schatten Kopie von Client Versionen von Windows verwendet werden kann.|
|hartnäck|Gibt an, dass die Schatten Kopie über das Beenden, zurücksetzen oder Neustarten des Programms hinweg beibehalten wird.|
|volatile|Löscht die Schatten Kopie beim Beenden oder zurücksetzen.|
|nowriter|Gibt an, dass alle Writer ausgeschlossen werden.|

## <a name="remarks"></a>Hinweise

-   Der *Client barrierefreie* Kontext ist standardmäßig persistent.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu verhindern, dass Schatten Kopien beim Beenden von DiskShadow gelöscht werden:
```
set context persistent
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)