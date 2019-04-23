---
title: Wbadmin Start systemstaterecovery
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 208b1be9-3452-4aba-bb49-46bc587fca96
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c99a934987e320baaec0e56c69f36eda5a32819
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852681"
---
# <a name="wbadmin-start-systemstaterecovery"></a>Wbadmin Start systemstaterecovery



Führt eine Wiederherstellung des Systemstatus an einen Speicherort und aus einer Sicherung, die Sie angeben.

> [!NOTE]
> Windows Server-Sicherung nicht sichern oder Benutzer Registrierungsstrukturen (HKEY_CURRENT_USER) als Teil des Systemstatus-Sicherung oder Wiederherstellung des Systemstatus wiederherstellen.

Um eine Wiederherstellung des Systemstatus, mit diesem Unterbefehl auszuführen, muss Sie Mitglied der **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

Die Syntax für WindowsServer 2008:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-quiet]
```
Syntax für Windows Server 2008 R2 oder höher:
```
wbadmin start systemstaterecovery
-version:<VersionIdentifier>
-showsummary
[-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:<TargetPathForRecovery>]
[-authsysvol]
[-autoReboot]
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Version|Gibt an, die Versions-ID für die Sicherung zum Wiederherstellen in MM/TT/JJJJ-hh: mm-Format. Wenn Sie die Versions-ID nicht kennen, geben Sie **Wbadmin get Versionen**.|
|-showsummary|Meldet der Zusammenfassung der letzten systemstatuswiederherstellung (nach dem Neustart zum Abschließen des Vorgangs erforderlich). Dieser Parameter kann nicht durch alle anderen Parameter ergänzt werden.|
|-backupTarget|Gibt den Speicherort, der enthält die Sicherung oder Sicherungen, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn der Speicherort unterscheidet sich von, wo die Sicherungen dieses Computers in der Regel gespeichert werden.|
|-Computer|Gibt den Namen des Computers ein, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn die **- BackupTarget** Parameter angegeben ist.|
|-recoveryTarget|Gibt das Verzeichnis wiederherstellen. Dieser Parameter ist hilfreich, wenn die Sicherung an einem alternativen Speicherort wiederhergestellt wird.|
|-authsysvol|Wenn verwendet, führt eine autorisierende Wiederherstellung von SYSVOL (das Systemvolume freigegebenen Verzeichnis).|
|-autoReboot|Gibt an, um das System am Ende des Wiederherstellungsvorgangs System Zustand neu zu starten. Dieser Parameter gilt nur für eine Wiederherstellung am ursprünglichen Speicherort. Wir empfehlen nicht, dass Sie diesen Parameter verwenden, wenn Sie Schritte nach dem Recovery-Vorgang ausführen möchten.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="BKMK_examples"></a>Beispiele für

-   Geben Sie Folgendes ein, um eine Wiederherstellung des Systemstatus, der die Sicherung vom 03/31/2013 um 9:00 Uhr auszuführen:  
    ```
    wbadmin start systemstaterecovery -version:03/31/2013-09:00
    ```  
-   Eine Wiederherstellung des Systemstatus, der die Sicherung von 30/04/2013 ausführen, um 9:00 Uhr für die freigegebene Ressource gespeichert wird \\ \\Servername\share für "SERVER01", Typ:  
    ```
    wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
    ```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-WBSystemStateRecovery](https://technet.microsoft.com/library/jj902449.aspx) cmdlet