---
title: wbadmin get versions
description: Referenz Artikel für den Befehl Wbadmin Get Versions, der Details zu den verfügbaren Sicherungen auflistet, die auf dem lokalen Computer oder einem anderen Computer gespeichert sind.
ms.topic: reference
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6825b515f028046702283a2374de26100fd3015f
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155928"
---
# <a name="wbadmin-get-versions"></a>wbadmin get versions

Listet Details zu den verfügbaren Sicherungen, die auf dem lokalen Computer oder einem anderen Computer gespeichert sind. Die für eine Sicherung bereitgestellten Details umfassen die Sicherungs Zeit, den Sicherungs Speicherort, den Versions Bezeichner und den Typ der Wiederherstellungen, die Sie ausführen können.

Um Details zu verfügbaren Sicherungen mit diesem Befehl anzuzeigen, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

Wenn dieser Befehl ohne Parameter verwendet wird, werden alle Sicherungen des lokalen Computers aufgelistet, auch wenn diese Sicherungen nicht verfügbar sind.

## <a name="syntax"></a>Syntax

```
wbadmin get versions [-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}] [-machine:BackupMachineName]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -backupTarget | Gibt den Speicherort an, der die Sicherungen enthält, für die Sie Details anzeigen möchten. Verwenden Sie zum Auflisten der an diesem Ziel Speicherort gespeicherten Sicherungen. Sicherungs Zielspeicher Orte können lokal angefügte Laufwerke, Volumes, freigegebene Remote Ordner, Wechselmedien wie DVD-Laufwerke oder andere optische Medien sein. Wenn dieser Befehl auf dem gleichen Computer ausgeführt wird, auf dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Dieser Parameter ist jedoch erforderlich, um Informationen zu einer Sicherung zu erhalten, die von einem anderen Computer erstellt wurde. |
| -Computer | Gibt den Computer an, für den Sie Sicherungs Details anzeigen möchten. Verwenden Sie, wenn Sicherungen mehrerer Computer am gleichen Speicherort gespeichert werden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der verfügbaren Sicherungen anzuzeigen, die auf dem Volume H: gespeichert sind:

```
wbadmin get versions -backupTarget:H:
```

Wenn Sie eine Liste der verfügbaren Sicherungen anzeigen möchten, die im freigegebenen Remote Ordner `\\<servername>\<share>` für den Computer Server01 gespeichert sind, geben Sie Folgendes ein:

```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Befehl "Get Items" in Wbadmin](wbadmin-get-items.md)

- [Get-wbbackuptarget](/powershell/module/windowserverbackup/Get-WBBackupTarget)
