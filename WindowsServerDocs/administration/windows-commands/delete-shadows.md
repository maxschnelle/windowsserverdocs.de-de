---
title: delete shadows
description: Referenz Artikel für den Befehl "Shadows löschen", mit dem Schatten Kopien gelöscht werden.
ms.topic: reference
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f8fe95ac21c36f4605a544c97036c0a02bddaf42
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628847"
---
# <a name="delete-shadows"></a>delete shadows

Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
