---
title: list shadows
description: Referenz Artikel für den Befehl list shadows, der permanente und vorhandene, nicht persistente Schatten Kopien auflistet, die sich auf dem System befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fcf1946f5b2424eb7aa13af51bd6ff13c43349c1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931790"
---
# <a name="list-shadows"></a>list shadows

Listet persistente und vorhandene nicht persistente Schatten Kopien auf dem System auf.

## <a name="syntax"></a>Syntax

```
list shadows {all | set <setID> | id <shadowID>}
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ---------- |
| alle | Listet alle Schatten Kopien auf. |
| Set`<setID>` | Listet Schatten Kopien auf, die zur angegebenen Schattenkopiesatz-ID gehören. |
| Name`<shadowID>` | Listet eine beliebige Schatten Kopie mit der angegebenen Schattenkopiekennung auf. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)