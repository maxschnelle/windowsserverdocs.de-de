---
title: Wbadmin Get-Elemente
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d08ce3-6e06-4260-b264-fc1bde132d09
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeb7c29ff552f968b4785612f626a86baf154ad7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842881"
---
# <a name="wbadmin-get-items"></a>Wbadmin Get-Elemente



Listet die Elemente in einer bestimmten Sicherung enthalten.

Um dieses Unterbefehl verwenden zu können, muss Sie Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin get items
-version:<VersionIdentifier>
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Version|Gibt die Version der Sicherung in MM/TT/JJJJ-hh: mm-Format. Wenn Sie die Informationen zur Version nicht kennen, geben Sie **Wbadmin get Versionen**.|
|-backupTarget|Gibt den Speicherort, der die Sicherungen enthält, für die die Details werden sollen. Verwenden Sie zum Auflisten von Sicherungen, die an dieser Stelle Ziel gespeichert. Zielspeicherorte für Sicherungen können einem lokal angeschlossenen Laufwerk oder einem freigegebenen Remoteordner sein. Wenn **Wbadmin Elemente abrufen**wird ausgeführt, auf dem gleichen Computer, in dem die Sicherung erstellt wurde, wird dieser Parameter nicht benötigt. Allerdings ist dieser Parameter erforderlich, um Informationen über eine Sicherung erstellt wurde, von einem anderen Computer abzurufen.|
|-Computer|Gibt den Namen des Computers, der die Sicherung Details angezeigt werden sollen. Hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn **- BackupTarget** angegeben ist.|

## <a name="BKMK_examples"></a>Beispiele für

Beim Auflisten von Elementen aus der Sicherung, die auf dem 31. März 2013 um 9:00 Uhr, Typ ausgeführt wurde:
```
wbadmin get items -version:03/31/2013-09:00
```
Beim Auflisten von Elementen aus der Sicherung von "SERVER01", die am 30. April 2013 um 9:00 Uhr ausgeführt wurde und auf gespeicherte \\ \\Servername\share, Typ:
```
wbadmin get items -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBackupSet](https://technet.microsoft.com/library/jj902473.aspx) cmdlet