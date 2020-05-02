---
title: Detail Volume
description: Referenz Thema für das Detail Volume, in dem die Datenträger angezeigt werden, auf denen sich das aktuelle Volume befindet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38f2bc75-2ed6-4e80-aa74-ab83133db1cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2958c82b1dfc3b99d0e15690ef9857e7d83b244f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719619"
---
# <a name="detail-volume"></a>Detail Volume

Zeigt die Datenträger an, auf denen sich das aktuelle Volume befindet.

## <a name="syntax"></a>Syntax

```
detail volume
```

## <a name="remarks"></a>Bemerkungen

-   Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
-   Die Volumedetails gelten nicht für schreibgeschützte Volumes, wie z. b. ein DVD-ROM-oder CD-ROM-Laufwerk.

## <a name="examples"></a>Beispiele

Um alle Datenträger anzuzeigen, in denen sich das aktuelle Volume befindet, geben Sie Folgendes ein:
```
detail volume
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

