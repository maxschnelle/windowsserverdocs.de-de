---
title: wbadmin start recovery
description: Referenz Artikel für den Befehl Wbadmin Start Recovery, der einen Wiederherstellungs Vorgang basierend auf den von Ihnen angegebenen Parametern ausführt.
ms.topic: reference
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 408ccadd830e50e9b51447cc19f7243d349cb3ef
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524755"
---
# <a name="wbadmin-start-recovery"></a>wbadmin start recovery

Führt einen Wiederherstellungs Vorgang basierend auf den Parametern aus, die Sie angeben.

Zum Ausführen einer Wiederherstellung mithilfe dieses Befehls müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```
wbadmin start recovery -version:<VersionIdentifier> -items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>} -itemtype:{Volume | App | File} [-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}] [-machine:<BackupMachineName>] [-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}] [-recursive] [-overwrite:{Overwrite | CreateCopy | Skip}] [-notRestoreAcl] [-skipBadClusterCheck] [-noRollForward] [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -version | Gibt den Versions Bezeichner der wiederherzustellenden Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, führen Sie den [Befehl Wbadmin Get Versions](wbadmin-get-versions.md)aus. |
| -Elemente | Gibt eine durch Trennzeichen getrennte Liste von Volumes, apps, Dateien oder Ordnern an, die wieder hergestellt werden sollen. Sie müssen diesen Parameter mit dem **-ItemType-** Parameter verwenden. |
| -ItemType | Gibt den Typ der wiederherzustellenden Elemente an. Muss ein **Volume**, eine **App**oder eine **Datei**sein. Wenn " **-ItemType** " ein *Volume*ist, können Sie nur ein einzelnes Volume angeben, indem Sie den volumedatenträger, den volumeeinstellungspunkt oder den GUID-basierten Volumenamen angeben. Wenn " **-ItemType** " eine *App*ist, können Sie nur eine einzelne Anwendung angeben. Sie können auch den Wert " **adifm** " verwenden, um eine Installation von Active Directory wiederherzustellen. Damit die APP wieder hergestellt werden kann, muss Sie bei Windows Server-Sicherung registriert sein. Wenn **ItemType** den Wert *File*hat, können Sie Dateien oder Ordner angeben, die jedoch Teil desselben Volumes sind und sich im selben übergeordneten Ordner befinden. |
| -backupTarget | Gibt den Speicherort an, der die Sicherung enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn sich der Standort von dem Speicherort unterscheidet, in dem die Sicherungen dieses Computers normalerweise gespeichert werden. |
| -Computer | Gibt den Namen des Computers an, für den Sie die Sicherung wiederherstellen möchten. Dieser Parameter muss verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird. Der Parameter " **-Machine** " ist nützlich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. |
| -wiederherstellungziel | Gibt den Speicherort für die Wiederherstellung an. Dieser Parameter ist hilfreich, wenn sich dieser Speicherort von dem Speicherort unterscheidet, der zuvor gesichert wurde. Sie kann auch für die Wiederherstellung von Volumes, Dateien oder Apps verwendet werden. Wenn Sie ein Volume wiederherstellen, können Sie den volumelaufwerks Buchstaben des alternativen Volumes angeben. Wenn Sie eine Datei oder eine App wiederherstellen, können Sie einen alternativen Wiederherstellungs Speicherort angeben. |
| -rekursiv | Nur beim Wiederherstellen von Dateien gültig. Stellt die Dateien in den Ordnern und alle Dateien wieder her, die den angegebenen Ordnern untergeordnet sind. Standardmäßig werden nur Dateien, die sich direkt in den angegebenen Ordnern befinden, wieder hergestellt. |
|-Überschreiben | Nur beim Wiederherstellen von Dateien gültig. Gibt die Aktion an, die ausgeführt werden soll, wenn eine wieder herzustellende Datei bereits am gleichen Speicherort vorhanden ist. Die gültigen Optionen sind:<ul><li>**Skip** : bewirkt, dass Windows Server-Sicherung die vorhandene Datei auslassen und die Wiederherstellung der nächsten Datei fortsetzen.</li><li>" **Kreatecopy** ": bewirkt, dass Windows Server-Sicherung eine Kopie der vorhandenen Datei erstellt, sodass die vorhandene Datei nicht geändert wird.</li><li>Über **Schreiben** : bewirkt, dass Windows Server-Sicherung die vorhandene Datei mit der Datei aus der Sicherung überschreibt. |
| -notrestoreacl | Nur beim Wiederherstellen von Dateien gültig. Gibt an, dass die Sicherheits-Zugriffs Steuerungs Listen (ACLs) der Dateien, die aus der Sicherung wieder hergestellt werden, nicht wieder hergestellt werden. Standardmäßig werden die Sicherheits-ACLs wieder hergestellt (der Standardwert ist **true**). Wenn dieser Parameter verwendet wird, werden die ACLs für die wiederhergestellten Dateien von dem Speicherort geerbt, an dem die Dateien wieder hergestellt werden. |
| -skipbadclustercheck | Nur beim Wiederherstellen von Volumes gültig. Überspringt die Überprüfung der wiederherzustellenden Datenträger auf fehlerhafte Cluster Informationen. Wenn Sie die Wiederherstellung auf einem anderen Server oder auf einer anderen Hardware durchführen, wird empfohlen, diesen Parameter nicht zu verwenden. Sie können den Befehl **chkdsk/b** auf diesen Datenträgern jederzeit manuell ausführen, um Sie auf fehlerhafte Cluster zu überprüfen, und dann die Dateisystem Informationen entsprechend aktualisieren.<p>**Wichtig:** Bis zum Ausführen von **chkdsk/b**sind die in Ihrem wiederhergestellten System gemeldeten fehlerhaften Cluster möglicherweise nicht korrekt. |
| -norollforward | Nur beim Wiederherstellen von apps gültig. Ermöglicht die vorherige Wiederherstellung einer APP zu einem bestimmten Zeitpunkt, wenn Sie die neueste Version aus den Sicherungen auswählen. Die vorherige Wiederherstellung bis zu einem bestimmten Zeitpunkt wird als Standardeinstellung für alle anderen nicht aktuellen Versionen der app ausgeführt. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

#### <a name="remarks"></a>Bemerkungen

- Zum Anzeigen einer Liste von Elementen, die für die Wiederherstellung nach einer bestimmten Sicherungs Version verfügbar sind, führen [Sie den Befehl Wbadmin Get Items](wbadmin-get-items.md)aus. Wenn ein Volume zum Zeitpunkt der Sicherung keinen Einfügepunkt oder Laufwerk Buchstabe enthielt, gibt dieser Befehl einen GUID-basierten Volumenamen zurück, der zum Wiederherstellen des Volumes verwendet werden soll.

- Wenn Sie den Wert " **adifm** " verwenden, um eine Installation von einem Medien Vorgang auszuführen, um die zugehörigen Daten wiederherzustellen, die für Active Directory Domain Services erforderlich sind, erstellt **adifm** eine Kopie der Active Directory Datenbank-, Registrierungs-und SYSVOL-Status und speichert diese Informationen dann an dem Speicherort, der von **-Wiederherstellungsziel**angegeben wird. Verwenden Sie diesen Parameter nur, wenn " **-herstellytarget** " angegeben wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung ab dem 31. März 2020 (um 9:00 Uhr) von Volume d: durchzuführen:

```
wbadmin start recovery -version:03/31/2020-09:00 -itemType:Volume -items:d:
```

Geben Sie Folgendes ein, um eine Wiederherstellung auf Laufwerk d der Sicherung ab dem 31. März 2020 (9:00 Uhr) der Registrierung auszuführen:

```
wbadmin start recovery -version:03/31/2020-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```

Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung vom 31. März 2020 (um 9:00 Uhr) der Ordner "d:\folder" und der untergeordneten Ordner "d:\folder" durchzuführen:

```
wbadmin start recovery -version:03/31/2020-09:00 -itemType:File -items:d:\folder -recursive
```

Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung ab dem 31. März 2020 (9:00 Uhr) des Volumes auszuführen `\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\` :

```
wbadmin start recovery -version:03/31/2020-09:00 -itemType:Volume -items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```

Geben Sie Folgendes ein, um eine Wiederherstellung der Sicherung ab dem 30. April 2020 (um 9:00 Uhr) des freigegebenen Ordners `\\servername\share` aus Server01 durchzuführen:

```
wbadmin start recovery -version:04/30/2020-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Start-wbfilerecovery](/powershell/module/windowserverbackup/Start-WBFileRecovery)

- [Start-wbhypervrecovery](/powershell/module/windowserverbackup/Start-WBHyperVRecovery)

- [Start-wbsystemstatus](/powershell/module/windowserverbackup/Start-WBSystemStateRecovery)

- [Start-wbvolumerecovery](/powershell/module/windowserverbackup/Start-WBVolumeRecovery)
