---
title: create volume simple
description: Referenz Artikel für den Befehl Volume Simple erstellen, mit dem ein einfaches Volume auf dem angegebenen dynamischen Datenträger erstellt wird.
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a434cc959eac79011cf57e2aca101ffc536b7633
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891628"
---
# <a name="create-volume-simple"></a>create volume simple

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt ein einfaches Volume auf dem angegebenen dynamischen Datenträger. Nachdem Sie das Volume erstellt haben, wird der Fokus automatisch auf das neue Volume verlagert.

## <a name="syntax"></a>Syntax

```
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Größe =`<n>`  | Die Größe des Volumes in Megabyte (MB). Wenn keine Größe angegeben wird, nimmt das neue Volume den verbleibenden freien Speicherplatz auf dem Datenträger an. |
| Festplatte =`<n>`  | Der dynamische Datenträger, auf dem das Volume erstellt wird. Wenn kein Datenträger angegeben ist, wird der aktuelle Datenträger verwendet. |
| ausrichten =`<n>` | Richtet alle volumeblöcke an der nächstgelegenen Ausrichtungs Grenze aus. Wird in der Regel mit den Hardware-RAID-Arrays der logischen Gerätenummer verwendet, um die Leistung zu verbessern. `<n>`die Anzahl der Kilobyte (KB) vom Anfang des Datenträgers bis zur nächsten Ausrichtungs Grenze. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie auf Datenträger 1 Folgendes ein, um ein Volume mit einer Größe von 1000 Megabyte zu erstellen:

```
create volume simple size=1000 disk=1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Create-Befehl](create.md)
