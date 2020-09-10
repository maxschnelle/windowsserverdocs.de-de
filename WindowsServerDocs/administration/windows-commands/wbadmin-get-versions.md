---
title: wbadmin get versions
description: Referenz Artikel für Wbadmin Get-Versionen, die Details zu den verfügbaren Sicherungen auflisten, die auf dem lokalen Computer oder einem anderen Computer gespeichert sind.
ms.topic: reference
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f3b9f5ca967e3d125575809bc4bd882d37eef5ff
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640274"
---
# <a name="wbadmin-get-versions"></a>wbadmin get versions



Listet Details zu den verfügbaren Sicherungen, die auf dem lokalen Computer oder einem anderen Computer gespeichert sind. Wenn dieser Unterbefehl ohne Parameter verwendet wird, listet er alle Sicherungen des lokalen Computers auf, auch wenn diese Sicherungen nicht verfügbar sind. Die für eine Sicherung bereitgestellten Details umfassen die Sicherungs Zeit, den Sicherungs Speicherort, den Versions Bezeichner (erforderlich für den Unterbefehl **Wbadmin Get Items** und Wiederherstellungen) und den Typ der Wiederherstellungen, die Sie ausführen können.

Um Details zu verfügbaren Sicherungen mit diesem Unterbefehl anzuzeigen, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Öffnen Sie **eine Eingabeaufforderung** mit erhöhten Rechten, und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin get versions
[-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}]
[-machine:BackupMachineName]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-backupTarget|Gibt den Speicherort an, der die Sicherungen enthält, für die Sie Details anzeigen möchten. Verwenden Sie zum Auflisten der an diesem Ziel Speicherort gespeicherten Sicherungen. Sicherungs Zielspeicher Orte können lokal angefügte Laufwerke, Volumes, freigegebene Remote Ordner, Wechselmedien wie DVD-Laufwerke oder andere optische Medien sein. Wenn **Wbadmin Get-Versionen** auf dem gleichen Computer ausgeführt wird, auf dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Dieser Parameter ist jedoch erforderlich, um Informationen zu einer Sicherung zu erhalten, die von einem anderen Computer erstellt wurde.|
|-Computer|Gibt den Computer an, für den Sie Sicherungs Details anzeigen möchten. Verwenden Sie, wenn Sicherungen mehrerer Computer am gleichen Speicherort gespeichert werden. Sollte verwendet werden, wenn " **-backupTarget** " angegeben wird.|

## <a name="remarks"></a>Hinweise

Zum Auflisten von Elementen, die für die Wiederherstellung aus einer bestimmten Sicherung verfügbar sind, verwenden **Sie Wbadmin Get Items**.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der verfügbaren Sicherungen anzuzeigen, die auf Volume h gespeichert sind:
```
wbadmin get versions -backupTarget:h:
```
Wenn Sie eine Liste der verfügbaren Sicherungen anzeigen möchten, die im freigegebenen Remote Ordner \\ \\ servername\share für den Computer Server01 gespeichert sind, geben Sie Folgendes ein:
```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   Cmdlet " [Get-wbbackuptarget](/powershell/module/windowserverbackup/?view=winserver2012r2-ps) "
