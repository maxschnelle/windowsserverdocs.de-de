---
title: Löschen Sie Schatten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1a0945477bc4fce907b5ec4a697c7a2ec2f59557
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436110"
---
# <a name="delete-shadows"></a>Löschen Sie Schatten



Löscht die Schattenkopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>Parameter

|     Parameter     |                                                                             Beschreibung                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        all        |                                                                      Löscht alle Schattenkopien.                                                                      |
| Volume \<Volume >  |                                                            Löscht alle Schattenkopien auf dem angegebenen Volume.                                                            |
| älteste \<Volume >  |                                                         Löscht die älteste Schattenkopie des angegebenen Volumes an.                                                          |
|   Legen Sie \<SetID >    | Löscht die Schattenkopien in die Schatten-kopieren-Satz von der angegebenen ID Sie können einen Alias angeben, indem die **%** symbol, wenn der Alias in der aktuellen Umgebung vorhanden ist. |
|  ID \<ShadowID >   |              Löscht eine Schattenkopie von der angegebenen ID Sie können einen Alias angeben, indem die **%** symbol, wenn der Alias in der aktuellen Umgebung vorhanden ist.               |
| verfügbar gemachten {\<Drive > |                                                                            <MountPoint>}                                                                             |

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)