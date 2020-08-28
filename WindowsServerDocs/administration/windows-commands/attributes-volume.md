---
title: attributes volume
description: Referenz Artikel für den Befehl Attribut Volume, in dem die Attribute eines Volumes angezeigt, festgelegt oder gelöscht werden.
ms.topic: reference
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71f11eb692676cec4121e2ea24aed123f6a7d7d5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029188"
---
# <a name="attributes-volume"></a>attributes volume

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden die Attribute eines Volumes angezeigt, festgelegt oder gelöscht.

## <a name="syntax"></a>Syntax

```
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ------- | -------- |
| set | Legt das angegebene Attribut des Volumes mit dem Fokus fest. |
| clear | Löscht das angegebene Attribut des Volumes mit dem Fokus. |
| readonly | Gibt an, dass das Volume schreibgeschützt ist. |
| hidden | Gibt an, dass das Volume ausgeblendet ist. |
| nodefaultdriveletter | Gibt an, dass das Volume standardmäßig keinen Laufwerk Buchstaben erhält. |
| "Shadowcopy | Gibt an, dass das Volume ein Schattenkopievolume ist. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="remarks"></a>Bemerkungen

- Auf den MBR-Datenträgern (Basic Master Boot Record) gelten die Parameter **Hidden**, Read **only**und **nodefaultdriveletter** für alle Volumes auf dem Datenträger.

- Auf einfachen GPT-Datenträgern (GUID-Partitionstabelle) und auf dynamischen MBR-und GPT-Datenträgern gelten die Parameter **Hidden**, Read **only**und **nodefaultdriveletter** nur für das ausgewählte Volume.

- Es muss ein Volume ausgewählt werden, damit der **Attribut Volume** -Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

## <a name="examples"></a>Beispiele

Wenn Sie die aktuellen Attribute auf dem ausgewählten Volume anzeigen möchten, geben Sie Folgendes ein:

```
attributes volume
```

Um das ausgewählte Volume als ausgeblendet und schreibgeschützt festzulegen, geben Sie Folgendes ein:

```
attributes volume set hidden readonly
```

Um die ausgeblendeten und schreibgeschützten Attribute auf dem ausgewählten Volume zu entfernen, geben Sie Folgendes ein:

```
attributes volume clear hidden readonly
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Volume auswählen"](select-volume.md)
