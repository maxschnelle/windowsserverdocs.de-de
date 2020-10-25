---
title: wbadmin start systemstaterecovery
description: Referenz Artikel für den Wbadmin start systemstaterecovery-Befehl, der eine Systemstatus Wiederherstellung an einem Speicherort und von einer von Ihnen angegebenen Sicherung ausführt.
ms.topic: reference
ms.assetid: 208b1be9-3452-4aba-bb49-46bc587fca96
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b52b4fedf14eb2d4caab4e9d521767ff9e89365a
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524715"
---
# <a name="wbadmin-start-systemstaterecovery"></a>wbadmin start systemstaterecovery

Führt eine Wiederherstellung des Systemstatus an einem Speicherort und von einer von Ihnen angegebenen Sicherung aus.

Wenn Sie mit diesem Befehl eine Systemstatus Wiederherstellung durchführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

> [!NOTE]
> Windows Server-Sicherung im Rahmen der Sicherung oder Wiederherstellung des Systemstatus die registrierungsbenutzer Strukturen (HKEY_CURRENT_USER) nicht sichern oder wiederherstellen.

## <a name="syntax"></a>Syntax

```
wbadmin start systemstaterecovery -version:<VersionIdentifier> -showsummary [-backupTarget:{<BackupDestinationVolume> | <NetworkSharePath>}]
[-machine:<BackupMachineName>] [-recoveryTarget:<TargetPathForRecovery>] [-authsysvol] [-autoReboot] [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -version | Gibt den Versions Bezeichner der wiederherzustellenden Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, führen Sie den [Befehl Wbadmin Get Versions](wbadmin-get-versions.md)aus. |
| -ShowSummary | Meldet die Zusammenfassung der letzten Wiederherstellung des Systemstatus (nach dem Neustart, der zum Abschließen des Vorgangs erforderlich ist). Dieser Parameter darf nicht von anderen Parametern begleitet werden. |
| -backupTarget | Gibt den Speicherort mit den Sicherungen an, die Sie wiederherstellen möchten. Dieser Parameter ist nützlich, wenn sich der Speicherort vom Speicherort unterscheidet, in dem die Sicherungen normalerweise gespeichert werden |
| -Computer | Gibt den Namen des Computers an, für den die Sicherung wieder hergestellt werden soll. Dieser Parameter muss verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird. Der Parameter " **-Machine** " ist nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. |
| -wiederherstellungziel | Gibt an, in welchem Verzeichnis wieder hergestellt werden soll. Dieser Parameter ist hilfreich, wenn die Sicherung an einem alternativen Speicherort wieder hergestellt wird. |
| -authsysvol | Führt eine autorisierende Wiederherstellung des freigegebenen Verzeichnisses des System Volume (SYSVOL) aus. |
| -AutoReboot | Gibt an, dass das System am Ende des Wiederherstellungs Vorgangs für den Systemstatus neu gestartet werden soll. Dieser Parameter ist nur für eine Wiederherstellung am ursprünglichen Speicherort gültig. Wir empfehlen Ihnen nicht, diesen Parameter zu verwenden, wenn Sie nach dem Wiederherstellungs Vorgang Schritte ausführen müssen. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Wiederherstellung des Systemstatus der Sicherung von 03/31/2020 um 9:00 Uhr zu starten:

```
wbadmin start systemstaterecovery -version:03/31/2020-09:00
```

So starten Sie eine Wiederherstellung des Systemstatus der Sicherung von 04/30/2020 um 9:00 Uhr der in der freigegebenen Ressource für Server01 gespeichert ist, geben Sie Folgendes ein `\\servername\share` :

```
wbadmin start systemstaterecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Start-wbsystemstatus](/powershell/module/windowserverbackup/Start-WBSystemStateRecovery)
