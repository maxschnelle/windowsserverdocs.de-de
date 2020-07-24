---
title: nfsadmin
description: Referenz Artikel für den NF Sadmin-Befehl, der den Server für NFS und den Client für NFS verwaltet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 968c3debfafd552f295591199366c5f6c10fde47
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956772"
---
# <a name="nfsadmin"></a>nfsadmin

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein Befehlszeilen-Hilfsprogramm, mit dem Server für NFS oder Client für NFS auf dem lokalen Computer oder dem Remote Computer verwaltet wird, auf dem Microsoft Services for Network File System (NFS) ausgeführt wird. Wird ohne Parameter verwendet, zeigt der NF Sadmin-Server die aktuellen Server für NFS-Konfigurationseinstellungen an und der NF Sadmin-Client zeigt den aktuellen Client für NFS-Konfigurationseinstellungen an.

## <a name="syntax"></a>Syntax

```
nfsadmin server [computername] [-u Username [-p Password]] -l
nfsadmin server [computername] [-u Username [-p Password]] -r {client | all}
nfsadmin server [computername] [-u Username [-p Password]] {start | stop}
nfsadmin server [computername] [-u Username [-p Password]] config option[...]
nfsadmin server [computername] [-u Username [-p Password]] creategroup <name>
nfsadmin server [computername] [-u Username [-p Password]] listgroups
nfsadmin server [computername] [-u Username [-p Password]] deletegroup <name>
nfsadmin server [computername] [-u Username [-p Password]] renamegroup <oldname> <newname>
nfsadmin server [computername] [-u Username [-p Password]] addmembers <hostname>[...]
nfsadmin server [computername] [-u Username [-p Password]] listmembers
nfsadmin server [computername] [-u Username [-p Password]] deletemembers <hostname><groupname>[...]
nfsadmin client [computername] [-u Username [-p Password]] {start | stop}
nfsadmin client [computername] [-u Username [-p Password]] config option[...]
```

### <a name="general-parameters"></a>Allgemeine Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| computername | Gibt den Remote Computer an, den Sie verwalten möchten. Sie können den Computer mithilfe eines WINS-Namens (Windows Internet Name Service) oder eines Domain Name System (DNS) oder über eine IP-Adresse (Internet Protocol) angeben. |
| -u Benutzername | Gibt den Benutzernamen des Benutzers an, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen im Format "Domäne *\ Benutzer*Name" hinzuzufügen. |
| -p Kennwort | Gibt das Kennwort des Benutzers an, der mit der Option **-u** angegeben wurde. Wenn Sie die Option "- **u** " angeben, aber die Option " **-p** " weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert. |

