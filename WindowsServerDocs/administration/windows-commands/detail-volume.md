---
title: Detail Volume
description: Windows-Befehls Thema für das Detail Volume, in dem die Datenträger angezeigt werden, auf denen sich das aktuelle Volume befindet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38f2bc75-2ed6-4e80-aa74-ab83133db1cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f0441beba769066c593e77b55b9266918e5f778
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846320"
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

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um alle Datenträger anzuzeigen, in denen sich das aktuelle Volume befindet, geben Sie Folgendes ein:
```
detail volume
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

