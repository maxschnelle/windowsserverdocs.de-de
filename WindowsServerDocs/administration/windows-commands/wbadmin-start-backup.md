---
title: Sicherung des Wbadmin-starten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ac602506960b92333750e7a37692c44c92aae22
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440277"
---
# <a name="wbadmin-start-backup"></a>Sicherung des Wbadmin-starten



Erstellt eine Sicherung, die mit angegebenen Parametern. Wenn keine Parameter angegeben werden, und Sie eine geplante tägliche Sicherung erstellt haben, wird dieses Unterbefehl die Sicherung mit den Einstellungen für die geplante Sicherung erstellt. Wenn der Parameter angegeben werden, eine kopiesicherung Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) erstellt und den Verlauf der Dateien, die gesichert werden, werden nicht aktualisiert.

Um eine einmalige Sicherung mit diesem Unterbefehl erstellen zu können, müssen Sie Mitglied werden die **Sicherungs-Operatoren** Gruppe oder der **Administratoren** Gruppe, oder Sie wurde die entsprechenden Berechtigungen delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.)

Beispiele zur Verwendung dieses Unterbefehl finden Sie in [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

Syntax für das Windows ° Vista und WindowsServer 2008:
```
wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<VolumesToInclude>]
[-allCritical]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noinheritAcl]
[-vssFull]
[-quiet]
```
Syntax für das Windows ° 7 und Windows Server 2008 R2 und höher:
```
Wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<ItemsToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>]
[-allCritical]
[-systemState]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noInheritAcl]
[-vssFull | -vssCopy] 
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-backupTarget|Gibt den Speicherort für diese Sicherung an. Erfordert ein Festplattenlaufwerk Buchstabe (f:)), einen Volume-GUID-basierte Pfad im Format \\ \\? \Volume{GUID}, oder ein Universal Naming Convention (UNC)-Pfad zu einem freigegebenen Remoteordner (\\\\\<Servername > \<Sharename >\). Die Sicherung wird standardmäßig unter gespeichert werden: \\ \\ <servername> \<Sharename >\** "WindowsImageBackup" **\\<ComputerBackedUp>\.</br>Wichtig: Wenn Sie eine Sicherung auf einem freigegebenen Remoteordner speichern, werden bei Verwendung des gleichen Ordner auf dem gleichen Computer erneut sichern, dass die Sicherung überschrieben. Darüber hinaus, wenn der Sicherungsvorgang fehlerhaft, können es ohne Sicherung kommen, da die ältere Sicherung überschrieben werden, aber die neuere Sicherung nicht verwendet werden. Sie können dies vermeiden, indem Sie Unterordner erstellen, in den freigegebenen Remoteordner zum Organisieren Ihrer Sicherungen. Wenn Sie dies tun, benötigen die Unterordner zweimal Bereich als den übergeordneten Ordner.|
|-include|Für Windows ° Vista und Windows Server 2008 gibt die durch Trennzeichen getrennte Liste von volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen in die Sicherung eingeschlossen werden sollen. Dieser Parameter sollte verwendet werden nur dann, wenn die **- BackupTarget** Parameter wird verwendet.</br>Für Windows ° 7 und Windows Server 2008 R2 und höher gibt an, die durch Trennzeichen getrennte Liste von Elementen, die in die Sicherung einschließen. Sie können mehrere Dateien, Ordner oder Volumes enthalten. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\\). Sie können das Platzhalterzeichen (\*) in den Dateinamen ein, wenn Sie einen Pfad zu einer Datei angeben. Sollte verwendet werden, nur, wenn die **- BackupTarget** Parameter wird verwendet.|
|-Ausschließen|Für Windows ° 7 und Windows Server 2008 R2 und höher gibt an, die durch Trennzeichen getrennte Liste von Elementen, die von der Sicherung ausgeschlossen. Sie können Dateien, Ordner oder Volumes ausschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\\). Sie können das Platzhalterzeichen (\*) in den Dateinamen ein, wenn Sie einen Pfad zu einer Datei angeben. Sollte verwendet werden, nur, wenn die **- BackupTarget** Parameter wird verwendet.|
|-nonRecurseInclude|Für Windows ° 7 und Windows Server 2008 R2 und höher gibt an, die nicht rekursiven, durch Trennzeichen getrennte Liste von Elementen, die in die Sicherung einschließen. Sie können mehrere Dateien, Ordner oder Volumes enthalten. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\\). Sie können das Platzhalterzeichen (\*) in den Dateinamen ein, wenn Sie einen Pfad zu einer Datei angeben. Sollte verwendet werden, nur, wenn die **- BackupTarget** Parameter wird verwendet.|
|-nonRecurseExclude|Für Windows ° 7 und Windows Server 2008 R2 und höher gibt an, die nicht rekursiven, durch Trennzeichen getrennte Liste von Elementen, die von der Sicherung ausgeschlossen. Sie können Dateien, Ordner oder Volumes ausschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollten sie mit einem umgekehrten Schrägstrich beendet (\\). Sie können das Platzhalterzeichen (\*) in den Dateinamen ein, wenn Sie einen Pfad zu einer Datei angeben. Sollte verwendet werden, nur, wenn die **- BackupTarget** Parameter wird verwendet.|
|-allCritical|Gibt an, dass alle wichtigen Volumes (Volumes, die Status des Betriebssystems enthalten) in die Sicherungen einbezogen werden. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für eine bare-Metal-Recovery erstellen. Er sollte verwendet werden nur, wenn **- BackupTarget** ist angegeben, andernfalls der Befehl schlägt fehl. Kann verwendet werden, mit der **-umfassen** Option.</br>Tipp: Das Zielvolume für eine kritische-Volume-Sicherung kann ein lokales Laufwerk sein, aber es nicht möglich, alle Volumes, die in der Sicherung enthalten sind.|
|-"SystemState"|Für Windows ° 7 und Windows Server 2008 R2 und höher, erstellt eine Sicherung, die den Systemstatus zusätzlich zu aller anderen Elemente, die Sie angegeben haben enthält, mit der **-umfassen** Parameter. Der Systemstatus enthält Startdateien (Datei "Boot.ini", NDTLDR, NTDetect.com) der Windows-Registrierung, z. B. com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmeldeskripts), die Active Directory und NTDS. Die DIT auf einem Domänencontroller und, wenn der Dienst Zertifikate installiert ist, wird das Zertifikat Store. Wenn Ihr Server die Webserverrolle installiert hat, wird das IIS-Metaverzeichnis eingeschlossen werden. Wenn der Server Teil eines Clusters ist, wird der Clusterdienst-Informationen auch enthalten sein.|
|-noVerify|Gibt an, dass Sicherungen auf ein Wechselmedium (z. B. eine DVD) gespeichert, nicht auf Fehler überprüft werden. Wenn Sie diesen Parameter nicht verwenden, werden Sicherungen gespeichert werden, auf ein Wechselmedium auf Fehler überprüft.|
|-Benutzer|Wenn die Sicherung in einem freigegebenen Remoteordner gespeichert wird, gibt den Benutzernamen mit Schreibberechtigung auf den Ordner aus.|
|-Kennwort|Gibt das Kennwort für den Benutzernamen ein, die von den Parameter bereitgestellte **-Benutzer**.|
|-noInheritAcl|Betrifft die Zugriffssteuerungsliste (ACL) Zugriffsberechtigungen, die entsprechen der Anmeldeinformationen der **-Benutzer** und **-Kennwort** Parameter \\ \\ \< Servername >\<Sharename > \WindowsImageBackup\<ComputerBackedUp > \ (im Ordner mit der Sicherung). Für den Zugriff auf die Sicherung müssen Sie später verwenden Sie diese Anmeldeinformationen oder ein Mitglied der Gruppe "Administratoren" oder die Gruppe "Sicherungsoperatoren" auf dem Computer mit den freigegebenen Ordner sein. Wenn **- NoInheritAcl** wird nicht verwendet, die ACL-Berechtigungen aus dem freigegebenen Remoteordner gelten für die \<ComputerBackedUp > Ordner standardmäßig so, dass alle Personen mit Zugriff auf den freigegebenen Remoteordner die Sicherung zugreifen kann.|
|-vssFull|Führt eine vollständige Sicherung, mit dem Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS). Alle Dateien gesichert werden, jede Dateiverlauf wird aktualisiert, um darauf hinzuweisen, dass sie gesichert wurde, und die Protokolle von vorherigen Sicherungen verkürzt werden. Wenn dieser Parameter nicht verwendet wird **Sicherung des Wbadmin-starten** wird eine kopiesicherung, aber den Verlauf der Dateien, die gesichert werden, wird nicht aktualisiert.</br>Vorsicht: Verwenden Sie diesen Parameter nicht, wenn Sie ein Produkt als Windows Server-Sicherung verwenden, zum Sichern von Anwendungen, die auf den Volumes, die in der aktuellen Sicherung enthalten sind. Dadurch kann also zu schwerwiegenden Fehlern führen die inkrementelle, Differenziell oder andere Art von Sicherungen, die die anderen sicherungsanwendung erstellt wird, da der Verlauf, dem sie verlassen sich auf Sie bestimmen, wie viele Daten für die Sicherung möglicherweise fehlen und sie ggf. eine vollständige ausführen Sicherung unnötig.|
|-vssCopy|Für Windows 7 und Windows Server 2008 R2 und höher führt eine kopiesicherung mit VSS. Alle Dateien gesichert werden, aber der Verlauf der Dateien gesichert wird nicht aktualisiert werden, sodass Sie beibehalten werden, die alle Informationen, auf welche Dateien von, geändert, gelöscht, usw., sowie alle Protokolldateien für die Anwendung. Verwenden diese Art der Sicherung wirkt sich nicht auf die Reihenfolge der inkrementellen oder differenziellen Sicherungen aus, die unabhängig von dieser Sicherung kopieren auftreten können. Dies ist der Standardwert.</br>Warnung: Eine kopiesicherung kann nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden.|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Beispiele zeigen die **Sicherung des Wbadmin-starten** in verschiedenen backup-Szenarien verwendet werden:

Szenario #1
- Erstellen Sie eine Sicherung von Volumes "e:", d:\mountpoint, und \\ \\? \Volume{cc566d14-4410-11d9-9d93-806e6f6e6963}
- Speichern Sie die Sicherung auf Volume f:
  ```
  wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  Szenario #2
- Führen Sie eine Einmalsicherung *f:\folder1* und *h:\folder2* Volume *"d:"* .
- Sicherung des Systemstatus
- Stellen Sie eine Sicherung kopieren, damit die Normal geplante differenzielle Sicherung nicht beeinträchtigt wird.
  ```
  wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
  ```
  #3-Szenario
- Führen Sie eine Einmalsicherung *d:\folder1* , sollte gesichert werden nicht rekursiv.
- Sichern Sie den Ordner für den Netzwerkspeicherort  *\\ \\backupshare\backup1*
- Beschränken des Zugriffs auf die Mitglieder der Sicherung der **Administratoren** oder **Sicherungs-Operatoren** Gruppe.
  ```
  wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
  ```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
