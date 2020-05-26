---
title: Schatten auflisten
description: Referenz Thema für den Befehl list shadows, der permanente und vorhandene, nicht persistente Schatten Kopien auflistet, die sich auf dem System befinden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0261a25c7a70a0c8690d578cadc9e73ff9a62e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817170"
---
# <a name="list-shadows"></a>Schatten auflisten

Listet persistente und vorhandene nicht persistente Schatten Kopien auf dem System auf.

## <a name="syntax"></a>Syntax

```
list shadows {all | set <setID> | id <shadowID>}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ---------- |
| all | Listet alle Schatten Kopien auf. |
| Set`<setID>` | Listet Schatten Kopien auf, die zur angegebenen Schattenkopiesatz-ID gehören. |
| Name`<shadowID>` | Listet eine beliebige Schatten Kopie mit der angegebenen Schattenkopiekennung auf. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)