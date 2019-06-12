---
title: Sicherung des Wbadmin-aktivieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08a9754b6bb11c50e21ba0d30543761be1866326
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440249"
---
# <a name="wbadmin-enable-backup"></a>Sicherung des Wbadmin-aktivieren



Erstellt und ermöglicht einen täglichen Sicherungszeitplan oder ändert einen vorhandenen Zeitplan für die Sicherung. Ohne Parameter angegeben wird wird die Einstellungen für die aktuell geplanten angezeigt.

Zum Konfigurieren oder einen täglichen Sicherungszeitplan zu ändern, muss Sie entweder Mitglied der **Administratoren** oder **Sicherungs-Operatoren** Gruppe. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

Die Syntax für WindowsServer 2008:
```
wbadmin enable backup
[-addtarget:<BackupTargetDisk>]
[-removetarget:<BackupTargetDisk>]
[-schedule:<TimeToRunBackup>]
[-include:<VolumesToInclude>]
[-allCritical]
[-quiet]
```
Die Syntax für Windows Server 2008 R2:
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
Syntax für WindowsServer 2012 und Windows Server 2012 R2:
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

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-addtarget|Für Windows Server 2008 gibt den Speicherort für Sicherungen. Erfordert, dass Sie als Datenträger-ID an ein Ziel für Sicherungen (siehe Hinweise). Vor der Verwendung der Datenträger formatiert, und alle vorhandenen Daten darauf werden dauerhaft gelöscht.</br>Für Windows Server 2008 R2 und höher gibt den Speicherort für Sicherungen. Erfordert, dass Sie den Speicherort als Datenträger, Volumes oder Universal Naming Convention (UNC)-Pfad zu einem freigegebenen Remoteordner angeben (\\\\\<Servername >\<Sharename >\). Die Sicherung wird standardmäßig unter gespeichert werden: \\ \\ <servername> \<Sharename > \WindowsImageBackup\<ComputerBackedUp >\. Wenn Sie einen Datenträger angeben, vor der Verwendung der Datenträger formatiert, und alle vorhandenen Daten darauf werden dauerhaft gelöscht. Wenn Sie einen freigegebenen Ordner angeben, wird Sie können nicht mehr Speicherorte hinzufügen. Sie können nur einem freigegebenen Ordner als Speicherort zu einem Zeitpunkt angeben.</br>Wichtig: Wenn Sie eine Sicherung auf einem freigegebenen Remoteordner speichern, werden bei Verwendung des gleichen Ordner auf dem gleichen Computer erneut sichern, dass die Sicherung überschrieben. Darüber hinaus, wenn der Sicherungsvorgang fehlerhaft, können es ohne Sicherung kommen, da die ältere Sicherung überschrieben werden, aber die neuere Sicherung nicht verwendet werden. Sie können dies vermeiden, indem Sie Unterordner erstellen, in den freigegebenen Remoteordner zum Organisieren Ihrer Sicherungen. Wenn Sie dies tun, benötigen die Unterordner zweimal auf den Speicherplatz des übergeordneten Ordners.</br>Nur ein Standort kann in einem einzigen Befehl angegeben werden. Mehrere Volumes und Sicherungsspeicher Standorte können hinzugefügt werden, durch den Befehl erneut ausführen.|
|-removetarget|Gibt den Speicherort, den Sie aus dem bestehenden Sicherungszeitplan entfernen möchten. Erfordert, dass Sie den Speicherort an, wie ein Datenträger-ID (siehe Hinweise).|
|-Zeitplan|Gibt an, Uhrzeiten, erstellen Sie eine Sicherung, HH: mm und durch Trennzeichen getrennten Format.|
|-include|Für Windows Server 2008 gibt die durch Trennzeichen getrennte Liste von volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen in die Sicherung eingeschlossen werden sollen.</br>Für Windows Server 2008 R2and gibt höher, die durch Trennzeichen getrennte Liste von Elementen, die in die Sicherung einschließen. Sie können mehrere Dateien, Ordner oder Volumes enthalten. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\). Sie können im Dateinamen das Platzhalterzeichen (*) verwenden, wenn Sie einen Pfad zu einer Datei angeben.|
|-nonRecurseInclude|Für Windows Server 2008 R2 und höher gibt an, die nicht rekursiven, durch Trennzeichen getrennte Liste von Elementen, die in die Sicherung einschließen. Sie können mehrere Dateien, Ordner oder Volumes enthalten. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\). Sie können im Dateinamen das Platzhalterzeichen (*) verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte verwendet werden, nur, wenn der Parameter - BackupTarget verwendet wird.|
|-Ausschließen|Für Windows Server 2008 R2 und höher gibt die durch Trennzeichen getrennte Liste von Elementen, die von der Sicherung ausgeschlossen. Sie können Dateien, Ordner oder Volumes ausschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\). Sie können im Dateinamen das Platzhalterzeichen (*) verwenden, wenn Sie einen Pfad zu einer Datei angeben.|
|-nonRecurseExclude|Für Windows Server 2008 R2 und höher gibt an, die nicht rekursiven, durch Trennzeichen getrennte Liste von Elementen, die von der Sicherung ausgeschlossen. Sie können Dateien, Ordner oder Volumes ausschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\). Sie können im Dateinamen das Platzhalterzeichen (*) verwenden, wenn Sie einen Pfad zu einer Datei angeben.|
|-hyperv|Gibt an, die durch Trennzeichen getrennte Liste von Komponenten in der Sicherung enthalten sein. Der Bezeichner kann es sich um einen Komponentennamen oder Komponenten-GUID (mit oder ohne Klammern) sein.|
|-"SystemState"|Für Windows ° 7 und Windows Server 2008 R2 und höher, erstellt eine Sicherung, die den Systemstatus zusätzlich zu aller anderen Elemente, die Sie angegeben haben enthält, mit der **-umfassen** Parameter. Der Systemstatus enthält Startdateien (Datei "Boot.ini", NDTLDR, NTDetect.com) der Windows-Registrierung, z. B. com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmeldeskripts), die Active Directory und NTDS. Die DIT auf einem Domänencontroller und, wenn der Dienst Zertifikate installiert ist, wird das Zertifikat Store. Wenn Ihr Server die Webserverrolle installiert hat, wird das IIS-Metaverzeichnis eingeschlossen werden. Wenn der Server Teil eines Clusters ist, ist die Cluster-Dienstinformationen ebenfalls enthalten.|
|-allCritical|Gibt an, dass alle wichtigen Volumes (Volumes, die Status des Betriebssystems enthalten) in die Sicherungen einbezogen werden. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für vollständige oder Wiederherstellung des Systemstatus erstellen. Es sollten verwendet werden, wenn - BackupTarget angegeben ist, andernfalls schlägt der Befehl fehl. Kann verwendet werden, mit der **-umfassen** Option.</br>Tipp: Das Zielvolume für eine kritische-Volume-Sicherung kann ein lokales Laufwerk sein, aber es nicht möglich, alle Volumes, die in der Sicherung enthalten sind.|
|-vssFull|Für Windows Server 2008 R2 und höher führt eine vollständige Sichern Sie den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) verwenden. Alle Dateien gesichert werden, jede Dateiverlauf wird aktualisiert, um darauf hinzuweisen, dass sie gesichert wurde, und die Protokolle von vorherigen Sicherungen verkürzt werden. Wenn dieser Parameter nicht verwendet wird Wbadmin Start-Sicherung wird eine Kopie, die Sicherung, der Verlauf der zu sichernden Dateien wird jedoch nicht aktualisiert.</br>Vorsicht: Verwenden Sie diesen Parameter nicht, wenn Sie ein Produkt als Windows Server-Sicherung verwenden, zum Sichern von Anwendungen, die auf den Volumes, die in der aktuellen Sicherung enthalten sind. Dadurch kann also zu schwerwiegenden Fehlern führen die inkrementelle, Differenziell oder andere Art von Sicherungen, die die anderen sicherungsanwendung erstellt wird, da der Verlauf, dem sie verlassen sich auf Sie bestimmen, wie viele Daten für die Sicherung möglicherweise fehlen und sie ggf. eine vollständige ausführen Sicherung unnötig.|
|-vssCopy|Für Windows Server 2008 R2 und höher führt eine kopiesicherung mit VSS. Alle Dateien gesichert werden, aber der Verlauf der Dateien gesichert wird nicht aktualisiert werden, sodass Sie beibehalten werden, die alle Informationen, auf welche Dateien von, geändert, gelöscht, usw., sowie alle Protokolldateien für die Anwendung. Verwenden diese Art der Sicherung wirkt sich nicht auf die Reihenfolge der inkrementellen oder differenziellen Sicherungen aus, die unabhängig von dieser Sicherung kopieren auftreten können. Dies ist der Standardwert.</br>Warnung: Eine kopiesicherung kann nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden.|
|-Benutzer|Für Windows Server 2008 R2 und höher, gibt Sie den Benutzer mit Schreibberechtigungen für das Ziel des Sicherungsspeichers (sofern es sich um einen freigegebenen Remoteordner ist). Der Benutzer muss ein Mitglied der Gruppe "Administratoren" oder die Gruppe "Sicherungsoperatoren" auf dem Computer, der gesichert wird.|
|-Kennwort|Für Windows Server 2008 R2 und höher gibt an, das Kennwort für den Benutzernamen ein, die von diesem Parameter bereitgestellte-Benutzer.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|
|-allowDeleteOldBackups|Überschreibt alle Sicherungen vorgenommen werden, bevor der Computer aktualisiert wurde.|

