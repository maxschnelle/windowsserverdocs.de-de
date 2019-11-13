---
title: nfsadmin
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 2658cf610e4328d382b9224f4230d68a022d1cc3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373219"
---
# <a name="nfsadmin"></a>nfsadmin

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit **nfsadmin** können Sie Server für NFS und Client für NFS verwalten.  
  
## <a name="syntax"></a>Syntax  
**nbsadmin-Server** `[`*Computername*`] [`\-u *Benutzername*`[`\-p *Kennwort*`]]` \-l  
  
**nbsadmin-Server** `[`*Computername*`] [`\-u *username* `[`\-p *Password*`]]` \-r `{`*Client* `|` alle`}`  
  
**nbsadmin-Server** `[`*Computername*`] [`\-u *username* `[`\-p- *Kennwort*`]] {``|` beendet`}`  
  
**nbsadmin-Server** `[`*Computername*`] [`\-u *username* `[`\-p *Password*`]]` config- *Option*`[...]`  
  
**nbsadmin-Server** `[`*Computer Name*`] [`\-u *Benutzername* `[`\-p *Kennwort*`]]` *Name* der buildgruppe  
  
**nbsadmin-Server** `[`*Computername*`] [`\-u *Benutzername* `[`\-p *Kennwort*`]]` Parameter List Groups  
  
**nbsadmin-Server** `[`*Computer Name*`] [`\-u *Benutzername* `[`\-p *Kennwort*`]]` DeleteGroup- *Name*  
  
**nbsadmin-Server** `[`*Computername*`] [`\-u *Benutzername* `[`\-p *Kennwort*`]]` renamegroup *OldName newname*  
  
**nfsadmin Server** `[`*Computer Name*`] [`\-u *username* `[`\-p *Password*`]]` AddMembers *Name Host*`[...]`  
  
**nfsadmin-Server** `[`*Computername*`] [`\-u *Benutzername* `[`\-p *Kennwort*`]]` ListMembers  
  
**nfsadmin Server** `[`*Computername*`] [`\-u *username* `[`\-p *Password*`]]` deletemembers *Group Host*`[...]`  
  
**nbsadmin-Client** `[`*Computername*`] [`\-u *username* `[`\-p- *Kennwort*`]] {``|` beendet`}`  
  
der **NF Sadmin-Client** `[`*Computername*`] [`\-u *username* `[`\-p *Password*`]]` config- *Option*`[...]`  
  
## <a name="description"></a>Beschreibung  
Mit dem Befehl " **nfsadmin** "\--Zeilen Dienstprogramm wird Server für NFS oder Client für NFS auf dem lokalen Computer oder Remote Computer verwaltet, auf dem Microsoft-Dienste für Network File System \(NFS\)ausgeführt werden. Wenn Sie mit einem Konto angemeldet sind, das nicht über die erforderlichen Berechtigungen verfügt, können Sie einen Benutzernamen und ein Kennwort für ein Konto angeben, das über die erforderlichen Berechtigungen verfügt. Welche Aktion von **NF Sadmin** ausgeführt wird, hängt von den Befehls Argumenten ab, die Sie angeben.  
  
Neben den Dienst\-bestimmten Befehls Argumenten und-Optionen akzeptiert **nfsadmin** Folgendes:  
  
*Computername*  
Gibt den Remote Computer an, den Sie verwalten möchten. Sie können den Computer mithilfe eines Windows Internet Name Service \(WINS\) namens oder eines Domain Name System \(DNS-\)-namens oder über eine IP-\(Adresse für das Internetprotokoll\) angeben.  
  
**\-u** *Benutzername*  
Gibt den Benutzernamen des Benutzers an, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen in der Form <em>Domäne</em> **\\** <em>Benutzernamen</em> hinzuzufügen.  
  
*Kennwort* für **\-p**  
Gibt das Kennwort des Benutzers an, der mit der Option **\-u** angegeben wurde. Wenn Sie die Option **\-u** angeben, aber die Option **\-p** weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert.  
  
#### <a name="administering-server-for-nfs"></a>Verwalten von Server für NFS  
Verwenden Sie den Befehl **nfsadmin Server** , um Server für NFS zu verwalten. Welche Aktion der **nbsadmin-Server** durchführt, hängt von der Befehls Option oder dem Argument ab, das Sie angeben:  
  
