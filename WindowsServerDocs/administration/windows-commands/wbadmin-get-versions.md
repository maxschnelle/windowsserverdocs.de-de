---
title: Wbadmin Get-Versionen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4ebbd0d78de0ffbff1ee8c658d6d9811b87df1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813531"
---
# <a name="wbadmin-get-versions"></a>Wbadmin Get-Versionen



Gibt Einzelheiten über die verfügbaren Sicherungen, die auf dem lokalen Computer oder einem anderen Computer gespeichert sind. Wenn dieses Unterbefehl ohne Parameter verwendet wird, werden der alle Sicherungen des lokalen Computers aufgelistet, auch wenn diese Sicherungen nicht verfügbar sind. Die Angaben für die Sicherung einschließen, die Uhrzeit der Sicherung, Speicherort der Sicherung, die Versions-ID (erforderlich für die **Wbadmin Elemente abrufen** Unterbefehl und Wiederherstellungen auf), und den Typ der Wiederherstellungen durchführen können.

Um Details zu verfügbaren Sicherungen, die mit diesem Unterbefehl zu erhalten, Sie müssen Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde delegiert die entsprechende Berechtigungen. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin get versions
[-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}]
[-machine:BackupMachineName]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-backupTarget|Gibt den Speicherort, der die Sicherungen enthält, denen Sie die Details angezeigt werden sollen. Verwenden Sie zum Auflisten von Sicherungen, die an dieser Stelle Ziel gespeichert. Zielspeicherorte für Sicherungen können lokal angefügten Laufwerken, Volumes, freigegebenen Remoteordner, Wechselmedien wie z. B. DVD-Laufwerke oder andere optischen Medien sein. Wenn **Wbadmin get Versionen** wird ausgeführt, auf dem gleichen Computer, in dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Allerdings ist dieser Parameter erforderlich, um Informationen über eine Sicherung erstellt wurde, von einem anderen Computer abzurufen.|
|-Computer|Gibt den Computer, dem Sie sichern Details angezeigt werden sollen. Wird verwendet, wenn Sie Sicherungen von mehreren Computern am gleichen Speicherort gespeichert werden. Sollte verwendet werden, wenn **- BackupTarget** angegeben ist.|

## <a name="remarks"></a>Hinweise

Verwenden Sie beim Auflisten von Elementen für die Wiederherstellung aus einer bestimmten Sicherung verfügbar, **Wbadmin Elemente abrufen**.

## <a name="BKMK_examples"></a>Beispiele für

Um eine Liste der verfügbaren Sicherungen anzuzeigen, die auf dem Volume h gespeichert sind, geben Sie Folgendes ein:
```
wbadmin get versions -backupTarget:h:
```
Um eine Liste der verfügbaren Sicherungen, die in den freigegebenen Remoteordner gespeichert sind, finden Sie unter \\ \\Servername\share für den Computer "SERVER01", Typ:
```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBackupTarget](https://technet.microsoft.com/library/jj902447.aspx) cmdlet