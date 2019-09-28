---
title: Detail Volume
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f8cd5889bfd2aea835cb64ef1a4076faee0f39b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378466"
---
# <a name="detail-volume"></a>Detail Volume



Zeigt die Datenträger an, auf denen sich das aktuelle Volume befindet.

## <a name="syntax"></a>Syntax

```
detail volume
```

## <a name="remarks"></a>Hinweise

-   Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
-   Die Volumedetails gelten nicht für schreibgeschützte Volumes, wie z. b. ein DVD-ROM-oder CD-ROM-Laufwerk.

## <a name="BKMK_examples"></a>Beispiele

Um alle Datenträger anzuzeigen, in denen sich das aktuelle Volume befindet, geben Sie Folgendes ein:
```
detail volume
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

