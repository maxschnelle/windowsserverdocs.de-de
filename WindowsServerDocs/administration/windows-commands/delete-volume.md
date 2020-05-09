---
title: Volume löschen
description: Referenz Thema für den Befehl Volume löschen, mit dem das ausgewählte Volume gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 59856e89ff96d2881040365d157540dc62c1aeb0
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993098"
---
# <a name="delete-volume"></a>delete volume

Löscht das ausgewählte Volume. Bevor Sie beginnen, müssen Sie ein Volume auswählen, damit dieser Vorgang erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl [Volume auswählen](select-volume.md) ein Volume aus, und verschieben Sie den Fokus auf das Volume.

> [!IMPORTANT]
> Das System Volume, das Start Volume oder ein beliebiges Volume, das die aktive Auslagerungs Datei oder das Absturz Abbild (Speicher Abbild) enthält, können nicht gelöscht werden.

## <a name="syntax"></a>Syntax

```
delete volume [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Um das Volume mit dem Fokus zu löschen, geben Sie Folgendes ein:

```
delete volume
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [DELETE-Befehl](delete.md)