**\-l**  
Listet alle Sperren auf, die von-Clients gehalten werden.  
  
**\-r** {*Client* | **all**}  
Gibt die Sperren frei, die von einem *Client* oder **, sofern angegeben, von allen Clients** aufbewahrt werden.  
  
**start**  
startet den Server für den NFS-Dienst.  
  
**stop**  
Beendet den Server für den NFS-Dienst.  
  
**config**  
Gibt allgemeine Einstellungen für Server für NFS an. Sie müssen mindestens eine der folgenden Optionen mit dem **Konfigurations** Befehls Argument angeben:  
  
**mapsvr-\=** <em>Server</em>  
Legt *Server* als Benutzernamenzuordnung Server für Server für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm **sfuadmin** verwenden.  
  
**auditlocation\=** {**EventLog** | **Datei** |  ** | ** **None**}  
Gibt an, ob Ereignisse überwacht werden und wo die Ereignisse aufgezeichnet werden. Eines der folgenden Argumente ist erforderlich.  
  
**EventLog**  
Gibt an, dass überwachte Ereignisse nur im Ereignisanzeige Anwendungsprotokoll aufgezeichnet werden.  
  
**file**  
Gibt an, dass überwachte Ereignisse nur in der durch config- **Name**angegebenen Datei aufgezeichnet werden.  
  
**zwar**  
Gibt an, dass überwachte Ereignisse sowohl im Anwendungsprotokoll Ereignisanzeige als auch in der durch config- **Name**angegebenen Datei aufgezeichnet werden.  
  
**gar**  
Gibt an, dass Ereignisse nicht überwacht werden.  
  
Datei **Name\=** <em>Datei</em>  
Legt die Datei fest, die von *File* als Überwachungs Datei angegeben wird. Der Standardwert ist% sfudir%\\Log\\nberssvr. log  
  
Größe **\=** \=*Größe*  
Legt die *Größe* als maximale Größe der Überwachungs Datei in Megabyte fest. Die maximale Standardgröße beträgt 7 MB.  
  
**Audit\=** \[ **\+** | **\-** \] **\[** \+ **|** \- **\]** \[\+| **\-** \] **\[** \+ **|** \- **\]** \[ **\+** | **\-\]** **Löschen** \[ **\+** | **\-** \] **\[** \+ **|** \- **\]**  
Gibt die zu protokollierenden Ereignisse an. Um mit der Protokollierung eines Ereignisses zu beginnen, geben Sie ein Pluszeichen ein, \( **\+** vor dem Ereignis Namen\). Wenn Sie das Protokollieren eines Ereignisses beenden möchten, geben Sie ein Minuszeichen \( **\-** vor dem Ereignis Namen\). Wenn das Vorzeichen weggelassen wird, wird das Pluszeichen angenommen. Verwenden Sie nicht **all** mit einem anderen Ereignis Namen.  
  
**Sperr Zeitraum\=** <em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die der Server für NFS wartet, bis die Sperre aufgehoben wird, nachdem eine Verbindung mit dem Server für NFS unterbrochen und dann wieder hergestellt wurde oder nachdem der Server für NFS-Dienst neu gestartet wurde.  
  
