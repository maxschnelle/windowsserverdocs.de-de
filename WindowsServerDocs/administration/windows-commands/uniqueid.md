---
title: uniqueid
description: Referenz Artikel für UniqueId, der die GUID-Partitionstabelle (GPT) oder die Master Boot Record (MBR)-Signatur für den Datenträger mit dem Fokus anzeigt oder festlegt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5acf29d9a7dfd505a5ecdad2a08dfdb1a9f4d975
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937279"
---
# <a name="uniqueid"></a>uniqueid

Zeigt den GPT-Bezeichner (GUID-Partitionstabelle) oder die Master Boot Record (MBR)-Signatur für den Datenträger mit Fokus an oder legt ihn fest.

> [!IMPORTANT]
> Dieser Diskpart-Befehl ist in keiner Edition von Windows Vista verfügbar.

## <a name="syntax"></a>Syntax

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

### <a name="parameters"></a>Parameter

|  Parameter   |                                                                                             Beschreibung                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID = {\<dword> |                                                                                               <GUID>}                                                                                                |
|    Noerr     | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird. |

## <a name="remarks"></a>Hinweise

-   Dieser Befehl funktioniert auf grundlegenden und dynamischen Datenträgern.
-   Ein Datenträger muss ausgewählt werden, damit dieser Befehl erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl Datenträger **auswählen** einen Datenträger aus, und verschieben Sie den Fokus auf den Datenträger.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Signatur des MBR-Datenträgers mit dem Fokus anzuzeigen:
```
uniqueid disk
```
Wenn Sie die Signatur des MBR-Datenträgers mit dem Fokus auf 5f1b2c36 festlegen möchten, geben Sie Folgendes ein:
```
uniqueid disk id=5f1b2c36
```
Um den Bezeichner des GPT-Datenträgers mit dem Fokus auf baf784e7-6bbd-4cfb-aaac-e86c96e166ee festzulegen, geben Sie Folgendes ein:
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

## <a name="additional-references"></a>Weitere Verweise

