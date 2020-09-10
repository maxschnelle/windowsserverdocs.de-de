---
title: wbadmin enable backup
description: Referenz Artikel für Wbadmin enable Backup, bei dem ein täglicher Sicherungs Zeitplan erstellt und aktiviert oder ein vorhandener Sicherungs Zeitplan geändert wird.
ms.topic: reference
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bcca3c46b4e1314e89626e2ed9c333a2945927bd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640746"
---
# <a name="wbadmin-enable-backup"></a>wbadmin enable backup



Erstellt und aktiviert einen täglichen Sicherungs Zeitplan oder ändert einen vorhandenen Sicherungs Zeitplan. Wenn keine Parameter angegeben sind, werden die aktuell geplanten Sicherungs Einstellungen angezeigt.

Um einen täglichen Sicherungs Zeitplan zu konfigurieren oder zu ändern, müssen Sie Mitglied der Gruppe " **Administratoren** " oder " **Sicherungs-Operatoren** " sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

Syntax für Windows Server 2008:
```
wbadmin enable backup
[-addtarget:<BackupTargetDisk>]
[-removetarget:<BackupTargetDisk>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-allCritical]
[-quiet]
```
Syntax für Windows Server 2008 R2:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-allCritical]
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet]
```
Syntax für Windows Server 2012 und Windows Server 2012 R2:
```
wbadmin enable backup
[-addtarget:<BackupTarget>]
[-removetarget:<BackupTarget>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>][-systemState]
[-hyperv:<HyperVComponentsToExclude>]
[-allCritical]
[-systemState]
[-vssFull | -vssCopy]
[-user:<UserName>]
[-password:<Password>]
[-quiet]
[-allowDeleteOldBackups]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-addTarget|Für Windows Server 2008 gibt den Speicherort für Sicherungen an. Erfordert, dass Sie ein Ziel für Sicherungen als Datenträger Bezeichner angeben (siehe Hinweise). Der Datenträger wird vor der Verwendung formatiert, und alle vorhandenen Daten werden dauerhaft gelöscht.</br>Gibt für Windows Server 2008 R2 und höher den Speicherort für Sicherungen an. Erfordert die Angabe des Speicher Orts als Datenträger, Volume oder Universal Naming Convention Pfad (UNC-Pfad) zu einem freigegebenen Remote Ordner ( \\ \\ \<servername> \<sharename> \) . Standardmäßig wird die Sicherung unter: \\ \\ <servername> \<sharename> \WindowsImageBackup gespeichert.\<ComputerBackedUp>\. Wenn Sie einen Datenträger angeben, wird der Datenträger vor der Verwendung formatiert, und alle vorhandenen Daten werden dauerhaft gelöscht. Wenn Sie einen freigegebenen Ordner angeben, können Sie keine weiteren Speicherorte hinzufügen. Sie können jeweils nur einen freigegebenen Ordner als Speicherort angeben.</br>Wichtig: Wenn Sie eine Sicherung in einem freigegebenen Remote Ordner speichern, wird diese Sicherung überschrieben, wenn Sie denselben Ordner zum erneuten sichern desselben Computers verwenden. Wenn der Sicherungs Vorgang fehlschlägt, können Sie darüber hinaus keine Sicherung erstellen, da die ältere Sicherung überschrieben wird, aber die neuere Sicherung nicht verwendbar ist. Sie können dies vermeiden, indem Sie Unterordner im freigegebenen Remote Ordner erstellen, um die Sicherungen zu organisieren. Wenn Sie dies tun, benötigen die Unterordner den doppelten Speicherplatz des übergeordneten Ordners.</br>Nur ein Speicherort kann in einem einzelnen Befehl angegeben werden. Mehrere Speicherorte für Volumes und Datenträger Sicherungen können hinzugefügt werden, indem der Befehl erneut ausgeführt wird.|
|-removetarget|Gibt den Speicherort an, den Sie aus dem vorhandenen Sicherungs Zeitplan entfernen möchten. Erfordert die Angabe des Speicher Orts als Datenträger Bezeichner (siehe Hinweise).|
|-Zeitplan|Gibt die Tageszeiten zum Erstellen einer Sicherung an, die als hh: mm formatiert und durch Kommas getrennt formatiert sind.|
|-include|Für Windows Server 2008 gibt die durch Trennzeichen getrennte Liste der volumelaufwerks Buchstaben, Volumebereitstellungspunkte oder GUID-basierten Volumenamen an, die in die Sicherung eingeschlossen werden sollen.</br>Für Windows Server 2008 R2and gibt später die durch Trennzeichen getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich () beendet werden \) . Wenn Sie einen Pfad zu einer Datei angeben, können Sie im Dateinamen das Platzhalter Zeichen (*) verwenden.|
|-nonRecurseInclude|Gibt für Windows Server 2008 R2 und höher die nicht rekursive, durch Kommas getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich () beendet werden \) . Wenn Sie einen Pfad zu einer Datei angeben, können Sie im Dateinamen das Platzhalter Zeichen (*) verwenden. Sollte nur verwendet werden, wenn der-backupTarget-Parameter verwendet wird.|
|-ausschließen|Gibt für Windows Server 2008 R2 und höher die durch Trennzeichen getrennte Liste der Elemente an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich () beendet werden \) . Wenn Sie einen Pfad zu einer Datei angeben, können Sie im Dateinamen das Platzhalter Zeichen (*) verwenden.|
|-nonrecurabexclude|Gibt für Windows Server 2008 R2 und höher die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich () beendet werden \) . Wenn Sie einen Pfad zu einer Datei angeben, können Sie im Dateinamen das Platzhalter Zeichen (*) verwenden.|
|-HyperV|Gibt die durch Trennzeichen getrennte Liste der Komponenten an, die in die Sicherung eingeschlossen werden sollen. Der Bezeichner kann ein Komponenten Name oder eine Komponenten-GUID sein (mit oder ohne geschweifte Klammern).|
|-SystemState|Für Windows 7 und Windows Server 2008 R2 und höher erstellt eine Sicherung, die zusätzlich zu allen anderen Elementen, die Sie mit dem Parameter " **-include** " angegeben haben, auch den Systemstatus enthält. Der Systemstatus enthält Startdateien (Boot.ini, ndtldr, NTDetect.com), die Windows-Registrierung einschließlich com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmelde Skripts), die Active Directory und NTDS. DIT auf Domänen Controllern und im Zertifikat Speicher, wenn der Zertifikat Dienst installiert ist. Wenn die Webserver Rolle auf dem Server installiert ist, wird das IIS-Metaverzeichnis eingeschlossen. Wenn der Serverteil eines Clusters ist, werden Clusterdienst Informationen ebenfalls eingeschlossen.|
|-allcritical|Gibt an, dass alle wichtigen Volumes (Volumes, die den Zustand des Betriebssystems enthalten) in den Sicherungen enthalten sein sollen. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für die vollständige System-oder Systemstatus Wiederherstellung erstellen. Sie sollte nur verwendet werden, wenn "-backupTarget" angegeben wird, da andernfalls der Befehl fehlschlägt. Kann mit der Option **-include** verwendet werden.</br>Tipp: das Ziel Volume für eine Sicherung mit einem kritischen Volume kann ein lokales Laufwerk sein, aber es darf keines der Volumes sein, die in der Sicherung enthalten sind.|
|-vssfull|Für Windows Server 2008 R2 und höher führt eine vollständige Sicherungskopie mithilfe des Volumeschattenkopie-Dienst (VSS) aus. Alle Dateien werden gesichert, der Verlauf jeder Datei wird aktualisiert, um widerzuspiegeln, dass Sie gesichert wurde, und die Protokolle vorheriger Sicherungen werden möglicherweise abgeschnitten. Wenn dieser Parameter nicht verwendet wird, wird bei der Start Sicherung von Wbadmin eine Kopier Sicherung durchgeführt, aber der Verlauf der zu sichernden Dateien wird nicht aktualisiert.</br>Vorsicht: Verwenden Sie diesen Parameter nicht, wenn Sie ein anderes Produkt als Windows Server-Sicherung zum Sichern von Anwendungen verwenden, die sich auf den Volumes befinden, die in der aktuellen Sicherung enthalten sind. Dadurch kann der inkrementelle, differenzielle oder andere Sicherungstyp, den das andere Sicherungs Produkt erstellt, möglicherweise nicht mehr ausgeführt werden, da der Verlauf, auf den Sie sich verlassen, bestimmt, wie viele Daten gesichert werden können, und Sie können unnötig eine vollständige Sicherung durchführen.|
|-vsscopy|Für Windows Server 2008 R2 und höher wird eine Kopiesicherung mithilfe von VSS durchführt. Alle Dateien werden gesichert, aber der Verlauf der Dateien, die gesichert werden, wird nicht aktualisiert, sodass Sie alle Informationen darüber erhalten, wo die Dateien geändert, gelöscht usw. sowie beliebige Anwendungsprotokoll Dateien. Die Verwendung dieser Art von Sicherung wirkt sich nicht auf die Sequenz von inkrementellen und differenziellen Sicherungen aus, die unabhängig von dieser Kopier Sicherung auftreten können. Dies ist der Standardwert.</br>Warnung: eine Kopier Sicherung kann nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden.|
|-Benutzer|Gibt für Windows Server 2008 R2 und höher den Benutzer mit Schreib Berechtigung für das Sicherungs Speicher Ziel an (wenn es sich um einen freigegebenen Remote Ordner handelt). Der Benutzer muss Mitglied der Gruppe "Administratoren" oder der Gruppe "Sicherungs-Operatoren" auf dem Computer sein, der gesichert wird.|
|-password|Gibt für Windows Server 2008 R2 und höher das Kennwort für den Benutzernamen an, der vom Parameter-User bereitgestellt wird.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|
|-allowdeleteoldbackups|Überschreibt alle Sicherungen, die vor dem Upgrade des Computers durchgeführt wurden.|

