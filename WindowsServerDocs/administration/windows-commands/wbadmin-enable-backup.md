---
title: wbadmin enable backup
description: Referenz Artikel für den Wbadmin-Befehl "Sicherung aktivieren", mit dem ein täglicher Sicherungs Zeitplan erstellt und aktiviert oder ein vorhandener Sicherungs Zeitplan geändert wird.
ms.topic: reference
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3135df39135a1d085509bdbdabdfa7f88817c3be
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156062"
---
# <a name="wbadmin-enable-backup"></a>wbadmin enable backup

Erstellt und aktiviert einen täglichen Sicherungs Zeitplan oder ändert einen vorhandenen Sicherungs Zeitplan. Wenn keine Parameter angegeben sind, werden die aktuell geplanten Sicherungs Einstellungen angezeigt.

Zum Konfigurieren oder Ändern eines täglichen Sicherungs Zeitplans mithilfe dieses Befehls müssen Sie Mitglied der Gruppe "Sicherungs- **Operatoren** " oder der Gruppe " **Administratoren** " sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

Um den datenträgerbezeichnerwert für Ihre Datenträger anzuzeigen, führen Sie den Befehl [Wbadmin Get Disks](wbadmin-get-disks.md) aus.

## <a name="syntax"></a>Syntax

```
wbadmin enable backup [-addtarget:<BackupTarget>] [-removetarget:<BackupTarget>] [-schedule:<TimeToRunBackup>] [-include:<VolumesToInclude>] [-nonRecurseInclude:<ItemsToInclude>] [-exclude:<ItemsToExclude>] [-nonRecurseExclude:<ItemsToExclude>][-systemState] [-hyperv:<HyperVComponentsToExclude>] [-allCritical] [-systemState] [-vssFull | -vssCopy] [-user:<UserName>] [-password:<Password>] [-allowDeleteOldBackups]  [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -addTarget | Gibt den Speicherort für Sicherungen an. Erfordert die Angabe des Speicher Orts als Datenträger, Volume oder Universal Naming Convention Pfad (UNC-Pfad) zu einem freigegebenen Remote Ordner ( `\\<servername>\<sharename>` ). Standardmäßig wird die Sicherung unter: gespeichert `\\<servername>\<sharename> WindowsImageBackup <ComputerBackedUp>` . Wenn Sie einen Datenträger angeben, wird der Datenträger vor der Verwendung formatiert, und alle vorhandenen Daten werden dauerhaft gelöscht. Wenn Sie einen freigegebenen Ordner angeben, können Sie keine weiteren Speicherorte hinzufügen. Sie können jeweils nur einen freigegebenen Ordner als Speicherort angeben.<p>**Wichtig:** Wenn Sie eine Sicherung in einem freigegebenen Remote Ordner speichern, wird diese Sicherung überschrieben, wenn Sie denselben Ordner zum erneuten sichern desselben Computers verwenden. Wenn der Sicherungs Vorgang fehlschlägt, können Sie darüber hinaus über eine Sicherung verfügen, da die ältere Sicherung überschrieben wird, aber die neuere Sicherung nicht verwendbar ist. Sie können dies vermeiden, indem Sie Unterordner im freigegebenen Remote Ordner erstellen, um die Sicherungen zu organisieren. Wenn Sie dies tun, benötigen die Unterordner den doppelten Speicherplatz des übergeordneten Ordners.<p>Nur ein Speicherort kann in einem einzelnen Befehl angegeben werden. Mehrere Speicherorte für Volumes und Datenträger Sicherungen können hinzugefügt werden, indem der Befehl erneut ausgeführt wird. |
| -removetarget | Gibt den Speicherort an, den Sie aus dem vorhandenen Sicherungs Zeitplan entfernen möchten. Erfordert die Angabe des Speicher Orts als Datenträger Bezeichner. |
| -Zeitplan | Gibt die Tageszeiten zum Erstellen einer Sicherung an, die als hh: mm formatiert und durch Kommas getrennt formatiert sind. |
| -include | Gibt die durch Kommas getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) enden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. |
| -nonRecurseInclude | Gibt die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) enden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird. |
| -ausschließen | Gibt die durch Trennzeichen getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) enden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. |
| -nonrecurabexclude | Gibt die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) enden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. |
| -HyperV | Gibt die durch Trennzeichen getrennte Liste der Komponenten an, die in die Sicherung eingeschlossen werden sollen. Der Bezeichner kann ein Komponenten Name oder eine Komponenten-GUID sein (mit oder ohne geschweifte Klammern). |
| -SystemState | Erstellt eine Sicherung, die den Systemstatus zusätzlich zu allen anderen Elementen enthält, die Sie mit dem **-include-** Parameter angegeben haben. Der Systemstatus enthält Startdateien (Boot.ini, ndtldr, NTDetect.com), die Windows-Registrierung einschließlich com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmelde Skripts), die Active Directory und NTDS. DIT auf Domänen Controllern und im Zertifikat Speicher, wenn der Zertifikat Dienst installiert ist. Wenn die Webserver Rolle auf dem Server installiert ist, wird das IIS-Metaverzeichnis eingeschlossen. Wenn der Serverteil eines Clusters ist, werden Clusterdienst Informationen ebenfalls eingeschlossen. |
| -allcritical | Gibt an, dass alle wichtigen Volumes (Volumes, die den Zustand des Betriebssystems enthalten) in den Sicherungen enthalten sein sollen. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für die vollständige System-oder Systemstatus Wiederherstellung erstellen. Sie sollte nur verwendet werden, wenn " **-backupTarget** " angegeben wird. Andernfalls schlägt der Befehl fehl. Kann mit der Option **-include** verwendet werden.<p>**Tipp:** Das Zielvolume für eine Sicherung mit einem kritischen Volume kann ein lokales Laufwerk sein, aber es darf keines der Volumes sein, die in der Sicherung enthalten sind. |
| -vssfull | Führt eine vollständige Sicherungskopie mithilfe des Volumeschattenkopie-Dienst (VSS) aus. Alle Dateien werden gesichert, der Verlauf jeder Datei wird aktualisiert, um widerzuspiegeln, dass Sie gesichert wurde, und die Protokolle vorheriger Sicherungen werden möglicherweise abgeschnitten. Wenn dieser Parameter nicht verwendet wird, erstellt der Befehl [Wbadmin start Backup](wbadmin-start-backup.md) eine Kopier Sicherung, aber der Verlauf der zu sichernden Dateien wird nicht aktualisiert.<p>**Vorsicht:** Verwenden Sie diesen Parameter nicht, wenn Sie ein anderes Produkt als Windows Server-Sicherung zum Sichern von Apps verwenden, die sich auf den Volumes befinden, die in der aktuellen Sicherung enthalten sind. Dadurch kann der inkrementelle, differenzielle oder andere Sicherungstyp, den das andere Sicherungs Produkt erstellt, möglicherweise nicht mehr ausgeführt werden, da der Verlauf, auf den Sie sich verlassen, bestimmt, wie viele Daten gesichert werden können, und Sie können unnötig eine vollständige Sicherung durchführen. |
| -vsscopy | Führt eine Kopier Sicherung mithilfe von VSS aus. Alle Dateien werden gesichert, aber der Verlauf der Dateien, die gesichert werden, wird nicht aktualisiert, sodass Sie alle Informationen darüber erhalten, wo die Dateien geändert, gelöscht usw. sowie beliebige Anwendungsprotokoll Dateien. Die Verwendung dieser Art von Sicherung wirkt sich nicht auf die Sequenz von inkrementellen und differenziellen Sicherungen aus, die unabhängig von dieser Kopier Sicherung auftreten können. Dies ist der Standardwert.<p>**Warnung:** Sicherungskopien können nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden. |
| -Benutzer | Gibt den Benutzer an, der über die Schreib Berechtigung für das Sicherungs Speicher Ziel verfügt (wenn es sich um einen freigegebenen Remote Ordner handelt). Der Benutzer muss Mitglied der Gruppe " **Administratoren** " oder " **Sicherungs-Operatoren** " auf dem Computer sein, der gesichert wird. |
| -password | Gibt das Kennwort für den Benutzernamen an, der vom Parameter **-User**bereitgestellt wird. |
| -allowdeleteoldbackups | Überschreibt alle Sicherungen, die vor dem Upgrade des Computers durchgeführt wurden. |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

## <a name="examples"></a>Beispiele

So planen Sie tägliche Sicherungen um 9:00 Uhr und 6:00 Uhr für die Festplattenlaufwerke E:, d:\mountpoint und und `\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\` speichern die Dateien auf dem Datenträger mit dem Namen DiskId, indem Sie Folgendes eingeben:

```
wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:E:,D:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```

Um tägliche Sicherungen des Ordners "d:\Documents" um 12:00 Uhr und 7:00 Uhr am Netzwerkort zu planen `\\backupshare\backup1` , geben Sie unter Verwendung der Netzwerk Anmelde Informationen für den **Sicherungs Operator**, aarekelund (aekel), das Kennwort für das Kennwort *$3hm9 ^ 5LP* und das Mitglied der Domäne contosoeast an, das zum Authentifizieren des Zugriffs

```
wbadmin enable backup –addtarget:\\backupshare\backup1 –include: D:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
```

Geben Sie Folgendes ein, um tägliche Sicherungen von Volume T: und dem Ordner "d:\Documents" um 1:00 Uhr zu Laufwerk H:, ohne den Ordner `d:\documents\~tmp` und Durchführung einer vollständigen Sicherung mithilfe des Volumeschattenkopie-Dienst zu planen:

```
wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)

- [Wbadmin-Befehl zum Aktivieren der Sicherung](wbadmin-enable-backup.md)

- [Befehl zum Starten der Wbadmin-Sicherung](wbadmin-start-backup.md)

- [Befehl "Get Disks" in Wbadmin](wbadmin-get-disks.md)
