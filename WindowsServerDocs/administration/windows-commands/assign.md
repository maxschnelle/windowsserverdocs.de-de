---
title: assign
description: Referenz Artikel für den Assign-Befehl, der dem Volume einen Laufwerk Buchstaben oder einen Einfügepunkt mit Fokus zuweist.
ms.topic: reference
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a453790b3622804138794b9656b18ed160e6f676
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029318"
---
# <a name="assign"></a>assign

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Weist dem Volume mit dem Fokus einen Laufwerk Buchstaben oder einen Einfügepunkt zu. Sie können diesen Befehl auch verwenden, um den Laufwerk Buchstaben zu ändern, der einem Wechsel Datenträger zugeordnet ist. Wenn kein Laufwerk Buchstabe oder Einfügepunkt angegeben ist, wird der nächste verfügbare Laufwerk Buchstabe zugewiesen. Wenn der Laufwerk Buchstabe oder der Einfügepunkt bereits verwendet wird, wird ein Fehler generiert.

Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Volume auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.

> [!IMPORTANT]
> Sie können System Volumes, Startvolumes oder Volumes, die die Auslagerungs Datei enthalten, keine Laufwerk Buchstaben zuweisen. Außerdem ist es nicht möglich, einem Original Gerätehersteller (OEM) oder einer anderen GPT-Partition (GUID-Partitionstabelle) einen Laufwerk Buchstaben zuzuweisen, der keine grundlegende Daten Partition ist.

## <a name="syntax"></a>Syntax

```
assign [{letter=<d> | mount=<path>}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `letter=<d>` | Der Laufwerk Buchstabe, der dem Volume zugewiesen werden soll. |
| `mount=<path>` | Der Pfad des einstellungspunkts, der dem Volume zugewiesen werden soll. Anweisungen zur Verwendung dieses Befehls finden [Sie unter Zuweisen eines Ordners für einen einstellungspunktpfad zu einem Laufwerk](../../storage/disk-management/assign-a-mount-point-folder-path-to-a-drive.md). |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Buchstaben E dem Volume im Fokus zuzuweisen:

```
assign letter=e
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Volume auswählen"](select-volume.md)