### <a name="server-for-nfs-related-parameters"></a>Server für NFS-bezogene Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -l | Listet alle Sperren auf, die von-Clients gehalten werden. |
| -r`{client|all}` | Gibt die Sperren frei, die von einem Client oder, sofern angegeben, von allen Clients aufbewahrt werden. |
| start | Startet den Server für den NFS-Dienst. |
| stop | Beendet den Server für den NFS-Dienst. |
| config | Gibt allgemeine Einstellungen für Server für NFS an. Sie müssen mindestens eine der folgenden Optionen mit dem **Konfigurations** Befehls Argument angeben:<ul><li>**mapsvr = `<server>` ** : Legt Server als Benutzernamenzuordnung Server für Server für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm sfuadmin verwenden.</li><li>**auditlocation = `{eventlog|file|both|none}` ** : Gibt an, ob Ereignisse überwacht werden und wo die Ereignisse aufgezeichnet werden. Eines der folgenden Argumente ist erforderlich:<ul><li>**EventLog** : Hiermit wird angegeben, dass überwachte Ereignisse nur im Ereignisanzeige Anwendungsprotokoll aufgezeichnet werden.</li><li>**File** : gibt an, dass überwachte Ereignisse nur in der durch angegebenen Datei aufgezeichnet werden `config fname` .</li><li>**beide** : Hiermit wird angegeben, dass überwachte Ereignisse sowohl im Anwendungsprotokoll Ereignisanzeige als auch in der durch angegebenen Datei aufgezeichnet werden `config fname` .</li><li>**keine** : gibt an, dass Ereignisse nicht überwacht werden.</li></ul><li>**Name = `<file>` ** : Legt die Datei fest, die von der Datei als Überwachungs Datei angegeben wird. Der Standardwert ist **%sfudir%\Log \\ NF-VR. log**.</li><li>**f size = `<size>` ** : Legt die Größe als maximale Größe der Überwachungs Datei in Megabyte fest. Die maximale Standardgröße beträgt **7 MB**.</li><li>**`audit=[+|-]mount [+|-]read [+|-]write [+|-]create [+|-]delete [+|-]locking [+|-]all`**: Gibt die zu protokollierenden Ereignisse an. Um mit der Protokollierung eines Ereignisses zu beginnen, geben Sie ein Pluszeichen ( **+** ) vor dem Ereignis Namen ein. um die Protokollierung eines Ereignisses zu beenden, geben Sie **-** vor dem Ereignis Namen ein Minuszeichen () ein. Wenn das Vorzeichen weggelassen wird, **+** wird das Vorzeichen angenommen. Verwenden Sie nicht **all** mit einem anderen Ereignis Namen.</li><li>**Sperr Zeitraum = `<seconds>` ** : Gibt die Anzahl der Sekunden an, die der Server für NFS wartet, um Sperren freizugeben, nachdem eine Verbindung mit dem Server für NFS unterbrochen und dann wieder hergestellt wurde oder nachdem der Server für NFS-Dienst neu gestartet wurde.</li><li>**portmapprotocol = `{TCP|UDP|TCP+UDP}` ** : Gibt an, welche Transportprotokolle von portmap unterstützt werden. Die Standardeinstellung ist **TCP + UDP**.</li><li>**mountprotocol = `{TCP|UDP|TCP+UDP}` ** : Gibt an, welche Transportprotokolle von unterstützt werden. Die Standardeinstellung ist **TCP + UDP**.</li><li>**NF-Protokoll-Col `{TCP|UDP|TCP+UDP}` =** : Gibt an, welche Transportprotokolle von Network File System (NFS) unterstützt werden. Die Standardeinstellung ist **TCP + UDP** .</li><li>**nlmprotocol = `{TCP|UDP|TCP+UDP}` ** : Gibt an, welche Transportprotokolle der Netzwerk Sperr Manager (NLM) unterstützt. Die Standardeinstellung ist **TCP + UDP**.</li><li>**nsmprotocol = `{TCP|UDP|TCP+UDP}` ** : Gibt an, welche Transportprotokolle der Netzwerk Status-Manager (NSM) unterstützt. Die Standardeinstellung ist **TCP + UDP**.</li><li>**enableV3 = `{yes|no}` ** : Hiermit wird angegeben, ob NFS Version 3-Protokolle unterstützt werden. Die Standardeinstellung ist **Ja**.</li><li>**erneuter verlänglich `{yes|no}` =** : Hiermit wird angegeben, ob Clientverbindungen nach dem durch config erneuerauthinterval angegebenen Zeitraum erneut authentifiziert werden müssen. Die Standardeinstellung ist " **Nein**".</li><li>**erneuungsinterintervall = `<seconds>` ** : Gibt die Anzahl der Sekunden an, die ververgehen, bevor ein Client erneut authentifiziert werden muss, wenn `config renewauth` auf **Ja**festgelegt ist. Der Standardwert ist **600 Sekunden**.</li><li>**dircache = `<size>` ** : Gibt die Größe des Verzeichnis Caches in Kilobyte an. Die als Größe angegebene Zahl muss ein Vielfaches von 4 zwischen 4 und 128 sein. Die Standardgröße des Verzeichnis Caches beträgt **128 KB**.</li><li>**translationfile = `<file>` ** : Gibt eine Datei mit Mapping-Informationen zum Ersetzen von Zeichen in den Namen von Dateien an, wenn diese aus Windows-basierten in UNIX-basierten Dateisystemen verschoben werden. Wenn File nicht angegeben wird, ist die Übersetzung von Dateinamen Zeichen deaktiviert. Wenn der Wert von " **translationfile** " geändert wird, müssen Sie den Server neu starten, damit die Änderung wirksam wird.</li><li>**dotfileshidden = `{yes|no}` ** : Hiermit wird angegeben, ob Dateien mit Namen, die mit einem Zeitraum (.) beginnen, im Windows-Dateisystem als ausgeblendet markiert und folglich von NFS-Clients ausgeblendet werden. Die Standardeinstellung ist " **Nein**".</li><li>**casesensitivelookups = `{yes|no}` ** : Hiermit wird angegeben, ob bei Verzeichnis Suchvorgängen die Groß-/Kleinschreibung beachtet wird (eine exakte Übereinstimmung des Zeichen Falls<p>Sie müssen auch die Unterscheidung nach Groß-/Kleinschreibung von Windows-Kernel deaktivieren, damit Dateinamen unterstützt werden. Um die Unterscheidung nach Groß-/Kleinschreibung zu unterstützen, ändern Sie den **DWORD** -Wert des Registrierungsschlüssels `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\kernel` in **0**.</li><li>**ntsscase = `{lower|upper|preserve}` ** : Gibt an, ob die Groß-/Kleinschreibung von Zeichen in den Namen von Dateien im NTFS-Dateisystem in Kleinbuchstaben, Großbuchstaben oder in der im Verzeichnis gespeicherten Form zurückgegeben wird. Die Standardeinstellung ist " **Preserve**". Diese Einstellung kann nicht geändert werden, wenn **casesensitivelookups** auf **Yes**festgelegt ist.</li></ul> |
| "kreategroup"`<name>` | Erstellt eine neue Clientgruppe unter Angabe des angegebenen Namens. |
| Parameter List Groups | Zeigt die Namen aller Client Gruppen an. |
| DeleteGroup`<name>` | Entfernt die durch den Namen angegebene Clientgruppe. |
| renamegroup `<oldname>``<newname>` | Ändert den Namen der durch *OldName* angegebenen Clientgruppe in *NewName*. |
| AddMembers`<hostname>[...]` | Fügt der durch den *Namen*angegebenen Clientgruppe einen *Host* hinzu. |
| ListMembers`<name>` | Listet die Host Computer in der durch den *Namen*angegebenen Clientgruppe auf. |
| deletemembers`<hostname><groupname>[...]` | Entfernt den vom *Host* angegebenen Client aus der durch die *Gruppe*angegebenen Clientgruppe. |

### <a name="client-for-nfs-related-parameters"></a>Client für NFS-bezogene Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| start | Startet den Client für den NFS-Dienst. |
| stop | Beendet den Client für den NFS-Dienst. |
| config | Gibt allgemeine Einstellungen für Client für NFS an. Sie müssen mindestens eine der folgenden Optionen mit dem **Konfigurations** Befehls Argument angeben:<ul><li>**File Access = `<mode>` ** : Gibt den Standard Berechtigungs Modus für Dateien an, die auf NFS-Servern (Network File System) erstellt werden. Das **Mode** -Argument besteht aus einer dreistelligen Zahl zwischen 0 und 7 (einschließlich), die die Standard Berechtigungen für den Benutzer, die Gruppe und andere darstellen. Die Ziffern werden wie folgt in UNIX-Berechtigungen übersetzt: *0 = None*, *1 = x (Execute)*, *2 = w (nur schreiben)*, *3 = WX (Write und Execute)*, *4 = r (* schreibgeschützt), *5 = RX (Read und Execute)*, *6 = RW (lesen und schreiben)* und *7 = rwx (lesen, schreiben und ausführen)*. Beispielsweise `fileaccess=750` gewährt den Besitzern Berechtigungen zum Lesen, schreiben und ausführen, Lese-und Ausführungs Berechtigungen für die Gruppe und keine Zugriffsberechtigung für andere.</li><li>**mapsvr = `<server>` ** : Legt Server als Benutzernamenzuordnung Server für den Client für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm sfuadmin verwenden.</li><li>**mtype = `{hard|soft}` ** : Gibt den Standard Einstellungstyp an. Bei einer festen Bereitstellung wird der Client für NFS so lange wiederholt, bis er erfolgreich ausgeführt wird. Für eine weiche Bereitstellung gibt Client für NFS einen Fehler an die aufrufende Anwendung zurück, nachdem der Aufruf so oft wie durch die Wiederholungs Option angegeben wurde.</li><li>**Retry = `<number>` ** : Hiermit wird angegeben, wie oft versucht werden soll, eine Verbindung für eine weiche Feststellung herzustellen. Dieser Wert muss zwischen 1 und 10 (einschließlich) liegen. Der Standardwert lautet **1**.</li><li>**Timeout = `<seconds>` ** : Gibt die Anzahl der Sekunden an, die auf eine Verbindung gewartet werden soll (Remote Prozedur Aufrufe). Dieser Wert muss *0,8*, *0,9*oder eine ganze Zahl zwischen *1 und 60*einschließlich sein. Der Standardwert ist **0,8**.</li><li>**Protokoll = `{TCP|UDP|TCP+UDP}` ** : Gibt an, welche Transportprotokolle vom Client unterstützt werden. Die Standardeinstellung ist **TCP + UDP**.</li><li>**rsize = `<size>` ** : Gibt die Größe des Lese Puffers in Kilobyte an. Dieser Wert kann *0,5, 1, 2, 4, 8, 16* oder *32*sein. Der Standardwert ist **32**.</li><li>**wsize = `<size>` ** : Gibt die Größe des Schreib Puffers in Kilobyte an. Dieser Wert kann *0,5, 1, 2, 4, 8, 16* oder *32*sein. Der Standardwert ist **32**.</li><li>**perf = default** : stellt die folgenden Leistungseinstellungen in den Standardwerten *mtype*, *Wiederholen Sie*, *Timeout*, *rsize*oder *wsize*wieder her. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Server für NFS oder den Client für NFS anzuhalten:

```
nfsadmin server stop
nfsadmin client stop
```

Geben Sie Folgendes ein, um den Server für NFS oder den Client für NFS zu starten:

```
nfsadmin server start
nfsadmin client start
```

Geben Sie Folgendes ein, um die Groß-/Kleinschreibung von Server für NFS festzulegen:

```
nfsadmin server config casesensitive=no
```

Geben Sie Folgendes ein, um die Groß-/Kleinschreibung von Clients für NFS festzulegen:

```
nfsadmin client config casesensitive=yes
```

Wenn Sie alle aktuellen Server für NFS-oder Client für NFS-Optionen anzeigen möchten, geben Sie Folgendes ein:

```
nfsadmin server config
nfsadmin client config
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Referenz zu NFS-Cmdlets](/powershell/module/nfs)
