---
title: wbadmin get items
description: Referenz Artikel für Wbadmin Get Items, der die in einer bestimmten Sicherung enthaltenen Elemente auflistet.
ms.topic: reference
ms.assetid: 27d08ce3-6e06-4260-b264-fc1bde132d09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e82bfc6cee3a8ff6a4fd0165770870d09a0873e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031998"
---
# <a name="wbadmin-get-items"></a>wbadmin get items



Listet die Elemente auf, die in einer bestimmten Sicherung enthalten sind.

Um diesen Unterbefehl verwenden zu können, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin get items
-version:<VersionIdentifier>
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-version|Gibt die Version der Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie die Versionsinformationen nicht kennen, geben Sie **Wbadmin Get Versions**ein.|
|-backupTarget|Gibt den Speicherort an, der die Sicherungen enthält, für die Sie Details anzeigen möchten. Verwenden Sie zum Auflisten der an diesem Ziel Speicherort gespeicherten Sicherungen. Bei Sicherungs Ziel Standorten kann es sich um ein lokal angefügtes Laufwerk oder einen freigegebenen Remote Ordner handeln. Wenn **Wbadmin Get Items**auf dem gleichen Computer ausgeführt wird, auf dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Dieser Parameter ist jedoch erforderlich, um Informationen zu einer Sicherung zu erhalten, die von einem anderen Computer erstellt wurde.|
|-Computer|Gibt den Namen des Computers an, für den Sie die Sicherungs Details anzeigen möchten. Nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird.|

## <a name="examples"></a>Beispiele

Zum Auflisten von Elementen aus der Sicherung, die am 31. März 2013 um 9:00 Uhr ausgeführt wurde, geben Sie Folgendes ein:
```
wbadmin get items -version:03/31/2013-09:00
```
So Listen Sie Elemente aus der Sicherung von Server01 auf, die am 2013 30. April um 9:00 Uhr ausgeführt wurde und auf \\ \\ servername\share gespeichert ist, geben Sie Folgendes ein:
```
wbadmin get items -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-wbbackaufgeregt](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) -Cmdlet
