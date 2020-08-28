---
title: expose
description: Referenz Artikel für den Befehl "verfügbar machen", der eine persistente Schatten Kopie als Laufwerk Buchstabe, Freigabe oder Einstellungspunkt verfügbar macht.
ms.topic: reference
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67e6b230b780e6ae84ea1ff30804c5722ca2337d
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036688"
---
# <a name="expose"></a>expose

Macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.

## <a name="syntax"></a>Syntax

```
expose <shadowID> {<drive:> | <share> | <mountpoint>}
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| shadowid | Gibt die Schatten-ID der Schatten Kopie an, die Sie verfügbar machen möchten. Sie können auch einen vorhandenen Alias oder eine Umgebungsvariable anstelle von *shadowid*verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen. |
| `<drive:>` | Macht die angegebene Schatten Kopie als Laufwerk Buchstaben verfügbar (z. b `p:` .). |
| `<share>` | Macht die angegebene Schatten Kopie in einer Freigabe verfügbar (z `\\machinename` . b.).   |
| `<mountpoint>` | Macht die angegebene Schatten Kopie für einen Einstellungspunkt verfügbar (z `C:\shadowcopy` . b.). |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die dem VSS_SHADOW_1-Umgebungsvariable zugeordnete persistente Schatten Kopie als Laufwerk X verfügbar zu machen:

```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)
