---
title: wbadmin restore catalog
description: Referenz Artikel für den Befehl Wbadmin restore catalog, der einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wiederherstellt.
ms.topic: reference
ms.assetid: ce1e24a0-821d-4353-b09d-8f82c5c4ad56
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 046c4b4162c9512d5893c3c06e83e7260386c990
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155865"
---
# <a name="wbadmin-restore-catalog"></a>wbadmin restore catalog

Stellt einen Sicherungs Katalog für den lokalen Computer von einem von Ihnen angegebenen Speicherort wieder her.

Zum Wiederherstellen eines Sicherungs Katalogs, der mit diesem Befehl in einer bestimmten Sicherung enthalten ist, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

> [!NOTE]
> Wenn der Speicherort (Datenträger, DVD oder frei gegebener Remote Ordner), in dem Sie die Sicherungen speichern, beschädigt ist oder verloren gegangen ist und nicht zum Wiederherstellen des Sicherungs Katalogs verwendet werden kann, führen Sie den Befehl [Wbadmin delete catalog](wbadmin-delete-catalog.md) aus, um den beschädigten Katalog zu löschen. In diesem Fall empfiehlt es sich, nach dem Löschen des Sicherungs Katalogs eine neue Sicherung zu erstellen.

## <a name="syntax"></a>Syntax

```
wbadmin restore catalog -backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>} [-machine:<BackupMachineName>] [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -backupTarget | Gibt den Speicherort des Sicherungs Katalogs des Systems an dem Punkt an, an dem die Sicherung erstellt wurde. |
| -Computer | Gibt den Namen des Computers an, für den Sie den Sicherungs Katalog wiederherstellen möchten. Verwenden Sie, wenn Sicherungen für mehrere Computer am gleichen Speicherort gespeichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

Um einen Katalog aus einer auf Datenträger D: gespeicherten Sicherung wiederherzustellen, geben Sie Folgendes ein:

```
wbadmin restore catalog -backupTarget:D
```

Um einen Katalog aus einer Sicherung wiederherzustellen, die im freigegebenen Ordner `\\<servername>\<share>` von Server01 gespeichert ist, geben Sie Folgendes ein:

```
wbadmin restore catalog -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "delete catalog" in Wbadmin](wbadmin-delete-catalog.md)

- [Restore-wbcatalog](/powershell/module/windowserverbackup/Restore-WBCatalog)
