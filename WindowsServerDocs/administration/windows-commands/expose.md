---
title: expose
description: Referenz Artikel für den Befehl "verfügbar machen", der eine persistente Schatten Kopie als Laufwerk Buchstabe, Freigabe oder Einstellungspunkt verfügbar macht.
ms.topic: reference
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3d36ec0a1c4f85282c1949700dad1f4568356748
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635905"
---
# <a name="expose"></a>expose

Macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.

## <a name="syntax"></a>Syntax

```
expose <shadowID> {<drive:> | <share> | <mountpoint>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
