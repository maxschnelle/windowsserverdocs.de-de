---
title: volumestripe erstellen
description: Referenz Thema zum Create Volume Stripe-Befehl, der ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern erstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 315d7a08dfcf64ae09501975b5f5bdb72c37754e
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993206"
---
# <a name="create-volume-stripe"></a>volumestripe erstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein Stripesetvolume mit zwei oder mehr angegebenen dynamischen Datenträgern. Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.

## <a name="syntax"></a>Syntax

```
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |  -----------|
| Größe =`<n>` | Die Menge des Speicherplatzes in Megabyte (MB), die das Volume auf den einzelnen Datenträgern einnimmt. Wenn keine Größe angegeben ist, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem kleinsten Datenträger und den gleichen Speicherplatz auf jedem nachfolgenden Datenträger an. |
| Festplatte =`<n>,<n>[,<n>,...]` | Die dynamischen Datenträger, auf denen das Stripesetvolume erstellt wird. Sie benötigen mindestens zwei dynamische Datenträger, um ein Stripesetvolume zu erstellen. Eine Menge an Speicherplatz, `size=<n>` der gleich ist, wird auf jedem Datenträger zugeordnet. |
| ausrichten =`<n>` | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>`die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie auf den Datenträgern 1 und 2 Folgendes ein, um ein Stripesetvolume mit einer Größe von 1000 Megabyte zu erstellen:

```
create volume stripe size=1000 disk=1,2
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)
