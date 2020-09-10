---
title: wbadmin restore catalog
description: Referenz Artikel für den Wbadmin-Wiederherstellungs Katalog, der einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wiederherstellt.
ms.topic: reference
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c551aa77ff98a66d3faacc3901806be8cc67b8f2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637600"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog

Stellt einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wieder her.

Wenn Sie einen Sicherungs Katalog mit diesem Unterbefehl wiederherstellen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-backupTarget|Gibt den Speicherort des Sicherungs Katalogs des Systems an dem Punkt an, an dem die Sicherung erstellt wurde.|
|-Computer|Gibt den Namen des Computers an, für den Sie den Sicherungs Katalog wiederherstellen möchten. Verwenden Sie, wenn Sicherungen für mehrere Computer am gleichen Speicherort gespeichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="remarks"></a>Hinweise

Wenn der Speicherort (Datenträger, DVD oder frei gegebener Remote Ordner), in dem Sie die Sicherungen speichern, beschädigt ist oder verloren geht und nicht zum Wiederherstellen des Sicherungs Katalogs verwendet werden kann, verwenden Sie **Wbadmin delete catalog** , um den beschädigten Katalog zu löschen. In diesem Fall sollten Sie eine neue Sicherung erstellen, sobald der Sicherungs Katalog gelöscht wurde.

## <a name="examples"></a>Beispiele

Um einen Katalog aus einer auf Datenträger d: gespeicherten Sicherung wiederherzustellen, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:d
```
Um einen Katalog aus einer Sicherung wiederherzustellen, die im freigegebenen Ordner \\ \\ servername\share von Server01 gespeichert ist, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Restore-wbcatalog-](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) Cmdlet
