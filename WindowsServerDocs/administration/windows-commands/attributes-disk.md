---
title: Attribute-Datenträger
description: Windows-Befehls Artikel für **Attribut**Datenträger, auf dem die Attribute eines Datenträgers angezeigt, festgelegt oder gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3c29a009a1efdfb7fed3d04d194cc8cfd2ea4eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851243"
---
# <a name="attributes-disk"></a>Attribute-Datenträger

Hiermit werden die Attribute eines Datenträgers angezeigt, festgelegt oder gelöscht.

## <a name="syntax"></a>Syntax

```
attributes disk [{set | clear}] [readonly] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| set | Legt das angegebene Attribut des Datenträgers mit dem Fokus fest. |
| nicht aktiviert | Löscht das angegebene Attribut des Datenträgers mit dem Fokus. |
| readonly | Gibt an, dass der Datenträger schreibgeschützt ist. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Hinweise

-   Wenn **Attribute Disk** verwendet wird, um die aktuellen Attribute eines Datenträgers anzuzeigen, gibt das Attribut des Start Datenträgers den Datenträger an, der zum Starten des Computers verwendet wird. Bei einer dynamischen Spiegelung wird diese für den Datenträger angezeigt, der den Start-Plex des Start Volume enthält.

-   Ein Datenträger muss ausgewählt werden, damit der Befehl Datenträger für **Attribute** erfolgreich ist. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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