Portmapprotocol\={TCP | UDP | TCP-\+UDP  
Gibt an, welche Transportprotokolle portmap unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
mountprotocol-\={TCP | UDP | TCP\+UDP}  
Gibt an, welche Transportprotokolle von unterstützt werden. Die Standardeinstellung ist **TCP\+UDP**.  
  
nspsproycol\={TCP | UDP | TCP\+UDP}  
Gibt an, welche Transportprotokolle das Netzwerkdatei System \(NFS\) unterstützt. Die Standardeinstellung ist **TCP\+UDP** .  
  
nlmprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welche Transportprotokolle der Netzwerk Sperren-Manager \(NLM-\) unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
nsmprotocol\={TCP | UDP | TCP\+UDP}  
Gibt an, welche Transportprotokolle der Netzwerk Status-Manager \(NSM\) unterstützt. Die Standardeinstellung ist **TCP\+UDP**.  
  
**enableV3\=** {**Yes** | **Nein**}  
Gibt an, ob NFS Version 3-Protokolle unterstützt werden. Die Standardeinstellung ist **Ja**.  
  
**erneuter erneuter\=** {**Yes** | **Nein**}  
Gibt an, ob Clientverbindungen nach dem durch **config erneuerauthinterval**angegebenen Zeitraum erneut authentifiziert werden müssen. Die Standardeinstellung ist " **Nein**".  
  
**erneuungauthinterval\=** <em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die ververgehen, bevor ein Client erneut authentifiziert werden muss, wenn **config erneuerauth** auf **Yes**festgelegt ist. Der Standardwert ist 600 Sekunden.  
  
**dircache-\=** <em>Größe</em>  
Gibt die Größe des Verzeichnis Caches in Kilobyte an. Die als *Größe* angegebene Zahl muss ein Vielfaches von 4 zwischen 4 und 128 sein. Das Standardverzeichnis\-Cache Größe beträgt 128 KB.  
  
\[Datei " **translationfile** "\=\]  
Gibt eine Datei mit Mapping-Informationen zum Ersetzen von Zeichen in den Namen von Dateien an, wenn Sie von Windows-\-basierend auf UNIX-\-basierten Dateisystemen verschoben werden. Wenn *File* nicht angegeben wird, ist die Übersetzung von Dateinamen Zeichen deaktiviert. Wenn der Wert von " **translationfile** " geändert wird, müssen Sie den Server neu starten, damit die Änderung wirksam wird.  
  
**dotfileshidden**\={**Yes** | **Nein**}  
Gibt an, ob Dateien, die mit Namen erstellt werden, die mit einem Zeitraum \(beginnen.\) werden im Windows-Dateisystem als ausgeblendet markiert und daher von NFS-Clients ausgeblendet. Die Standardeinstellung ist " **Nein**".  
  
**casesensitivelookups\=** {**Yes** | **No**}  
Gibt an, ob bei Verzeichnis Suchvorgängen die Groß-/Kleinschreibung beachtet wird \(die genaue Übereinstimmung von Zeichen Fällen\)erfordert  
  
Außerdem müssen Sie den Windows-Kernel Fall\-Insensitivität deaktivieren, damit Server für NFS die Groß-/Kleinschreibung\-sensible Dateinamen unterstützen. Wenn Sie den folgenden Registrierungsschlüssel auf 0 (null) deaktivieren möchten, können Sie den Windows-Kernel Fall\-Insensitivität  
  
HKLM\\System\\CurrentControlSet\\Control\\Session Manager\\Kernel  
  
DWORD ObCaseInsensitive   
  
> [!IMPORTANT]  
> Dieser Abschnitt gilt nur für Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003. Dieser Abschnitt gilt nicht für Windows Server 2012 R2 oder Windows Server 2012.  
  
**ntsscase\=** {**Lower** | **Upper** | **Preserve**}  
Gibt an, ob die Groß-/Kleinschreibung von Zeichen in den Namen von Dateien im NTFS-Dateisystem in Kleinbuchstaben, Großbuchstaben oder in der im Verzeichnis gespeicherten Form zurückgegeben wird. Die Standardeinstellung ist " **Preserve**". Diese Einstellung kann nicht geändert werden, wenn **casesensitivelookups** auf **Yes**festgelegt ist.  
  
*Name der namens* Gruppe  
erstellt eine neue Clientgruppe unter Angabe des angegebenen *namens*.  
  
**Parameter List Groups**  
Zeigt die Namen aller Client Gruppen an.  
  
**DeleteGroup** - *Name*  
entfernt die durch den *Namen*angegebene Clientgruppe.  
  
**renamegroup** *OldName newname*  
ändert den Namen der durch *OldName* angegebenen Clientgruppe in *NewName* .  
  
**AddMembers** *Name Host*\[...\]  
Fügt der durch den *Namen*angegebenen Clientgruppe einen *Host* hinzu.  
  
**ListMembers** - *Name*  
Listet die Host Computer in der durch den *Namen*angegebenen Clientgruppe auf.  
  
\[" **deletemembers** "- *Gruppe* ...\]  
entfernt den vom *Host* angegebenen Client aus der durch die *Gruppe*angegebenen Clientgruppe.  
  
Wenn Sie keine Befehls Option oder ein Argument angeben, zeigt der **NF Sadmin-Server** den aktuellen Server für NFS-Konfigurationseinstellungen an.  
  
#### <a name="administering-client-for-nfs"></a>Verwalten von Client für NFS  
Verwenden Sie den **Client Befehl nfsadmin** , um den Client für NFS zu verwalten. Die spezifische Aktion, die der **nbsadmin-Client** durchführt, hängt vom angegebenen Befehls Argument ab:  
  
**start**  
startet den Client für den NFS-Dienst.  
  
**stop**  
Beendet den Client für den NFS-Dienst.  
  
**config**  
Gibt allgemeine Einstellungen für Client für NFS an. Sie müssen mindestens eine der folgenden Optionen mit dem **Konfigurations** Befehls Argument angeben:  
  
**File Access-\=** <em>Modus</em>  
-   Gibt den Standard Berechtigungs Modus für Dateien an, die auf Network File System \(NFS\)-Servern erstellt werden. Das *Mode* -Argument besteht aus drei Ziffern zwischen 0 und 7 \(inklusiven\) die die Standard Berechtigungen darstellen, die der Benutzer, die Gruppe und andere \(jeweils\)erteilt haben. Die Ziffern werden wie folgt in UNIX-\-Format Berechtigungen übersetzt: 0\=None, 1\=x, 2\=w, 3\=WX, 4\=r, 5\=RX, 6\=RW und 7\=rwx. Beispielsweise erteilt **File Access\=750** dem Besitzer, der RX-Berechtigung für die Gruppe und keinen Zugriffsberechtigungen für andere Benutzer die rwx-Berechtigung.  
  
**mapsvr-\=** <em>Server</em>  
Legt *Server* als Benutzernamenzuordnung Server für den Client für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm **sfuadmin** verwenden.  
  
**mtype\=** {**Hard** | **Soft**}  
Gibt den Standard Einstellungstyp an. Bei einer festen Bereitstellung wird der Client für NFS so lange wiederholt, bis er erfolgreich ausgeführt wird. Für eine weiche Bereitstellung gibt Client für NFS einen Fehler an die aufrufende Anwendung zurück, nachdem der Aufruf so oft wie durch die **Wiederholungs** Option angegeben wurde.  
  
**Wiederholungs\=** <em>Nummer</em>  
Gibt an, wie oft versucht werden soll, eine Verbindung für eine weiche Feststellung herzustellen. Dieser Wert muss zwischen 1 und 10 (einschließlich) liegen. Der Standardwert ist 1.  
  
**Timeout\=** <em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die auf eine Verbindung \(Remote Prozedur Aufruf\)gewartet werden soll. Dieser Wert muss 0,8, 0,9 oder eine ganze Zahl zwischen 1 und 60 einschließlich sein. Der Standardwert ist 0,8.  
  
**Protokoll\={TCP | UDP | TCP\+UDP}**  
Gibt an, welche Transportprotokolle vom Client unterstützt werden. Die Standardeinstellung ist **TCP\+UDP** .  
  
**rsize-\=** <em>Größe</em>  
Gibt die Größe des Lese Puffers in Kilobyte an. Dieser Wert kann 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**wsize-\=** <em>Größe</em>  
Gibt die Größe des Schreib Puffers in Kilobyte an. Dieser Wert kann 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**Leistungs-\=Standard**  
Stellt die folgenden Leistungseinstellungen in den Standardwerten wieder her:  
  
-   **mtype**  
  
-   **Wiederholen Sie**  
  
-   **timeout**  
  
-   **rsize**  
  
-   **wsize**  
  
**File Access-\=** <em>Modus</em>  
Gibt den Standard Berechtigungs Modus für Dateien an, die auf Network File System \(NFS\)-Servern erstellt werden. Das *Mode* -Argument besteht aus drei Ziffern zwischen 0 und 7 \(inklusiven\) die die Standard Berechtigungen darstellen, die der Benutzer, die Gruppe und andere \(jeweils\)erteilt haben. Die Ziffern werden wie folgt in UNIX-\-Format Berechtigungen übersetzt: 0\=None, 1\=x, 2\=w, 3\=WX, 4\=r, 5\=RX, 6\=RW und 7\=rwx. Beispielsweise erteilt **File Access\=750** dem Besitzer, der RX-Berechtigung für die Gruppe und keinen Zugriffsberechtigungen für andere Benutzer die rwx-Berechtigung.  
  
Wenn Sie keine Befehls Option oder ein Argument angeben, zeigt der **NF Sadmin-Client** den aktuellen Client für NFS-Konfigurationseinstellungen an.  
  

