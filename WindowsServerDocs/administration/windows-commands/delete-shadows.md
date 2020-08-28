---
title: delete shadows
description: Referenz Artikel für den Befehl "Shadows löschen", mit dem Schatten Kopien gelöscht werden.
ms.topic: reference
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d2613fc978db8c8e5b323df142b204a7270f6bad
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89024204"
---
# <a name="delete-shadows"></a>delete shadows

Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---- | ---- |
| alle | Löscht alle Schatten Kopien. |
| Handels `<volume>` | Löscht alle Schatten Kopien des angegebenen Volumes. |
| ältesten `<volume>` | Löscht die älteste Schatten Kopie des angegebenen Volumes. |
| Set `<setID>` | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol verwenden, **%** Wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| Name `<shadowID>` | Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol verwenden, **%** Wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| verfügbar gemacht {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DELETE-Befehl](delete.md)
