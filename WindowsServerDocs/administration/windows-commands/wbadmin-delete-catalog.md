---
title: Befehl Wbadmin Delete catalog
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d9f60cf79fcd856fa972d8f43f195c5823e5d81
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841411"
---
# <a name="wbadmin-delete-catalog"></a>Befehl Wbadmin Delete catalog



Löscht den Sicherungskatalog, der auf dem lokalen Computer gespeichert sind. Verwenden Sie diesen Befehl aus, bei der Sicherungskatalog beschädigt wurde und kann nicht wiederhergestellt werden die mit **Wbadmin Wiederherstellung Katalog**.

Zum Löschen eines Sicherungskatalogs mit diesem Unterbefehl muss ein Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin delete catalog
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="remarks"></a>Hinweise

Wenn Sie den Sicherungskatalog für einen Computer löschen, werden Sie nicht auf die Sicherungen dieses Computers mit dem Windows Server-Sicherung Snap-in erstellt zugreifen können. Wenn Sie einen anderen Sicherungsspeicherort zugreifen können, in diesem Fall verwenden Sie **Wbadmin Wiederherstellung Katalog** Sicherungskatalog von diesem Speicherort wiederhergestellt. Sie sollten eine neue Sicherung erstellen, sobald Ihre Sicherungskatalog gelöscht wurde.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Remove-WBCatalog](https://technet.microsoft.com/library/jj902445.aspx)