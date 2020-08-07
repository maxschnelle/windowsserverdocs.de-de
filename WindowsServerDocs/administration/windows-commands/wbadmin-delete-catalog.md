---
title: wbadmin delete catalog
description: Referenz Artikel zum Löschen eines Wbadmin-Katalogs, mit dem der auf dem lokalen Computer gespeicherte Sicherungs Katalog gelöscht wird.
ms.topic: article
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c43c201c4c14b3eab14fd8e1ec0d6d3e39fe4104
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892233"
---
# <a name="wbadmin-delete-catalog"></a>wbadmin delete catalog



Löscht den Sicherungs Katalog, der auf dem lokalen Computer gespeichert ist. Verwenden Sie diesen Befehl, wenn der Sicherungs Katalog beschädigt wurde und Sie ihn nicht mit dem **Wbadmin restore catalog**wiederherstellen können.

Wenn Sie einen Sicherungs Katalog mit diesem Unterbefehl löschen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin delete catalog
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="remarks"></a>Bemerkungen

Wenn Sie den Sicherungs Katalog für einen Computer löschen, sind Sie nicht in der Lage, mit dem Windows Server-Sicherung-Snap-in auf die Sicherungen zuzugreifen, die von diesem Computer erstellt wurden. Wenn Sie in diesem Fall auf einen anderen Sicherungs Speicherort zugreifen können, verwenden Sie den **Wbadmin restore catalog** , um den Sicherungs Katalog von diesem Speicherort wiederherzustellen. Sie sollten eine neue Sicherung erstellen, sobald der Sicherungs Katalog gelöscht wurde.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Remove-wbcatalog](/powershell/module/windowserverbackup/?view=winserver2012r2-ps)
