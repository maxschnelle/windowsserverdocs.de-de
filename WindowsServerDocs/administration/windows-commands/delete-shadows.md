---
title: delete shadows
description: Referenz Artikel für den Befehl "Shadows löschen", mit dem Schatten Kopien gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d541b50a78d738034204d14441352fff6c5d9fc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929507"
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
| Handels`<volume>` | Löscht alle Schatten Kopien des angegebenen Volumes. |
| ältesten`<volume>` | Löscht die älteste Schatten Kopie des angegebenen Volumes. |
| Set`<setID>` | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol verwenden, **%** Wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| Name`<shadowID>` | Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol verwenden, **%** Wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| verfügbar gemacht {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DELETE-Befehl](delete.md)
