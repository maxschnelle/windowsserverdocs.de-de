---
title: online disk
description: Referenz Artikel für den Online-Datenträger Befehl, bei dem der Offline Datenträger in den Online Status versetzt wird.
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81bfd2dfc8e32656602066d702e8c1af5f4d1c82
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885245"
---
# <a name="online-disk"></a>online disk

Der Offline Datenträger wird in den Online Zustand versetzt. Bei Basis Datenträgern versucht dieser Befehl, den ausgewählten Datenträger und alle Volumes auf diesem Datenträger online zu schalten. Bei dynamischen Datenträgern wird mit diesem Befehl versucht, alle Datenträger online zu schalten, die auf dem lokalen Computer nicht als fremd gekennzeichnet sind. Außerdem wird versucht, alle Volumes auf dem Satz dynamischer Datenträger online zu schalten.

Wenn ein dynamischer Datenträger in einer Datenträger Gruppe online geschaltet wird und es sich um den einzigen Datenträger in der Gruppe handelt, wird die ursprüngliche Gruppe neu erstellt, und der Datenträger wird in diese Gruppe verschoben. Wenn die Gruppe andere Datenträger enthält und Sie online sind, wird der Datenträger einfach wieder der Gruppe hinzugefügt. Wenn die Gruppe eines ausgewählten Datenträgers gespiegelte oder RAID-5-Volumes enthält, werden diese Volumes von diesem Befehl ebenfalls neu synchronisiert.

> [!NOTE]
> Ein Datenträger muss ausgewählt werden, damit der **Online Disk-** Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

> [!IMPORTANT]
> Dieser Befehl schlägt fehl, wenn er auf einem schreibgeschützten Datenträger verwendet wird.

## <a name="syntax"></a>Syntax

```
online disk [noerr]
```

### <a name="parameters"></a>Parameter

Anweisungen zur Verwendung dieses Befehls finden Sie unter Erneutes [Aktivieren eines fehlenden oder offline](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732026(v=ws.11))geschalteten dynamischen Datenträgers.

| Parameter | BESCHREIBUNG |
|--|--|
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Datenträger online zu schalten:

```
online disk
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
