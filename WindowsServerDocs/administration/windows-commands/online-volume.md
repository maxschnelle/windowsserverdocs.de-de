---
title: online volume
description: Referenz Thema für den Online Volume-Befehl, bei dem das Offline Volume in den Online Status versetzt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83a1e4bf1d6afe9485ab71c9af372166797900b3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472666"
---
# <a name="online-disk"></a>online disk

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
