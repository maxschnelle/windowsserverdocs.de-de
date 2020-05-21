---
title: sichtbar
description: Referenz Thema für den Befehl "verfügbar machen", der eine persistente Schatten Kopie als Laufwerksbuchstaben, Freigabe-oder Einfügepunkt verfügbar macht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4e8ebf71f6ddcb457460f8174793586e81c73a6
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437175"
---
# <a name="expose"></a>sichtbar

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)
