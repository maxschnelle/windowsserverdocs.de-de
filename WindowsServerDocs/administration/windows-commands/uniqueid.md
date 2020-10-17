---
title: uniqueid
description: Referenz Artikel für UniqueId, der die GUID-Partitionstabelle (GPT) oder die Master Boot Record (MBR)-Signatur für den Datenträger mit dem Fokus anzeigt oder festlegt.
ms.topic: reference
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 73721316747ffd0380f178622d37dc4fdbefc2fb
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156293"
---
# <a name="uniqueid"></a>uniqueid

Zeigt den GPT-Bezeichner (GUID-Partitionstabelle) oder die Master Boot Record (MBR)-Signatur für den Basis-oder dynamischen Datenträger mit Fokus an oder legt ihn fest. Ein einfacher oder dynamischer Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl Datenträger [auswählen](select-disk.md) einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="syntax"></a>Syntax

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| ID =`{<dword> | <GUID>}` | Bei MBR-Datenträgern gibt dieser Parameter einen 4-Byte-Wert (DWORD) in Hexadezimal Form für die Signatur an. Für GPT-Datenträger gibt dieser Parameter eine GUID für den Bezeichner an. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Signatur des MBR-Datenträgers mit dem Fokus anzuzeigen:

```
uniqueid disk
```

Wenn Sie die Signatur des MBR-Datenträgers mit dem Fokus auf den DWORD-Wert *5f1b2c36*festlegen möchten, geben Sie Folgendes ein:

```
uniqueid disk id=5f1b2c36
```

Um den Bezeichner des GPT-Datenträgers mit dem Fokus auf den GUID-Wert baf784e7-6bbd-4cfb-aaac-e86c96e166ee festzulegen, geben Sie Folgendes ein:

```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Datenträger Befehl auswählen](select-disk.md)