## <a name="remarks"></a>Hinweise

Um den datenträgerbezeichnerwert für Ihre Datenträger anzuzeigen, geben **Sie Wbadmin Get Disks**ein.

## <a name="examples"></a>Beispiele

In den folgenden Beispielen wird veranschaulicht, wie der Befehl **Wbadmin enable Backup** in verschiedenen sicherungsszenarien verwendet werden kann:

Szenario #1
- Planen der Sicherungen von Festplatten Laufwerken e:, d:\mountpoint und \\ \\ ? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
- Speichern Sie die Dateien auf dem Datenträger DiskId.
- Täglich um 9:00 Uhr täglich Sicherungen ausführen und 18:00 Uhr
  ```
  wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  Szenario #2
- Planen Sie Sicherungen des Ordners "d:\Documents" für den Netzwerk Speicherort " \\ \\ backupshare\backup1".
- Verwenden Sie die Netzwerk Anmelde Informationen für den Sicherungs Administrator Aaren Ekelund (aekel), der Mitglied der Domäne contosoeast ist, um den Zugriff auf die Netzwerkfreigabe zu authentifizieren. Das Kennwort von Aaren ist *$3hm9 ^ 5LP*.
- Täglich um 12:00 Uhr täglich Sicherungen ausführen und 7:00 Uhr
  ```
  wbadmin enable backup –addtarget:\\backupshare\backup1 –include: d:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
  ```
  Szenario #3
- Planen Sie Sicherungen von Volume t: und Ordner d:\Dokumente auf Laufwerk h:, aber schließen Sie den Ordner d:\Documents \~ tmp aus.
- Führen Sie eine vollständige Sicherung mithilfe des Volumeschattenkopie-Dienst aus.
- Täglich um 1:00 Uhr täglich Sicherungen ausführen
  ```
  wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
  ```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)