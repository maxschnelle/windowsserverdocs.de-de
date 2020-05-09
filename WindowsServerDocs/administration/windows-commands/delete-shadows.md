---
title: Schatten löschen
description: Referenz Thema für den Befehl "Schatten löschen", mit dem Schatten Kopien gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b757314c96024741795c6770a98d10ac23b5bd0
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993113"
---
# <a name="delete-shadows"></a>Schatten löschen

Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <volume> | oldest <volume> | set <setID> | id <shadowID> | exposed {<drive> | <mountpoint>}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---- | ---- |
| all | Löscht alle Schatten Kopien. |
| Handels`<volume>` | Löscht alle Schatten Kopien des angegebenen Volumes. |
| ältesten`<volume>` | Löscht die älteste Schatten Kopie des angegebenen Volumes. |
| Set`<setID>` | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie **%** das Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| Name`<shadowID>` | Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie **%** das Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| verfügbar gemacht {'<drive> | <mountpoint>} |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DELETE-Befehl](delete.md)
