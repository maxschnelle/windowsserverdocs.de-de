---
title: Wbadmin-Restore-Katalog
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5876a44b178025baac7ee5901cdc32c1b5d33dad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851711"
---
# <a name="wbadmin-restore-catalog"></a>Wbadmin-Restore-Katalog



Wiederherstellung ein Sicherungskatalogs für den lokalen Computer einen Speicherort, den Sie angeben.

Zum Wiederherstellen eines Sicherungskatalogs mit diesem Unterbefehl muss ein Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-backupTarget|Gibt den Speicherort des Sicherungskatalogs des Systems, wie die zum Zeitpunkt angezeigt wurde, nachdem die Sicherung erstellt wurde.|
|-Computer|Gibt den Namen des Computers, der den Sicherungskatalog für wiederhergestellt werden soll. Wird verwendet, wenn Sie Sicherungen für mehrere Computer am gleichen Ort gespeichert worden sind. Sollte verwendet werden, wenn **- BackupTarget** angegeben ist.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="remarks"></a>Hinweise

Wenn der Speicherort (Datenträger, DVD oder freigegebenen Remoteordner), in dem Sie Ihre Sicherungen speichern, beschädigt oder verloren gegangen ist und nicht verwendet werden, verwenden Sie zum Wiederherstellen des Sicherungskatalogs **Wbadmin delete Catalog** den beschädigten Katalog zu löschen. In diesem Fall sollten Sie eine neue Sicherung erstellen, sobald Ihre Sicherungskatalog gelöscht wurde.

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Wiederherstellen eines Katalogs aus einer Sicherung auf Datenträger "d:" gespeichert:
```
wbadmin restore catalog -backupTarget:d
```
Zum Wiederherstellen eines Katalogs aus einer Sicherung in den freigegebenen Ordner gespeicherten \\ \\Servername\share von "SERVER01", Typ:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Restore-WBCatalog](https://technet.microsoft.com/library/jj902437.aspx) Cmdlet