## <a name="remarks"></a>Hinweise

Geben Sie zum Anzeigen der Datenträger-ID-Wert für Ihre Datenträger **Wbadmin get Datenträger**.

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Beispiele zeigen die **Wbadmin Aktivieren der Sicherung** in verschiedenen backup-Szenarien verwendet werden:

Szenario #1
- Planen von Sicherungen von Festplattenlaufwerken "e:", d:\mountpoint, und \\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
- Speichern Sie die Dateien auf den Datenträger DiskID
- Ausführen von Sicherungen täglich um 9:00 Uhr und 18:00 Uhr
  ```
  wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  Szenario #2
- Planen von Sicherungen von den Ordner d:\documents für den Netzwerkspeicherort \\ \\backupshare\backup1
- Verwenden Sie die Netzwerkanmeldeinformationen für den Sicherungsadministrator Aaren Ekelund (Aekel), ist ein Mitglied der Domäne CONTOSOEAST zum Authentifizieren des Zugriffs auf die Netzwerkfreigabe verfügen. Die Aaren Kennwort ist *$3 hM 9 ^ 5lp*.
- Ausführen von Sicherungen täglich um 12:00 Uhr und 18:00 Uhr
  ```
  wbadmin enable backup –addtarget:\\backupshare\backup1 –include: d:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
  ```
  #3-Szenario
- Planen von Sicherungen der Volume-t "und" Ordner d:\documents auf dem Laufwerk h:, aber schließen Sie den Ordner d:\documents\~Tmp
- Führen Sie eine vollständige Sicherung, die mit dem Volumeschattenkopie-Dienst.
- Ausführen von Sicherungen täglich um 1:00 Uhr
  ```
  wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
  ```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)