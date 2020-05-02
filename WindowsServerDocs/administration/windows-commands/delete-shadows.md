---
title: Schatten löschen
description: Referenz Thema für Lösch Schatten, mit dem Schatten Kopien gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dd367d76ad1699321af9caf47a0ddc351088a05
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720796"
---
# <a name="delete-shadows"></a>Schatten löschen

Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---- | ---- |
| all | Löscht alle Schatten Kopien. |
| volumevolume \<> | Löscht alle Schatten Kopien des angegebenen Volumes. |
| ältestes \<Volume> | Löscht die älteste Schatten Kopie des angegebenen Volumes. |
| setID festlegen \<> | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie **%** das Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| ID \<shadowid> | Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie **%** das Symbol verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
| verfügbar gemachte\<{Drive> | <MountPoint>} |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)