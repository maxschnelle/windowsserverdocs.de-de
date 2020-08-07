---
title: wbadmin start backup
description: Referenz Artikel für die Wbadmin-Sicherung starten der Sicherung, bei der mithilfe der angegebenen Parameter eine Sicherung erstellt wird.
ms.topic: article
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b8ef64e00f8361a2f006944be65977c3d70769df
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891685"
---
# <a name="wbadmin-start-backup"></a>wbadmin start backup

Erstellt eine Sicherung mithilfe der angegebenen Parameter. Wenn keine Parameter angegeben sind und Sie eine geplante tägliche Sicherung erstellt haben, erstellt dieser Unterbefehl die Sicherung mithilfe der Einstellungen für die geplante Sicherung. Wenn Parameter angegeben werden, wird eine VSS-Kopier Sicherung (Volumeschattenkopie-Dienst) erstellt, und der Verlauf der zu sichernden Dateien wird nicht aktualisiert.

Wenn Sie mit diesem Unterbefehl eine einmalige Sicherung erstellen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen. (Um eine Eingabeaufforderung mit erhöhten Rechten zu öffnen, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung** und dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

Syntax für Windows ° Vista und Windows Server 2008:
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
Syntax für Windows ° 7 und Windows Server 2008 R2 und höher:
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

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|-backupTarget|Gibt den Speicherort für diese Sicherung an. Erfordert einen Festplatten Laufwerksbuchstaben (f:), einen auf einem Volume-GUID basierenden Pfad im Format \\ \\ ? \\ Volume {GUID} oder ein Universal Naming Convention (UNC)-Pfad zu einem freigegebenen Remote Ordner ( \\ \\ \<servername> \\ \<sharename> \\ ). Standardmäßig wird die Sicherung unter: Windows Image Backup gespeichert \\ \\ \<servername> \\ \<sharename> \\ **WindowsImageBackup** \\ \<ComputerBackedUp> \\ .</br>Wichtig: Wenn Sie eine Sicherung in einem freigegebenen Remote Ordner speichern, wird diese Sicherung überschrieben, wenn Sie denselben Ordner zum erneuten sichern desselben Computers verwenden. Wenn der Sicherungs Vorgang fehlschlägt, können Sie darüber hinaus keine Sicherung erstellen, da die ältere Sicherung überschrieben wird, aber die neuere Sicherung nicht verwendbar ist. Sie können dies vermeiden, indem Sie Unterordner im freigegebenen Remote Ordner erstellen, um die Sicherungen zu organisieren. Wenn Sie dies tun, benötigen die Unterordner den doppelten Speicherplatz als übergeordneten Ordner.|
|-include|Gibt für Windows ° Vista und Windows Server 2008 die durch Trennzeichen getrennte Liste der volumelaufwerks Buchstaben, Volumebereitstellungspunkte oder GUID-basierten Volumen Amen an, die in die Sicherung eingeschlossen werden sollen. Dieser Parameter sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird.</br>Für Windows 7 und Windows Server 2008 R2 und höher gibt die durch Trennzeichen getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( \\ ) beendet werden. Sie können das Platzhalter Zeichen ( \* ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird.|
|-ausschließen|Für Windows 7 und Windows Server 2008 R2 und höher gibt die durch Trennzeichen getrennte Liste der Elemente an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( \\ ) beendet werden. Sie können das Platzhalter Zeichen ( \* ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird.|
|-nonRecurseInclude|Gibt für Windows 7 und Windows Server 2008 R2 und höher die nicht rekursive, durch Kommas getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( \\ ) beendet werden. Sie können das Platzhalter Zeichen ( \* ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird.|
|-nonrecurabexclude|Gibt für Windows 7 und Windows Server 2008 R2 und höher die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( \\ ) beendet werden. Sie können das Platzhalter Zeichen ( \* ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Sollte nur verwendet werden, wenn der **-backupTarget-** Parameter verwendet wird.|
|-allcritical|Gibt an, dass alle wichtigen Volumes (Volumes, die den Zustand des Betriebssystems enthalten) in den Sicherungen enthalten sein sollen. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für die Bare-Metal-Recovery erstellen. Sie sollte nur verwendet werden, wenn " **-backupTarget** " angegeben wird, da andernfalls der Befehl fehlschlägt. Kann mit der Option **-include** verwendet werden.</br>Tipp: das Ziel Volume für eine Sicherung mit einem kritischen Volume kann ein lokales Laufwerk sein, aber es darf keines der Volumes sein, die in der Sicherung enthalten sind.|
|-SystemState|Für Windows 7 und Windows Server 2008 R2 und höher erstellt eine Sicherung, die zusätzlich zu allen anderen Elementen, die Sie mit dem Parameter " **-include** " angegeben haben, auch den Systemstatus enthält. Der Systemstatus enthält Startdateien (Boot.ini, ndtldr, NTDetect.com), die Windows-Registrierung einschließlich com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmelde Skripts), die Active Directory und NTDS. DIT auf Domänen Controllern und im Zertifikat Speicher, wenn der Zertifikat Dienst installiert ist. Wenn die Webserver Rolle auf dem Server installiert ist, wird das IIS-Metaverzeichnis eingeschlossen. Wenn der Serverteil eines Clusters ist, werden auch Cluster Dienst Informationen eingeschlossen.|
|-noVerify|Gibt an, dass auf einem Wechselmedium (z. b. einer DVD) gespeicherte Sicherungen nicht auf Fehler überprüft werden. Wenn Sie diesen Parameter nicht verwenden, werden Sicherungen, die auf einem Wechsel Datenträger gespeichert werden, auf Fehler überprüft.|
|-Benutzer|Wenn die Sicherung in einem freigegebenen Remote Ordner gespeichert wird, gibt Sie den Benutzernamen mit der Schreib Berechtigung für den Ordner an.|
|-password|Gibt das Kennwort für den Benutzernamen an, der vom Parameter **-User**bereitgestellt wird.|
|-nogeerbt ACL|Wendet die Zugriffs Steuerungs Listen-Berechtigungen (Access Control List, ACL) für die Anmelde Informationen an, die von den Parametern " **-User** " und " **-Password** " für Windows Image Backup \\ \\ \<servername> \\ \<sharename> \\ \\ \<ComputerBackedUp> \\ (der Ordner mit der Sicherung) bereitgestellt werden. Wenn Sie später auf die Sicherung zugreifen möchten, müssen Sie diese Anmelde Informationen verwenden oder Mitglied der Gruppe "Administratoren" oder der Gruppe "Sicherungs-Operatoren" auf dem Computer mit dem freigegebenen Ordner sein. Wenn **-nogeerbt ACL** nicht verwendet wird, werden die ACL-Berechtigungen aus dem freigegebenen Remote Ordner standardmäßig auf den Ordner angewendet, \\ \<ComputerBackedUp> sodass jeder Benutzer mit Zugriff auf den freigegebenen Remote Ordner auf die Sicherung zugreifen kann.|
|-vssfull|Führt eine vollständige Sicherungskopie mithilfe des Volumeschattenkopie-Dienst (VSS) aus. Alle Dateien werden gesichert, der Verlauf jeder Datei wird aktualisiert, um widerzuspiegeln, dass Sie gesichert wurde, und die Protokolle vorheriger Sicherungen werden möglicherweise abgeschnitten. Wenn dieser Parameter nicht verwendet wird, wird bei der **Start Sicherung von Wbadmin** eine Kopier Sicherung durchgeführt, aber der Verlauf der zu sichernden Dateien wird nicht aktualisiert.</br>Vorsicht: Verwenden Sie diesen Parameter nicht, wenn Sie ein anderes Produkt als Windows Server-Sicherung zum Sichern von Anwendungen verwenden, die sich auf den Volumes befinden, die in der aktuellen Sicherung enthalten sind. Dadurch kann der inkrementelle, differenzielle oder andere Sicherungstyp, den das andere Sicherungs Produkt erstellt, möglicherweise nicht mehr ausgeführt werden, da der Verlauf, auf den Sie sich verlassen, bestimmt, wie viele Daten gesichert werden können, und Sie können unnötig eine vollständige Sicherung durchführen.|
|-vsscopy|Für Windows 7 und Windows Server 2008 R2 und höher wird eine Kopiesicherung mithilfe von VSS durchführt. Alle Dateien werden gesichert, aber der Verlauf der Dateien, die gesichert werden, wird nicht aktualisiert, sodass Sie alle Informationen darüber erhalten, wo die Dateien geändert, gelöscht usw. sowie beliebige Anwendungsprotokoll Dateien. Die Verwendung dieser Art von Sicherung wirkt sich nicht auf die Sequenz von inkrementellen und differenziellen Sicherungen aus, die unabhängig von dieser Kopier Sicherung auftreten können. Dies ist der Standardwert.</br>Warnung: eine Kopier Sicherung kann nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden.|
|-quiet|Führt den Unterbefehl ohne Aufforderungen an den Benutzer aus.|

## <a name="examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie der Befehl **Wbadmin start Backup** in verschiedenen sicherungsszenarien verwendet werden kann:

Szenario #1
- Erstellen Sie eine Sicherungskopie der Volumes e:, d: \\ Mountpoint und \\ \\ ? \\ Volume {cc566d14-4410-11d9-9d93-806e6f6e6963}
- Speichern Sie die Sicherung auf Volume f:
  ```
  wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  Szenario #2
- Führen Sie eine einmalige Sicherung von *f: \\ "Ordner1"* und *h: \\ Folder2* für Volume *d:* aus.
- Sichern des Systemstatus
- Erstellen Sie eine Kopiesicherung, sodass die normalerweise geplante differenzielle Sicherung nicht beeinträchtigt wird.
  ```
  wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
  ```
  Szenario #3
- Führen Sie eine einmalige Sicherung von *d: \\ "Ordner1"* aus, die nicht rekursiv gesichert werden soll.
- Sichern Sie den Ordner im Netzwerk Speicherort * \\ \\ Sicherungs \\ Sicherung 1*
- Beschränken Sie den Zugriff auf die Sicherung auf Mitglieder der Gruppe " **Administratoren** " oder " **Sicherungs-Operatoren** ".
  ```
  wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
  ```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
