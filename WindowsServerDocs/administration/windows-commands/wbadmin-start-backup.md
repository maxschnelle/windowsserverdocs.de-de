---
title: wbadmin start backup
description: Referenz Artikel für den Befehl Wbadmin start Backup, mit dem eine Sicherung mithilfe der angegebenen Parameter erstellt wird.
ms.topic: reference
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a99d467aed8df57660f46b5efbcb4b8df5feb215
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524845"
---
# <a name="wbadmin-start-backup"></a>wbadmin start backup

Erstellt eine Sicherung mithilfe der angegebenen Parameter. Wenn keine Parameter angegeben sind und Sie eine tägliche tägliche Sicherung erstellt haben, erstellt dieser Befehl die Sicherung mithilfe der Einstellungen für die geplante Sicherung. Wenn Parameter angegeben werden, wird eine VSS-Kopier Sicherung (Volumeschattenkopie-Dienst) erstellt, und der Verlauf der zu sichernden Dateien wird nicht aktualisiert.

Zum Erstellen einer einmaligen Sicherung mithilfe dieses Befehls müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein. Außerdem müssen Sie **Wbadmin** über eine Eingabeaufforderung mit erhöhten Rechten ausführen, indem Sie mit der rechten Maustaste auf **Eingabeaufforderung**klicken und dann **als Administrator ausführen**auswählen.

## <a name="syntax"></a>Syntax

