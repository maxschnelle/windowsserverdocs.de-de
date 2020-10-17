---
title: wbadmin delete catalog
description: Referenz Artikel für den Befehl Wbadmin delete catalog, mit dem der auf dem lokalen Computer gespeicherte Sicherungs Katalog gelöscht wird.
ms.topic: reference
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4a19d856b65fdcf17fb369d81607445530f77275
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156105"
---
# <a name="wbadmin-delete-catalog"></a>wbadmin delete catalog

Löscht den Sicherungs Katalog, der auf dem lokalen Computer gespeichert ist. Verwenden Sie diesen Befehl, wenn der Sicherungs Katalog beschädigt wurde und Sie ihn mit dem Befehl " [Wbadmin restore catalog](wbadmin-restore-catalog.md) " nicht wiederherstellen können.

Zum Löschen eines Sicherungs Katalogs mithilfe dieses Befehls müssen Sie Mitglied der Gruppe "Sicherungs- **Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```
wbadmin delete catalog [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

#### <a name="remarks"></a>Hinweise

- Wenn Sie den Sicherungs Katalog eines Computers löschen, sind Sie nicht mehr in der Lage, mit dem Windows Server-Sicherung-Snap-in auf die für diesen Computer erstellten Sicherungen zu gelangen. Wenn Sie jedoch zu einem anderen Sicherungsort gelangen und den Befehl [Wbadmin restore catalog](wbadmin-restore-catalog.md) ausführen können, können Sie den Sicherungs Katalog von diesem Speicherort wiederherstellen.

- Es wird dringend empfohlen, nach dem Löschen eines Sicherungs Katalogs eine neue Sicherung zu erstellen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "Wbadmin restore catalog"](wbadmin-restore-catalog.md)

- [Remove-wbcatalog](/powershell/module/windowsserverbackup/Remove-WBCatalog)
