---
title: wbadmin get items
description: Referenz Artikel für den Befehl Wbadmin Get Items, der die Elemente auflistet, die in einer bestimmten Sicherung enthalten sind.
ms.topic: reference
ms.assetid: 27d08ce3-6e06-4260-b264-fc1bde132d09
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5eda5977c0c7606f0e1031894360a06205044656
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155871"
---
# <a name="wbadmin-get-items"></a>wbadmin get items

Listet die Elemente auf, die in einer bestimmten Sicherung enthalten sind.

Um die in einer bestimmten Sicherung enthaltenen Elemente mithilfe dieses Befehls aufzulisten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```
wbadmin get items -version:<VersionIdentifier> [-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}] [-machine:<BackupMachineName>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -version | Gibt die Version der Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie die Versionsinformationen nicht kennen, führen Sie den Befehl [Wbadmin Get Versions](wbadmin-get-versions.md) aus. |
| -backupTarget | Gibt den Speicherort an, der die Sicherungen enthält, für die Sie Details anzeigen möchten. Verwenden Sie zum Auflisten der an diesem Ziel Speicherort gespeicherten Sicherungen. Bei Sicherungs Ziel Standorten kann es sich um ein lokal angefügtes Laufwerk oder einen freigegebenen Remote Ordner handeln. Wenn dieser Befehl auf dem gleichen Computer ausgeführt wird, auf dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Dieser Parameter ist jedoch erforderlich, um Informationen zu einer Sicherung zu erhalten, die von einem anderen Computer erstellt wurde. |
| -Computer | Gibt den Namen des Computers an, für den Sie die Sicherungs Details anzeigen möchten. Nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird. |

## <a name="examples"></a>Beispiele

Zum Auflisten von Elementen aus der Sicherung, die am 31. März 2013 um 9:00 Uhr ausgeführt wurde, geben Sie Folgendes ein:

```
wbadmin get items -version:03/31/2013-09:00
```

So Listen Sie Elemente aus der Sicherung von Server01 auf, die am 2013 30. April um 9:00 Uhr ausgeführt wurde und in gespeichert `\\<servername>\<share>` sind, geben Sie Folgendes ein:

```
wbadmin get items -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "WBADMIN GET Versions"](wbadmin-get-versions.md)

- [Get-wbbackaufgeregt](/powershell/module/windowserverbackup/Get-WBBackupSet)
