---
title: attributes disk
description: Referenz Artikel zum Befehl "Attribut Datenträger", mit dem die Attribute eines Datenträgers angezeigt, festgelegt oder gelöscht werden.
ms.topic: reference
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72b4a99c36085062441a7a8751a065dad1dd0c51
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029198"
---
# <a name="attributes-disk"></a>attributes disk

Hiermit werden die Attribute eines Datenträgers angezeigt, festgelegt oder gelöscht. Wenn dieser Befehl zum Anzeigen der aktuellen Attribute eines Datenträgers verwendet wird, kennzeichnet das Attribut des Start Datenträgers den Datenträger, der zum Starten des Computers verwendet wird. Bei einer dynamischen Spiegelung wird der Datenträger angezeigt, der den Start-Plex des Start Volume enthält.

> [!IMPORTANT]
> Ein Datenträger muss ausgewählt werden, damit der Befehl Datenträger für **Attribute** erfolgreich ist. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="syntax"></a>Syntax

```
attributes disk [{set | clear}] [readonly] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| set | Legt das angegebene Attribut des Datenträgers mit dem Fokus fest. |
| clear | Löscht das angegebene Attribut des Datenträgers mit dem Fokus. |
| readonly | Gibt an, dass der Datenträger schreibgeschützt ist. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Attribute des ausgewählten Datenträgers anzuzeigen:

```
attributes disk
```

Geben Sie Folgendes ein, um den ausgewählten Datenträger als schreibgeschützt festzulegen:

```
attributes disk set readonly
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Datenträger Befehl auswählen](select-disk.md)
