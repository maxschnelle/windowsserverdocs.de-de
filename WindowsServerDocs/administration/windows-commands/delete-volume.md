---
title: delete volume
description: Referenz Artikel für den Befehl Volume löschen, mit dem das ausgewählte Volume gelöscht wird.
ms.topic: reference
ms.assetid: f625933d-0f47-409e-93b2-a3e234049a5d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 66793e9d7c22b337164807bf76ee82c10d70547c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628802"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [select volume](select-volume.md)

- [DELETE-Befehl](delete.md)