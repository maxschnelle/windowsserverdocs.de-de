---
title: Kontext festlegen
description: Referenz Artikel für den Kontext Befehl festlegen, mit dem der Kontext für die Erstellung von Schatten Kopien festgelegt wird.
ms.topic: reference
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ce1414ab90f116f58618fcd67bc203f25dc58e46
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91389094"
---
# <a name="set-context"></a>Kontext festlegen

Legt den Kontext für die Erstellung von Schatten Kopien fest. Wenn Sie ohne Parameter verwendet wird, wird in der Eingabeaufforderung " **Kontext** anzeigen" angezeigt.

## <a name="syntax"></a>Syntax

```
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| clientbarrierefreiheits | Gibt an, dass die Schatten Kopie von Client Versionen von Windows verwendet werden kann. Dieser Kontext ist standardmäßig persistent. |
| hartnäck | Gibt an, dass die Schatten Kopie über das Beenden, zurücksetzen oder Neustarten des Programms hinweg beibehalten wird. |
| volatile | Löscht die Schatten Kopie beim Beenden oder zurücksetzen. |
| nowriter | Gibt an, dass alle Writer ausgeschlossen werden. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu verhindern, dass Schatten Kopien beim Beenden von DiskShadow gelöscht werden:

```
set context persistent
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Metadaten festlegen"](set-metadata.md)

- [Befehl "Set Option"](set-option.md)

- [Befehl "ausführliche festlegen"](set-verbose.md)
