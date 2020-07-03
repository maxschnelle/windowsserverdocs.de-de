---
title: expose
description: Referenz Artikel für den Befehl "verfügbar machen", der eine persistente Schatten Kopie als Laufwerk Buchstabe, Freigabe oder Einstellungspunkt verfügbar macht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 816aad0ba57a30d9d3a05709941b1915d9a97d03
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932405"
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
