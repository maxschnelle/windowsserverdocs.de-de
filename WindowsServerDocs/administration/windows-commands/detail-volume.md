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
ms.openlocfilehash: eac3749304a06ea4cc11bf90a3220f5e24f9b5ae
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993013"
---
# <a name="detail-volume"></a>Detail Volume

Zeigt die Datenträger an, auf denen sich das aktuelle Volume befindet. Bevor Sie beginnen, müssen Sie ein Volume auswählen, damit dieser Vorgang erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl [Volume auswählen](select-volume.md) ein Volume aus, und verschieben Sie den Fokus auf das Volume. Die Volumedetails gelten nicht für schreibgeschützte Volumes, wie z. b. ein DVD-ROM-oder CD-ROM-Laufwerk.

## <a name="syntax"></a>Syntax

```
detail volume
```

## <a name="examples"></a>Beispiele

Um alle Datenträger anzuzeigen, in denen sich das aktuelle Volume befindet, geben Sie Folgendes ein:

```
detail volume
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [Detail Befehl](detail.md)