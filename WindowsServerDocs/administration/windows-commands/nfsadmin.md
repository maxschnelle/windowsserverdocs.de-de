---
title: nfsadmin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 955f6d93379802444d542ea571f98b69b9191f5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837111"
---
# <a name="nfsadmin"></a>nfsadmin

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können **Nfsadmin** Server für NFS- und Client für NFS zu verwalten.  
  
## <a name="syntax"></a>Syntax  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername*`[`\-p *Kennwort* `]]` \-l  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` \-r `{` *Client* `|` alle`}`  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]] {`starten `|` beenden`}`  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Config *Option*`[...]`  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Creategroup *Name*  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Listgroups  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Deletegroup *Name*  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Renamegroup *OldName NewName*  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Addmembers *Name-Host*`[...]`  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Listmembers  
  
**Nfsadmin Server** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Deletemembers *Gruppenhost*`[...]`  
  
**Nfsadmin Client** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]] {`starten `|` beenden`}`  
  
**Nfsadmin Client** `[` *ComputerName*`] [`\-u *Benutzername* `[` \-p *Kennwort* `]]` Config *Option*`[...]`  
  
## <a name="description"></a>Beschreibung  
Die **Nfsadmin** Befehl\-Befehlszeilen-Hilfsprogramm verwaltet Server für NFS oder -Client für NFS auf dem lokalen oder remote-Computer, die mit Microsoft Services for Network File System \(NFS\). Wenn Sie mit einem Konto, die nicht über die erforderlichen Berechtigungen verfügt angemeldet sind, können Sie angeben, einen Benutzernamen und das Kennwort für ein Konto mit diesen. Vom durchgeführten Aktion **Nfsadmin** hängt die Befehlsargumente, die Sie angeben.  
  
Zusätzlich zum Dienst\-bestimmten Befehlsargumente und Optionen, **Nfsadmin** akzeptiert die folgenden:  
  
*computerName*  
Gibt den remote-Computer, die, den Sie verwalten möchten. Können Sie angeben, den Computer mithilfe einer Windows Internet Name Service \(WINS\) Name oder ein Domain Name System \(DNS\) anzugeben, oder Internetprotokoll \(IP\) Adresse.  
  
**\-u** *Benutzername*  
Gibt den Benutzernamen des Benutzers, dessen Anmeldeinformationen sind, verwendet werden soll. Es kann erforderlich sein, den Domänennamen hinzufügen, um den Benutzernamen im Format *Domäne***\\***Benutzername*  
  
**\-p** *Kennwort*  
Gibt das Kennwort des Benutzers angegeben, mit der  **\-u** Option. Bei Angabe der  **\-u** option jedoch weglassen der  **\-p** -Option verwenden, werden Sie aufgefordert, für das Kennwort des Benutzers.  
  
#### <a name="administering-server-for-nfs"></a>Verwalten von Server für NFS  
Verwenden der **Nfsadmin Server** Befehl aus, um Server für NFS zu verwalten. Die spezifische Aktion, die **Nfsadmin Server** nimmt, hängt die Befehlsoption oder das Argument, die Sie angeben:  
  
**\-l**  
Listet alle Sperren frei, die von Clients an.  
  
**\-R** {*Client* | **alle**}  
Hebt die Sperren frei, die eine *Client* oder, wenn Sie **alle** angegeben wird, von allen Clients.  
  
**start**  
Startet den Server für NFS-Dienst.  
  
**stop**  
Beendet der Server für NFS-Dienst.  
  
**config**  
Gibt allgemeine Einstellungen für Server für NFS. Geben Sie an mindestens eine der folgenden Optionen zusammen mit den **Config** Befehlsargument:  
  
**mapsvr\=***server*  
Legt *Server* als Server User Name Mapping für den Server für NFS. Auch wenn diese Option aus, für die Kompatibilität mit früheren Versionen unterstützt werden müssen, verwenden Sie die **Sfuadmin** Hilfsprogramm stattdessen.  
  
**"auditlocation" an\=**{**Eventlog** | **Datei** | **sowohl** | **keine** }  
Gibt an, ob Ereignisse überwacht werden und, in dem die Ereignisse aufgezeichnet werden sollen. Eine der folgenden Argumente ist erforderlich.  
  
**eventlog**  
Gibt an, dass die überwachten Ereignisse aufgezeichnet werden sollen, nur im Ereignis-Viewer-Anwendung anmelden.  
  
**file**  
Gibt an, dass die überwachten Ereignisse nur in der angegebenen Datei aufgezeichnet werden sollen **Config Fname**.  
  
**both**  
Gibt an, dass die überwachten Ereignisse in das Anwendungsprotokoll der Ereignisanzeige sowie die angegebene Datei aufgezeichnet werden **Config Fname**.  
  
**Keine**  
Gibt an, dass Ereignisse nicht überwacht werden.  
  
**fname\=***file*  
Legt die angegebene Datei *Datei* als die Überwachungsdatei. Der Standardwert ist % Sfudir %\\Log\\nfssvr.log  
  
**fsize\=**\=*size*  
Legt *Größe* als die maximale Größe in Megabyte, der die Überwachungsdatei. Die maximale Größe der Standard ist 7 MB.  
  
**Audit\=**\[**\+**|**\-**\]**einbinden** \[ **\+** | **\-** \] **lesen** \[ **\+** | **\-** \] **schreiben** \[ **\+** | **\-** \] **erstellen** \[ **\+** | **\-** \] **löschen** \[ **\+** | **\-** \] **Sperren** \[ **\+** | **\-** \] **alle**  
Gibt die Ereignisse protokolliert werden. Geben Sie zum Starten der Protokollierung eines Ereignisses ein Pluszeichen \( **\+** \) vor dem Ereignisnamen, beenden Sie die Protokollierung eines Ereignisses, geben Sie ein Minuszeichen (-) \( **\-** \) vor den Ereignisnamen. Wenn die Zeichen ausgelassen werden, wird davon ausgegangen, dass das Pluszeichen. Verwenden Sie keine **alle** mit einem beliebigen anderen Event-Namen.  
  
**lockperiod\=***seconds*  
Gibt die Anzahl der Sekunden, die Server für NFS gewartet wird, um Sperren freizugeben, nachdem eine Verbindung mit Server für NFS verloren gehen und dann wieder hergestellt wurde, oder nach dem Neustart des Servers für NFS-Dienst.  
  
Portmapprotocol\={TCP | UDP | TCP\+UDP  
Gibt an, welche Transportprotokolle Portmap unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
Mountprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welcher Transport Protokolle einbinden unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
Nfsprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welcher Transport Network File System Protokolle \(NFS\) unterstützt. Die Standardeinstellung ist **TCP\+UDP**  
  
Nlmprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welcher Transport Network Sperren-Manager-Protokolle \(NLM\) unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
Nsmprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welcher Transport Network-Status-Manager-Protokolle \(NSM\) unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
**enableV3\=**{**yes** | **no**}  
Gibt an, ob es sich bei NFS V3-Protokolle unterstützt werden. Die Standardeinstellung ist **Ja**.  
  
**Renewauth\=**{**Ja** | **keine**}  
Gibt an, ob der Clientverbindungen benötigt wird nach Ablauf des Zeitraums, der anhand des überflüssig werden **Config "renewauthinterval"**. Die Standardeinstellung ist **keine**.  
  
**renewauthinterval\=***seconds*  
Gibt die Anzahl der Sekunden an, die verstreichen, bevor ein Client erzwungen wird, wenn überflüssig **Config Renewauth** nastaven NA hodnotu **Ja**. Der Standardwert ist 600 Sekunden.  
  
**dircache\=***size*  
Gibt die Größe der Directory Cache in Kilobyte an. Die Zahl als *Größe* muss ein Vielfaches von 4 zwischen 4 und 128 Zeichen sein. Das Standardverzeichnis\-Cache beträgt 128 KB.  
  
**translationfile**\=\[file\]  
Gibt eine Datei mit Zuordnungsinformationen für das Ersetzen von Zeichen in die Namen der Dateien beim Verschieben von Windows\-basierend auf UNIX\-basierte Dateisysteme. Wenn *Datei* nicht angegeben ist, und klicken Sie dann die Dateinamen-Zeichenübersetzung deaktiviert ist. Wenn der Wert des **Translationfile** wird geändert, müssen Sie neu starten des Servers für die Änderung wirksam wird.  
  
**dotfileshidden**\={**yes** | **no**}  
Gibt an, ob Dateien, die erstellt werden, deren Name mit einem Punkt beginnt \(.\) als in der Windows-Dateisystem ausgeblendet gekennzeichnet und daher von NFS-Clients ausgeblendet werden. Die Standardeinstellung ist **keine**.  
  
**"casesensitivelookups"\=**{**Ja** | **keine**}  
Gibt an, ob das Verzeichnis Groß-/Kleinschreibung beachtet werden, \(erfordern die genaue Übereinstimmung der Groß-und Kleinschreibung\).  
  
Sie müssen auch Windows-Kernel Fall deaktivieren\-/Kleinschreibung, damit der Server für NFS Fall unterstützt\-sensible Dateinamen. Sie können die Windows-Kernel Fall deaktivieren \- /Kleinschreibung, indem Sie den folgenden Registrierungsschlüssel auf 0 deaktivieren:  
  
HKLM\\SYSTEM\\CurrentControlSet\\Steuerelement\\Sitzungs-Manager\\Kernel  
  
DWOrd obcaseinsensitive   
  
> [!IMPORTANT]  
> Dieser Abschnitt gilt nur für Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003. Dieser Abschnitt gilt nicht für Windows Server 2012 R2 oder Windows Server 2012.  
  
**ntfscase\=**{**lower** | **upper** | **preserve**}  
Gibt an, ob es sich bei Zeichen in den Namen der Dateien im NTFS-Dateisystem die Groß-/Kleinschreibung in Kleinbuchstaben in Großbuchstaben angegeben werden oder in der Form, die im Verzeichnis gespeicherten zurückgegeben wird. Die Standardeinstellung ist **beibehalten**. Diese Einstellung kann nicht geändert werden, wenn **"casesensitivelookups"** nastaven NA hodnotu **Ja**.  
  
**CreateGroup** *Name*  
erstellt eine neue Clientgruppe, und legen sie den angegebenen *Namen*.  
  
**listgroups**  
Zeigt die Namen aller Clientgruppen.  
  
**deletegroup** *name*  
Entfernt den angegebenen Clientgruppe *Namen*.  
  
**Renamegroup** *OldName NewName*  
Ändert den Namen der angegebenen Clientgruppe *OldName* zu *NewName*  
  
**AddMembers** *Namen Host*\[...\]  
Fügt *Host* der Gruppe "Client" anhand des *Namen*.  
  
**listmembers** *Name*  
Listet die Hostcomputer in der Gruppe der gemäß *Namen*.  
  
**Deletemembers** *Gruppenhost*\[...\]  
Entfernt den Client gemäß *Host* aus der Gruppe der gemäß *Gruppe*.  
  
Wenn Sie eine Befehlsoption oder das Argument nicht angeben **Nfsadmin Server** zeigt den aktuellen Server für NFS-Konfigurationseinstellungen.  
  
#### <a name="administering-client-for-nfs"></a>Verwalten von Client für NFS  
Verwenden der **Nfsadmin Client** Befehl aus, um den Client für NFS zu verwalten. Die spezifische Aktion, die **Nfsadmin Client** nimmt, hängt das Befehlsargument, die Sie angeben:  
  
**start**  
beginnt der Client für NFS-Dienst.  
  
**stop**  
Den Client für NFS-Dienst wird beendet.  
  
**config**  
Gibt die allgemeine Einstellungen für den Client für NFS. Geben Sie an mindestens eine der folgenden Optionen zusammen mit den **Config** Befehlsargument:  
  
**fileaccess\=***mode*  
-   Gibt den Standardmodus für die Berechtigungen für Dateien, die für Network File System erstellt \(NFS\) Server. Die *Modus* -Argument besteht aus einer drei Ziffern von 0 bis 7 \(inklusive\) gewährt, die die Standardberechtigungen darstellt, der Benutzer, Gruppe und andere \(bzw.\). Die Ziffern zu übersetzen, in UNIX\-formatieren Sie die Berechtigungen wie folgt: 0\=kein, 1\=x, 2\=w, 3\=Wx, 4\=R, 5\=Rx, 6\=RW-Medien, und 7\=Rwx. Z. B. **"FileAccess"\=750** bietet Rwx-Berechtigungen an den Besitzer, Rx-Berechtigung für die Gruppe und keine Zugriffsberechtigungen für andere Benutzer.  
  
**mapsvr\=***server*  
Legt *Server* als Server User Name Mapping für den Client für NFS. Auch wenn diese Option aus, für die Kompatibilität mit früheren Versionen unterstützt werden müssen, verwenden Sie die **Sfuadmin** Hilfsprogramm stattdessen.  
  
**mtype\=**{**hard** | **soft**}  
Gibt den Standardtyp für die Bereitstellung an. Client für NFS weiterhin für eine ständige Bereitstellung fehlgeschlagenen Remoteprozeduraufrufe zu wiederholen, bis er erfolgreich abgeschlossen wurde. Für eine zeitweilige Bereitstellungen, Client für NFS gibt Fehler an die aufrufende Anwendung nach der der Aufruf wiederholt wird die Anzahl der angegebenen Zeiten die **wiederholen** Option.  
  
**Wiederholen Sie\=*** Anzahl*  
Gibt die Anzahl der Versuche zum Herstellen eine Verbindung für eine zeitweilige Bereitstellungen. Dieser Wert muss zwischen 1 und 10 (einschließlich) liegen. Der Standardwert ist 1.  
  
**timeout\=***seconds*  
Gibt die Anzahl der Sekunden für eine Verbindung \(Remoteprozeduraufruf\). Dieser Wert muss es sich um 0,8, 0.9 oder eine Ganzzahl zwischen 1 und 60, einschließlich sein. Der Standardwert ist 0,8.  
  
**Protokoll\={TCP | UDP | TCP\+UDP}**  
Gibt an, welcher Transport vom Client unterstützten Protokolle. Die Standardeinstellung ist **TCP\+UDP**  
  
**rsize\=***size*  
Gibt die Größe des Lesepuffers in Kilobytes an. Dieser Wert kann es sich um 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**wsize\=***size*  
Gibt die Größe des den Schreibpuffer in Kilobytes an. Dieser Wert kann es sich um 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**perf\=default**  
Stellt die folgenden Leistungseinstellungen auf die Standardwerte:  
  
-   **mtype**  
  
-   **retry**  
  
-   **timeout**  
  
-   **rsize**  
  
-   **wsize**  
  
**fileaccess\=***mode*  
Gibt den Standardmodus für die Berechtigungen für Dateien, die für Network File System erstellt \(NFS\) Server. Die *Modus* -Argument besteht aus einer drei Ziffern von 0 bis 7 \(inklusive\) gewährt, die die Standardberechtigungen darstellt, der Benutzer, Gruppe und andere \(bzw.\). Die Ziffern zu übersetzen, in UNIX\-formatieren Sie die Berechtigungen wie folgt: 0\=kein, 1\=x, 2\=w, 3\=Wx, 4\=R, 5\=Rx, 6\=RW-Medien, und 7\=Rwx. Z. B. **"FileAccess"\=750** bietet Rwx-Berechtigungen an den Besitzer, Rx-Berechtigung für die Gruppe und keine Zugriffsberechtigungen für andere Benutzer.  
  
Wenn Sie eine Befehlsoption oder das Argument nicht angeben **Nfsadmin Client** zeigt den aktuellen Client für NFS-Konfigurationseinstellungen.  
  

