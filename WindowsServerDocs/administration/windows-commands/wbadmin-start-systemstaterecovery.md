---
title: wbadmin start systemstaterecovery
description: Referenz Artikel für Wbadmin start systemstaterecovery, der eine Systemstatus Wiederherstellung an einem Speicherort und von einer von Ihnen angegebenen Sicherung ausführt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 208b1be9-3452-4aba-bb49-46bc587fca96
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c433871cb99018d10d064aac2f7a2098e0d42692
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954432"
---
# <a name="wbadmin-start-systemstaterecovery"></a>wbadmin start systemstaterecovery



Führt eine Wiederherstellung des Systemstatus an einem Speicherort und von einer von Ihnen angegebenen Sicherung aus.

> [!NOTE]
> Windows Server-Sicherung dient nicht zum Sichern oder Wiederherstellen von registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) im Rahmen der Sicherung oder Wiederherstellung des Systemstatus.

Wenn Sie mit diesem Unterbefehl eine Systemstatus Wiederherstellung durchführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.)



## <a name="syntax"></a>Syntax

Syntax für Windows Server 2008:
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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-version|Gibt den Versions Bezeichner für die wieder herzustellende Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, geben Sie **Wbadmin Get Versions**ein.|
|-ShowSummary|Gibt die Zusammenfassung der letzten Wiederherstellung des Systemstatus an (nach dem Neustart, der zum Abschluss des Vorgangs erforderlich ist). Dieser Parameter darf nicht von anderen Parametern begleitet werden.|
|-backupTarget|Gibt den Speicherort an, der die Sicherung oder Sicherungen enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn sich der Speicherort von dem Speicherort unterscheidet, in dem die Sicherungen dieses Computers normalerweise gespeichert werden.|
|-Computer|Gibt den Namen des Computers an, den Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird.|
|-wiederherstellungziel|Gibt das Verzeichnis an, in dem wieder hergestellt werden soll. Dieser Parameter ist hilfreich, wenn die Sicherung an einem alternativen Speicherort wieder hergestellt wird.|
|-authsysvol|Bei Verwendung von wird eine autoritative Wiederherstellung von SYSVOL (das freigegebene Verzeichnis des System Volume) durchführt.|
|-AutoReboot|Gibt an, dass das System am Ende des Wiederherstellungs Vorgangs für den Systemstatus neu gestartet werden soll. Dieser Parameter ist nur für eine Wiederherstellung am ursprünglichen Speicherort gültig. Es wird nicht empfohlen, diesen Parameter zu verwenden, wenn Sie nach dem Wiederherstellungs Vorgang Schritte ausführen müssen.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um eine Wiederherstellung des Systemstatus der Sicherung von 03/31/2013 um 9:00 Uhr durchzuführen:
  ```
  wbadmin start systemstaterecovery -version:03/31/2013-09:00
  ```
- So führen Sie eine Wiederherstellung des Systemstatus der Sicherung von 04/30/2013 um 9:00 Uhr aus der auf der freigegebenen Ressource \\ \\ servername\share für Server01 gespeichert ist, geben Sie Folgendes ein:
  ```
  wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
  ```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Start-wbsystemstatus](/previous-versions/windows/it-pro/windows-8.1-and-8/hh825173(v=win.10)) -Cmdlet
