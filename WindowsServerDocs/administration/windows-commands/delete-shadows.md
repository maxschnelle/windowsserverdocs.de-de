---
title: Schatten löschen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c965af8b045c5ab3a110542d148b255f382a95c3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378629"
---
# <a name="delete-shadows"></a>Schatten löschen



Löscht Schatten Kopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                             Beschreibung                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        all        |                                                                      Löscht alle Schatten Kopien.                                                                      |
| Volume \<volume >  |                                                            Löscht alle Schatten Kopien des angegebenen Volumes.                                                            |
| ältestes \<volume >  |                                                         Löscht die älteste Schatten Kopie des angegebenen Volumes.                                                          |
|   Legen Sie \<setid fest >    | Löscht die Schatten Kopien im Schattenkopiesatz der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol **%** verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
|  ID \<shadowid >   |              Löscht eine Schatten Kopie der angegebenen ID. Sie können einen Alias angeben, indem Sie das Symbol **%** verwenden, wenn der Alias in der aktuellen Umgebung vorhanden ist.               |
| {\<drive > verfügbar gemacht |                                                                            <MountPoint>}                                                                             |

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)