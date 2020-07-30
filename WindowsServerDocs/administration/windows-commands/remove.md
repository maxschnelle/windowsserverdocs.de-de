---
title: remove
description: Referenz Artikel für den remove-Befehl, mit dem ein Laufwerk Buchstabe oder ein Einstellungspunkt von einem Volume entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b0886140-da8b-4231-8cb2-f280874d99c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fba062945effd49efa9987d2c7d23fc90552fd4
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409681"
---
# <a name="remove"></a>remove

Entfernt einen Laufwerk Buchstaben oder einen Einfügepunkt aus dem Volume mit dem Fokus. Wenn der All-Parameter verwendet wird, werden alle aktuellen Laufwerk Buchstaben und Einstellungspunkte entfernt. Wenn kein Laufwerk Buchstabe oder Einfügepunkt angegeben ist, entfernt DiskPart den ersten Laufwerk Buchstaben oder Einstellungspunkt, auf den er trifft.

Der Befehl Remove kann auch verwendet werden, um den Laufwerk Buchstaben zu ändern, der einem Wechsel Datenträger zugeordnet ist. Sie können die Laufwerk Buchstaben auf System-, Start-oder Auslagerungs Volumes nicht entfernen. Darüber hinaus können Sie den Laufwerk Buchstaben für eine OEM-Partition, GPT-Partitionen mit einer nicht erkannten GUID oder eine der speziellen, nicht-Daten-GPT-Partitionen (z. b. die EFI-Systempartition) nicht entfernen.

> [!NOTE]
> Ein Volume muss ausgewählt werden, damit der Befehl zum **Entfernen** erfolgreich ist. Wählen Sie mit dem Befehl [Volume auswählen](select-volume.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="syntax"></a>Syntax

```
remove [{letter=<drive> | mount=<path> [all]}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Buchstabe =`<drive>` | Der Laufwerk Buchstabe, der entfernt werden soll. |
| einbinden =`<path>` | Der zu entfern gende Pfad für den Einstellungspunkt. |
| alle | Entfernt alle aktuellen Laufwerk Buchstaben und Einstellungspunkte. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

### <a name="examples"></a>Beispiele

So entfernen Sie d:\ Laufwerk, geben Sie Folgendes ein:

```
remove letter=d
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
