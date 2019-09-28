---
title: Wbadmin-Wiederherstellungs Katalog
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b0d646440ca9b30f9fa30fb1ac3ff08458b8e44d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362327"
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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-backupTarget|Gibt den Speicherort des Sicherungs Katalogs des Systems an dem Punkt an, an dem die Sicherung erstellt wurde.|
|-Computer|Gibt den Namen des Computers an, für den Sie den Sicherungs Katalog wiederherstellen möchten. Verwenden Sie, wenn Sicherungen für mehrere Computer am gleichen Speicherort gespeichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="remarks"></a>Hinweise

Wenn der Speicherort (Datenträger, DVD oder frei gegebener Remote Ordner), in dem Sie die Sicherungen speichern, beschädigt ist oder verloren geht und nicht zum Wiederherstellen des Sicherungs Katalogs verwendet werden kann, verwenden Sie **Wbadmin delete catalog** , um den beschädigten Katalog zu löschen. In diesem Fall sollten Sie eine neue Sicherung erstellen, sobald der Sicherungs Katalog gelöscht wurde.

## <a name="BKMK_examples"></a>Beispiele

Um einen Katalog aus einer auf Datenträger d: gespeicherten Sicherung wiederherzustellen, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:d
```
Wenn Sie einen Katalog aus einer im freigegebenen Ordner gespeicherten Sicherung wiederherstellen möchten \\ @ no__t-1servername\share von Server01, geben Sie Folgendes ein:
```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Restore-wbcatalog-](https://technet.microsoft.com/library/jj902437.aspx) Cmdlet