---
title: online volume
description: Referenz Artikel für den Online Volume-Befehl, bei dem das Offline Volume in den Online Status versetzt wird.
ms.topic: reference
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a53b3e3955f1435c9f34b4d2b16f17685d6b3bb4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627275"
---
# <a name="online-volume"></a>online volume

Schaltet das Offline Volume in den Online Zustand. Dieser Befehl funktioniert auf Volumes, bei denen Fehler aufgetreten sind, bei denen Fehler auftreten oder der Redundanz Status nicht erfüllt ist.

> [!NOTE]
> Ein Volume muss ausgewählt werden, damit der **Online Volume-** Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl [Volume auswählen](select-volume.md) ein Volume aus, und verschieben Sie den Fokus auf das Volume.

> [!IMPORTANT]
> Dieser Befehl schlägt fehl, wenn er auf einem schreibgeschützten Datenträger verwendet wird.

## <a name="syntax"></a>Syntax

```
online volume [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Volume mit dem Fokus online zu schalten:

```
online volume
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
