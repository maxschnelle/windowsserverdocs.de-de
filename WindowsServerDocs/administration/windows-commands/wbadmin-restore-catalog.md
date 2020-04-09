---
title: Wbadmin-Wiederherstellungs Katalog
description: Windows-Befehls Thema für den Wbadmin-Wiederherstellungs Katalog, der einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wiederherstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ce9182e4e405b1538277db25f06b6a49d7240f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80829703"
---
# <a name="wbadmin-restore-catalog"></a>Wbadmin-Wiederherstellungs Katalog



Stellt einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wieder her.

Wenn Sie einen Sicherungs Katalog mit diesem Unterbefehl wiederherstellen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele für die Verwendung dieses Unterbefehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin restore catalog
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-quiet]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-backupTarget|Gibt den Speicherort des Sicherungs Katalogs des Systems an dem Punkt an, an dem die Sicherung erstellt wurde.|
|-Computer|Gibt den Namen des Computers an, für den Sie den Sicherungs Katalog wiederherstellen möchten. Verwenden Sie, wenn Sicherungen für mehrere Computer am gleichen Speicherort gespeichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="remarks"></a>Hinweise

Wenn der Speicherort (Datenträger, DVD oder frei gegebener Remote Ordner), in dem Sie die Sicherungen speichern, beschädigt ist oder verloren geht und nicht zum Wiederherstellen des Sicherungs Katalogs verwendet werden kann, verwenden Sie **Wbadmin delete catalog** , um den beschädigten Katalog zu löschen. In diesem Fall sollten Sie eine neue Sicherung erstellen, sobald der Sicherungs Katalog gelöscht wurde.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Um einen Katalog aus einer auf Datenträger d: gespeicherten Sicherung wiederherzustellen, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:d
```
Wenn Sie einen Katalog aus einer Sicherung wiederherstellen möchten, die im freigegebenen Ordner \\\\servername\share von Server01 gespeichert ist, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Restore-wbcatalog-](https://technet.microsoft.com/library/jj902437.aspx) Cmdlet