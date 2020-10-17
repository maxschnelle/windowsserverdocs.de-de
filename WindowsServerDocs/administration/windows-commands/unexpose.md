---
title: unexpose
description: Referenz Artikel für den Befehl "nicht verfügbar machen", der eine verfügbar gemachte Schatten Kopie nicht verfügbar macht.
ms.topic: reference
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 35e545d632790f8c4d7d69d6e9fea1e7e1a07dc4
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156316"
---
# <a name="unexpose"></a>unexpose

Macht eine Schatten Kopie verfügbar, die mit dem verfügbar gemachten [Befehl](expose.md)verfügbar gemacht wurde. Die verfügbar gemachte Schatten Kopie kann durch die Schatten-ID, den Laufwerk Buchstaben, die Freigabe oder den Einfügepunkt angegeben werden.

## <a name="syntax"></a>Syntax

```
unexpose {<shadowID> | <drive:> | <share> | <mountpoint>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<shadowID>` | Zeigt die von der angegebenen Schatten-ID angegebene Schatten Kopie an. Anstelle von können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden `<shadowID>` . Verwenden [Sie den Befehl hinzufügen](add.md) ohne Parameter, um alle vorhandenen Aliase anzuzeigen. |
| `<drive:>` | Zeigt die dem angegebenen Laufwerk Buchstaben zugeordnete Schatten Kopie an (z. b. Laufwerk P). |
| `<share>` | Zeigt die der angegebenen Freigabe zugeordnete Schatten Kopie an (z `\\MachineName` . b.). |
| `<mountpoint>` | Zeigt die dem angegebenen Einstellungspunkt zugeordnete Schatten Kopie an (z `C:\shadowcopy\` . b.). |
| add | Wenn Sie ohne Parameter verwendet wird, werden die vorhandenen Aliase angezeigt. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die verfügbar machung der mit * Laufwerk P: verknüpften Schatten Kopie anzuzeigen \* :

```
unexpose P:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl hinzufügen](add.md)

- [Befehl verfügbar machen](expose.md)
