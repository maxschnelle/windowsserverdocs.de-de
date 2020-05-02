---
title: Wbadmin delete-Katalog
description: Referenz Thema für den Wbadmin delete-Katalog, mit dem der auf dem lokalen Computer gespeicherte Sicherungs Katalog gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73f6f44fb343d3347d18cf2c86913aea59613e07
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720215"
---
# <a name="wbadmin-delete-catalog"></a>Wbadmin delete-Katalog



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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Remove-wbcatalog](https://technet.microsoft.com/library/jj902445.aspx)