```com
wbadmin start backup [-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}] [-include:<ItemsToInclude>] [-nonRecurseInclude:<ItemsToInclude>] [-exclude:<ItemsToExclude>] [-nonRecurseExclude:<ItemsToExclude>] [-allCritical] [-systemState] [-noVerify] [-user:<UserName>] [-password:<Password>] [-noInheritAcl] [-vssFull | -vssCopy] [-quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -backupTarget | Gibt den Speicherort für diese Sicherung an. Erfordert einen Festplatten Laufwerksbuchstaben (f:), einen Volume-GUID-basierten Pfad im Format `\\?\Volume{GUID}` oder einen Universal Naming Convention (UNC)-Pfad zu einem freigegebenen Remote Ordner `(\\<servername>\<sharename>\)` . Standardmäßig wird die Sicherung unter: gespeichert `\\<servername>\<sharename>\WindowsImageBackup\<ComputerBackedUp>\` . |
| -include | Gibt die durch Kommas getrennte Liste der Elemente an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) beendet werden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Der **-include-** Parameter sollte nur in Verbindung mit dem **-backupTarget-** Parameter verwendet werden. |
| -ausschließen | Gibt die durch Trennzeichen getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) beendet werden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Der **-Exclude-** Parameter sollte nur in Verbindung mit dem **-backupTarget-** Parameter verwendet werden. |
| -nonRecurseInclude | Gibt die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die in die Sicherung eingeschlossen werden sollen. Sie können mehrere Dateien, Ordner oder Volumes einschließen. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) beendet werden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Der **-nonRecurseInclude-** Parameter sollte nur in Verbindung mit dem **-backupTarget-** Parameter verwendet werden. |
| -nonrecurabexclude | Gibt die nicht rekursive, durch Kommas getrennte Liste von Elementen an, die von der Sicherung ausgeschlossen werden sollen. Dateien, Ordner oder Volumes können ausgeschlossen werden. Volumepfade können mit Volumelaufwerkbuchstaben, Volumebereitstellungspunkten oder GUID-basierten Volumenamen angegeben werden. Wenn Sie einen GUID-basierten Volumenamen verwenden, sollte er mit einem umgekehrten Schrägstrich ( `\` ) beendet werden. Sie können das Platzhalter Zeichen ( `*` ) im Dateinamen verwenden, wenn Sie einen Pfad zu einer Datei angeben. Der **-nonrecur\exclude-** Parameter sollte nur in Verbindung mit dem **-backupTarget-** Parameter verwendet werden. |
| -allcritical | Gibt an, dass alle wichtigen Volumes (Volumes, die den Zustand des Betriebssystems enthalten) in den Sicherungen enthalten sein sollen. Dieser Parameter ist hilfreich, wenn Sie eine Sicherung für Bare-Metal-Recovery erstellen. Er sollte nur verwendet werden, wenn " **-backupTarget** " angegeben wird, da andernfalls der Befehl fehlschlägt. Kann mit der Option **-include** verwendet werden.<p>**Tipp:** Das Zielvolume für eine Sicherung mit einem kritischen Volume kann ein lokales Laufwerk sein, aber es darf keines der Volumes sein, die in der Sicherung enthalten sind. |
| -SystemState | Erstellt eine Sicherung, die den Systemstatus zusätzlich zu allen anderen Elementen enthält, die Sie mit dem **-include-** Parameter angegeben haben. Der Systemstatus enthält Startdateien (Boot.ini, ndtldr, NTDetect.com), die Windows-Registrierung einschließlich com-Einstellungen, SYSVOL (Gruppenrichtlinien und Anmelde Skripts), die Active Directory und NTDS. DIT auf Domänen Controllern und im Zertifikat Speicher, wenn der Zertifikat Dienst installiert ist. Wenn die Webserver Rolle auf dem Server installiert ist, wird das IIS-Metaverzeichnis eingeschlossen. Wenn der Serverteil eines Clusters ist, werden auch Cluster Dienst Informationen eingeschlossen. |
| -noVerify | Gibt an, dass auf einem Wechselmedium (z. b. einer DVD) gespeicherte Sicherungen nicht auf Fehler überprüft werden. Wenn Sie diesen Parameter nicht verwenden, werden Sicherungen, die auf einem Wechsel Datenträger gespeichert werden, auf Fehler überprüft. |
| -Benutzer | Wenn die Sicherung in einem freigegebenen Remote Ordner gespeichert wird, gibt Sie den Benutzernamen mit der Schreib Berechtigung für den Ordner an. |
| -password | Gibt das Kennwort für den Benutzernamen an, der vom Parameter **-User**bereitgestellt wird. |
| -nogeerbt ACL | Wendet die Zugriffs Steuerungs Listen-Berechtigungen, die den Anmelde Informationen entsprechen, die von den Parametern " **-User** " und " **-Password** " bereitgestellt werden, auf `\\<servername>\<sharename>\WindowsImageBackup\<ComputerBackedUp>\` (den Ordner, der die Sicherung enthält). Wenn Sie später auf die Sicherung zugreifen möchten, müssen Sie diese Anmelde Informationen verwenden oder Mitglied der Gruppe "Administratoren" oder der Gruppe "Sicherungs-Operatoren" auf dem Computer mit dem freigegebenen Ordner sein. Wenn **-nogeerbt ACL** nicht verwendet wird, werden die ACL-Berechtigungen aus dem freigegebenen Remote Ordner standardmäßig auf den Ordner angewendet, `\<ComputerBackedUp>` sodass jeder Benutzer mit Zugriff auf den freigegebenen Remote Ordner auf die Sicherung zugreifen kann. |
| -vssfull | Führt eine vollständige Sicherungskopie mithilfe des Volumeschattenkopie-Dienst (VSS) aus. Alle Dateien werden gesichert, der Verlauf jeder Datei wird aktualisiert, um widerzuspiegeln, dass Sie gesichert wurde, und die Protokolle vorheriger Sicherungen werden möglicherweise abgeschnitten. Wenn dieser Parameter nicht verwendet wird, erstellt die **Wbadmin-Sicherung** eine Kopier Sicherung, aber der Verlauf der zu sichernden Dateien wird nicht aktualisiert.<p>**Vorsicht:** Verwenden Sie diesen Parameter nicht, wenn Sie ein anderes Produkt als Windows Server-Sicherung zum Sichern von Apps verwenden, die sich auf den Volumes befinden, die in der aktuellen Sicherung enthalten sind. Dadurch kann der inkrementelle, differenzielle oder andere Sicherungstyp, den das andere Sicherungs Produkt erstellt, möglicherweise nicht mehr ausgeführt werden, da der Verlauf, auf den Sie sich verlassen, bestimmt, wie viele Daten gesichert werden können, und Sie können unnötig eine vollständige Sicherung durchführen. |
| -vsscopy | Führt eine Kopier Sicherung mithilfe von VSS aus. Alle Dateien werden gesichert, aber der Verlauf der Dateien, die gesichert werden, wird nicht aktualisiert, sodass Sie alle Informationen darüber erhalten, wo die Dateien geändert, gelöscht usw. sowie beliebige Anwendungsprotokoll Dateien. Die Verwendung dieser Art von Sicherung wirkt sich nicht auf die Sequenz von inkrementellen und differenziellen Sicherungen aus, die unabhängig von dieser Kopier Sicherung auftreten können. Dies ist der Standardwert.<p>**Warnung:** Eine Kopier Sicherung kann nicht für inkrementelle oder differenzielle Sicherungen oder Wiederherstellungen verwendet werden |
| -quiet | Führt den Befehl ohne Aufforderungen an den Benutzer aus. |

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie die Sicherung in einem freigegebenen Remote Ordner speichern und dann eine weitere Sicherung auf demselben Computer und demselben freigegebenen Remote Ordner durchführen, überschreiben Sie die vorherige Sicherung.

- Wenn der Sicherungs Vorgang fehlschlägt, können Sie ohne Sicherung eine Sicherung durchzuführen, da die ältere Sicherung überschrieben wird, aber die neuere Sicherung nicht verwendbar ist. Um dies zu vermeiden, empfiehlt es sich, Unterordner im freigegebenen Remote Ordner zu erstellen, um die Sicherungen zu organisieren. Aufgrund dieser Organisation müssen Sie jedoch zweimal über den übergeordneten Ordner verfügbaren Speicherplatz verfügen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherung der Volumes *e:*, *d: \\ Bereitstellungs Punkt*und `\\?\Volume{cc566d14-4410-11d9-9d93-806e6f6e6963}\` für Volume *f:* zu erstellen:

```
wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```

Zum Ausführen einer einmaligen Sicherung von *f: \\ "Ordner1"* und *h: \\ Folder2* auf Volume *d:*, um den Systemstatus zu sichern und eine Kopier Sicherung zu erstellen, sodass die normalerweise geplante differenzielle Sicherung nicht beeinträchtigt wird, geben Sie Folgendes ein:

```
wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
```

Zum Ausführen einer einmaligen, nicht rekursiven Sicherung von *d: \\ "Ordner1"* an der Netzwerkadresse `\\backupshare\backup1*` und zum Einschränken des Zugriffs auf Mitglieder der Gruppe " **Administratoren** " oder " **Sicherungs-Operatoren** " geben Sie Folgendes ein:

```
wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Wbadmin-Befehl](wbadmin.md)
