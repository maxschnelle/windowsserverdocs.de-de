---
title: Detail-volume
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38f2bc75-2ed6-4e80-aa74-ab83133db1cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7cae6dc9b82992b58c4f94801f90c0b7072492b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856921"
---
# <a name="detail-volume"></a>Detail-volume



Zeigt die Datenträger auf denen das aktuelle Volume befindet.

## <a name="syntax"></a>Syntax

```
detail volume
```

## <a name="remarks"></a>Hinweise

-   Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Volume** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.
-   Die volumedetails gelten nicht auf schreibgeschützten Volumes, z. B. eine DVD-ROM oder CD-ROM-Laufwerk.

## <a name="BKMK_examples"></a>Beispiele für

Um alle Datenträger angezeigt, in denen das aktuelle Volume befindet, geben Sie Folgendes ein:
```
detail volume
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

