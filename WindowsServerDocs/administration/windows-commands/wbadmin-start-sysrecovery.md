---
title: wbadmin start sysrecovery
description: Referenz Artikel für den Befehl "WBADMIN START SYSRECOVERY", der eine Systemwiederherstellung (Bare-Metal-Recovery) mit den angegebenen Parametern ausführt.
ms.topic: reference
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 292c0d6fc42f4fe58dda6a6fbbb6a693b70a8756
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524745"
---
# <a name="wbadmin-start-sysrecovery"></a>wbadmin start sysrecovery

Führt eine Systemwiederherstellung (Bare-Metal-Recovery) mit den angegebenen Parametern aus.

Wenn Sie mit diesem Befehl eine Systemwiederherstellung durchführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein.

> [!IMPORTANT]
> Der Befehl **Wbadmin start sysrecovery** muss in der Windows-Wiederherstellungskonsole ausgeführt werden und ist nicht im standardmäßigen Verwendungs Text für das **Wbadmin** -Tool aufgeführt. Weitere Informationen finden Sie in der [Windows-Wiederherstellungs Umgebung (WinRE)](/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

## <a name="syntax"></a>Syntax

```
wbadmin start sysrecovery -version:<VersionIdentifier> -backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}  [-machine:<BackupMachineName>] [-restoreAllVolumes] [-recreateDisks] [-excludeDisks] [-skipBadClusterCheck] [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -version | Gibt den Versions Bezeichner der wiederherzustellenden Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, führen Sie den [Befehl Wbadmin Get Versions](wbadmin-get-versions.md)aus. |
| -backupTarget | Gibt den Speicherort an, der die Sicherungen enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn sich der Speicherort von dem Speicherort unterscheidet, in dem die Sicherungen dieses Computers normalerweise gespeichert werden. |
| -Computer | Gibt den Namen des Computers an, für den Sie die Sicherung wiederherstellen möchten. Dieser Parameter muss verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird. Der Parameter " **-Machine** " ist nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. |
| -restoreallvolumes | Stellt alle Volumes aus der ausgewählten Sicherung wieder her. Wenn dieser Parameter nicht angegeben wird, werden nur kritische Volumes (Volumes, die den Systemstatus und die Betriebssystemkomponenten enthalten) wieder hergestellt. Dieser Parameter ist hilfreich, wenn Sie während der Systemwiederherstellung nicht kritische Volumes wiederherstellen müssen. |
| -neu erstellte atedisks | Stellt eine Datenträger Konfiguration in dem Zustand wieder her, der beim Erstellen der Sicherung vorhanden war.<p>**Warnung:** Mit diesem Parameter werden alle Daten auf Volumes gelöscht, auf denen Betriebssystemkomponenten gehostet werden. Es können auch Daten aus Datenvolumes gelöscht werden. |
| -excluenddisks | Gilt nur, wenn er mit dem Parameter " **--Neuerstellung** " angegeben wurde und als durch Trennzeichen getrennte Liste von Datenträger Bezeichnerzeichen eingegeben werden muss (wie in der Ausgabe des [Befehls "WBADMIN GET Disks](wbadmin-get-disks.md)" aufgeführt). Ausgeschlossene Datenträger sind nicht partitioniert oder formatiert. Dieser Parameter hilft bei der Beibehaltung von Daten auf Datenträgern, die Sie während des Wiederherstellungs Vorgangs nicht ändern möchten. |
| -skipbadclustercheck | Nur beim Wiederherstellen von Volumes gültig. Überspringt die Überprüfung der wiederherzustellenden Datenträger auf fehlerhafte Cluster Informationen. Wenn Sie die Wiederherstellung auf einem anderen Server oder auf einer anderen Hardware durchführen, wird empfohlen, diesen Parameter nicht zu verwenden. Sie können den Befehl **chkdsk/b** auf diesen Datenträgern jederzeit manuell ausführen, um Sie auf fehlerhafte Cluster zu überprüfen, und dann die Dateisystem Informationen entsprechend aktualisieren.<p>**Wichtig:** Bis zum Ausführen von **chkdsk/b**sind die in Ihrem wiederhergestellten System gemeldeten fehlerhaften Cluster möglicherweise nicht korrekt. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um mit der Wiederherstellung der Informationen aus der Sicherung zu beginnen, die am 31. März, 2020 um 9:00 Uhr, auf Laufwerk d: ausgeführt wurde:

```
wbadmin start sysrecovery -version:03/31/2020-09:00 -backupTarget:d:
```

Geben Sie Folgendes ein, um mit der Wiederherstellung der Informationen aus der Sicherung zu beginnen, die am 2020 30. April um 9:00 Uhr im freigegebenen Ordner `\\servername\share` für Server01 ausgeführt wurde:

```
wbadmin start sysrecovery -version:04/30/2020-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Get-wbbaremetalrecovery](/powershell/module/windowserverbackup/Get-WBBareMetalRecovery)
