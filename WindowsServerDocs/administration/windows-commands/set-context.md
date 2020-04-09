---
title: Kontext festlegen
description: Windows-Befehls Thema für den Set-Kontext, der den Kontext für die Erstellung von Schatten Kopien festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 162fefc46bc3b8ae39dcb41a387e50ed98fefa70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834563"
---
# <a name="set-contex"></a>Festlegen des Verbindungs Punkts

Legt den Kontext für die Erstellung von Schatten Kopien fest. Wenn Sie ohne Parameter verwendet wird, wird in der Eingabeaufforderung " **Kontext** anzeigen" angezeigt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|clientbarrierefreiheits|Gibt an, dass die Schatten Kopie von Client Versionen von Windows verwendet werden kann.|
|hartnäck|Gibt an, dass die Schatten Kopie über das Beenden, zurücksetzen oder Neustarten des Programms hinweg beibehalten wird.|
|volatile|Löscht die Schatten Kopie beim Beenden oder zurücksetzen.|
|nowriter|Gibt an, dass alle Writer ausgeschlossen werden.|

## <a name="remarks"></a>Hinweise

-   Der *Client barrierefreie* Kontext ist standardmäßig persistent.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um zu verhindern, dass Schatten Kopien beim Beenden von DiskShadow gelöscht werden:
```
set context persistent
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)