---
title: recover
description: Referenz Artikel für den Wiederherstellungs Befehl DiskPart, mit dem der Status aller Datenträger in einer Datenträger Gruppe aktualisiert wird, Datenträger in einer ungültigen Datenträger Gruppe wieder hergestellt werden und gespiegelte Volumes und RAID-5-Volumes mit veralteten Daten neu synchronisiert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19272e09147bb730e07d51d42926c01262bfb433
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924797"
---
# <a name="recover"></a>recover

Aktualisiert den Status aller Datenträger in einer Datenträger Gruppe, versucht, Datenträger in einer ungültigen Datenträger Gruppe wiederherzustellen, und synchronisiert die gespiegelten Volumes und RAID-5-Volumes mit veralteten Daten erneut. Dieser Befehl funktioniert auf Datenträgern, die fehlerhaft sind oder fehlschlagen. Sie funktioniert auch auf Volumes, die fehlerhaft oder fehlerhaft oder in fehlerhafter Redundanz Zustand sind.

Dieser Befehl wird für gruppendynamischer Datenträger angewendet. Wenn dieser Befehl in einer Gruppe mit einem Basis Datenträger verwendet wird, wird kein Fehler zurückgegeben, aber es wird keine Aktion ausgeführt.

> [!NOTE]
>  Ein Datenträger, der Teil einer Datenträger Gruppe ist, muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden kann. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.



## <a name="syntax"></a>Syntax

```
recover [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datenträger Gruppe mit dem Fokus auf dem Datenträger wiederherzustellen:

```
recover
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
