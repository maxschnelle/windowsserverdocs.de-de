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

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit **nfsadmin** können Sie Server für NFS und Client für NFS verwalten.  
  
## <a name="syntax"></a>Syntax  
**nbsadmin-Server** @no__t-*1 Computername*`] [` @ no__t-4U *username*`[` @ no__t-7p *Password*`]]` `[`0l  
  
**nbsadmin-Server** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` 0R 1*Client* 3 all @ no__t-14  
  
**nbsadmin-Server** @no__t-*1 Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]] {`start `[`0 Ende @ no__t-11  
  
**nbsadmin-Server** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` config *Option*1  
  
**nbsadmin-Server** `[`*Computer Name*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` *Name* der buildgruppe  
  
**nbsadmin-Server** @no__t-*1 Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` Parameter List Groups  
  
**nbsadmin-Server** `[`*Computer Name*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` DeleteGroup *Name*  
  
**nbsadmin-Server** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` renamegroup *OldName newname*  
  
**nfsadmin Server** `[`*Computer Name*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` AddMembers *Name Host*1  
  
**nfsadmin Server** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` ListMembers  
  
**nfsadmin Server** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` deletemembers *Group Host*1  
  
**NF Sadmin Client** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]] {`start 0 Ende @ no__t-11  
  
**nbsadmin Client** `[`*Computername*`] [` @ no__t-4U *username* `[` @ no__t-7p *Password*`]]` config *Option*1  
  
## <a name="description"></a>Beschreibung  
Mit dem **nfsadmin** -Befehl @ no__t-1-Line Utility wird Server für NFS oder Client für NFS auf dem lokalen Computer oder Remote Computer verwaltet, auf dem Microsoft Services for Network File System \(nfs @ no__t-3 ausgeführt wird. Wenn Sie mit einem Konto angemeldet sind, das nicht über die erforderlichen Berechtigungen verfügt, können Sie einen Benutzernamen und ein Kennwort für ein Konto angeben, das über die erforderlichen Berechtigungen verfügt. Welche Aktion von **NF Sadmin** ausgeführt wird, hängt von den Befehls Argumenten ab, die Sie angeben.  
  
Neben dem Dienst @ no__t-0specific Command Arguments und-Optionen akzeptiert **nfsadmin** Folgendes:  
  
*Computername*  
Gibt den Remote Computer an, den Sie verwalten möchten. Sie können den Computer mit einem Windows Internet Name Service \(wins @ no__t-1 oder einem Domain Name System \(dns @ no__t-3-Namen oder nach Internet Protokoll \(ip @ no__t-5-Adresse angeben.  
  
**\-U-** *Benutzername*  
Gibt den Benutzernamen des Benutzers an, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen in der Form <em>Domäne</em> **\\** <em>username</em> hinzuzufügen.  
  
*Kennwort* für **\-P**  
Gibt das Kennwort des Benutzers an, der mithilfe der Option " **\-U** " angegeben wurde. Wenn Sie die Option **\-U** angeben, aber die Option " **\-P** " weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert.  
  
#### <a name="administering-server-for-nfs"></a>Verwalten von Server für NFS  
Verwenden Sie den Befehl **nfsadmin Server** , um Server für NFS zu verwalten. Welche Aktion der **nbsadmin-Server** durchführt, hängt von der Befehls Option oder dem Argument ab, das Sie angeben:  
  
**\-L**  
Listet alle Sperren auf, die von-Clients gehalten werden.  
  
**\-R** {*Client* | **alle**}  
Gibt die Sperren frei, die von einem *Client* oder **, sofern angegeben, von allen Clients** aufbewahrt werden.  
  
**start**  
startet den Server für den NFS-Dienst.  
  
**stop**  
Beendet den Server für den NFS-Dienst.  
  
**config**  
Gibt allgemeine Einstellungen für Server für NFS an. Sie müssen mindestens eine der folgenden Optionen mit dem **Konfigurations** Befehls Argument angeben:  
  
**mapsvr @ no__t-1**<em>Server</em>  
Legt *Server* als Benutzernamenzuordnung Server für Server für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm **sfuadmin** verwenden.  
  
**auditlocation @ no__t-1**{**EventLog** | **Datei** | **beide** | **None**}  
Gibt an, ob Ereignisse überwacht werden und wo die Ereignisse aufgezeichnet werden. Eines der folgenden Argumente ist erforderlich.  
  
**EventLog**  
Gibt an, dass überwachte Ereignisse nur im Ereignisanzeige Anwendungsprotokoll aufgezeichnet werden.  
  
**file**  
Gibt an, dass überwachte Ereignisse nur in der durch config- **Name**angegebenen Datei aufgezeichnet werden.  
  
**zwar**  
Gibt an, dass überwachte Ereignisse sowohl im Anwendungsprotokoll Ereignisanzeige als auch in der durch config- **Name**angegebenen Datei aufgezeichnet werden.  
  
**gar**  
Gibt an, dass Ereignisse nicht überwacht werden.  
  
<em>Datei</em> **Name @ no__t-1**  
Legt die Datei fest, die von *File* als Überwachungs Datei angegeben wird. Der Standardwert ist% sfudir% @no__t -0log\\nfssvr.log  
  
*Größe* von **@ no__t-1**\=  
Legt die *Größe* als maximale Größe der Überwachungs Datei in Megabyte fest. Die maximale Standardgröße beträgt 7 MB.  
  
**Audit @ no__t-1**\[ **\+** | **\-** \]**Mount** \=0**2**3**5**6**Read** 8**0**1 **@no__ t-23**4**Write** 6**8**9**1**2**Create** 4**6**7**9**0**Delete** 2 **@no__ t-44**5**7**8**Sperren** 0**2**3**5**6**alle**  
Gibt die zu protokollierenden Ereignisse an. Um mit der Protokollierung eines Ereignisses zu beginnen, geben Sie ein Pluszeichen \( **\+** \) vor dem Ereignis Namen ein. um die Protokollierung eines Ereignisses zu beenden, geben Sie ein Minuszeichen \( **\-** \) vor dem Ereignis Namen ein. Wenn das Vorzeichen weggelassen wird, wird das Pluszeichen angenommen. Verwenden Sie nicht **all** mit einem anderen Ereignis Namen.  
  
**Sperr Zeitraum @ no__t-1**<em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die der Server für NFS wartet, bis die Sperre aufgehoben wird, nachdem eine Verbindung mit dem Server für NFS unterbrochen und dann wieder hergestellt wurde oder nachdem der Server für NFS-Dienst neu gestartet wurde.  
  
Portmapprotocol @ no__t-0 {TCP | UDP | TCP @ no__t-1udp  
Gibt an, welche Transportprotokolle portmap unterstützt. Die Standardeinstellung ist **TCP @ no__t-1udp**.  
  
mountprotocol @ no__t-0 {TCP | UDP | TCP @ no__t-1udp}  
Gibt an, welche Transportprotokolle von unterstützt werden. Die Standardeinstellung ist **TCP @ no__t-1udp**.  
  
NF-Protokoll-Col @ no__t-0 {TCP | UDP | TCP @ no__t-1udp}  
Gibt an, welche Transportprotokolle das Netzwerkdatei System \(nfs @ no__t-1 unterstützt. Die Standardeinstellung ist **TCP @ no__t-1udp.**  
  
nlmprotocol @ no__t-0 {TCP | UDP | TCP @ no__t-1udp}  
Gibt an, welche Transportprotokolle der Netzwerk Sperren-Manager \(nlm @ no__t-1 unterstützt. Die Standardeinstellung ist **TCP @ no__t-1udp**.  
  
nsmprotocol @ no__t-0 {TCP | UDP | TCP @ no__t-1udp}  
Gibt an, welche Transportprotokolle der Netzwerk Status-Manager \(nsm @ no__t-1 unterstützt. Die Standardeinstellung ist **TCP @ no__t-1udp**.  
  
**enableV3 @ no__t-1**{**Yes** | **No**}  
Gibt an, ob NFS Version 3-Protokolle unterstützt werden. Die Standardeinstellung ist **Ja**.  
  
**erneuter Authentifizierung @ no__t-1**{**Yes** | **No**}  
Gibt an, ob Clientverbindungen nach dem durch **config erneuerauthinterval**angegebenen Zeitraum erneut authentifiziert werden müssen. Die Standardeinstellung ist " **Nein**".  
  
**erneuerauthinterval @ no__t-1**<em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die ververgehen, bevor ein Client erneut authentifiziert werden muss, wenn **config erneuerauth** auf **Yes**festgelegt ist. Der Standardwert ist 600 Sekunden.  
  
**dircache @ no__t-1**<em>Größe</em>  
Gibt die Größe des Verzeichnis Caches in Kilobyte an. Die als *Größe* angegebene Zahl muss ein Vielfaches von 4 zwischen 4 und 128 sein. Der Standardwert für das Verzeichnis @ no__t-0cache beträgt 128 KB.  
  
**translationfile**\= @ no__t-2file @ no__t-3  
Gibt eine Datei mit den Mapping-Informationen zum Ersetzen von Zeichen in den Namen von Dateien an, wenn diese von Windows @ no__t-0basierend auf UNIX @ no__t-1based-Dateisysteme verschoben werden. Wenn *File* nicht angegeben wird, ist die Übersetzung von Dateinamen Zeichen deaktiviert. Wenn der Wert von " **translationfile** " geändert wird, müssen Sie den Server neu starten, damit die Änderung wirksam wird.  
  
**dotfileshidden**\= {**Yes** | **No**}  
Gibt an, ob Dateien, die mit Namen erstellt werden, die mit einem \(. \)-Wert beginnen, im Windows-Dateisystem als ausgeblendet markiert und folglich von NFS-Clients ausgeblendet werden. Die Standardeinstellung ist " **Nein**".  
  
**casesensitivelookups @ no__t-1**{**Yes** | **No**}  
Gibt an, ob bei Verzeichnis Suchvorgängen die Groß-/Kleinschreibung beachtet wird \(Die exakte Übereinstimmung des Zeichen Falls @ no__t-1.  
  
Sie müssen auch den Windows-Kernel Fall @ no__t-0insensitivität deaktivieren, damit Server für NFS die Groß-/Kleinschreibung @ no__t-1 sensible Dateinamen unterstützt. Sie können den Windows-Kernel Fall @ no__t-0insensitivität deaktivieren, indem Sie den folgenden Registrierungsschlüssel auf 0 (null) löschen:  
  
HKLM @ no__t-0system @ no__t-1currentcontrolset @ no__t-2control @ no__t-3session Manager @ no__t-4kernel  
  
DWORD ObCaseInsensitive   
  
> [!IMPORTANT]  
> Dieser Abschnitt gilt nur für Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003. Dieser Abschnitt gilt nicht für Windows Server 2012 R2 oder Windows Server 2012.  
  
**NTF-ASE @ no__t-1**{**Lower** | **Upper** | **Preserve**}  
Gibt an, ob die Groß-/Kleinschreibung von Zeichen in den Namen von Dateien im NTFS-Dateisystem in Kleinbuchstaben, Großbuchstaben oder in der im Verzeichnis gespeicherten Form zurückgegeben wird. Die Standardeinstellung ist " **Preserve**". Diese Einstellung kann nicht geändert werden, wenn **casesensitivelookups** auf **Yes**festgelegt ist.  
  
*Name der namens* Gruppe  
erstellt eine neue Clientgruppe unter Angabe des angegebenen *namens*.  
  
**Parameter List Groups**  
Zeigt die Namen aller Client Gruppen an.  
  
**DeleteGroup** - *Name*  
entfernt die durch den *Namen*angegebene Clientgruppe.  
  
**renamegroup** *OldName newname*  
ändert den Namen der durch *OldName* angegebenen Clientgruppe in *NewName* .  
  
**AddMembers** *Name Host*\[... \]  
Fügt der durch den *Namen*angegebenen Clientgruppe einen *Host* hinzu.  
  
**ListMembers** - *Name*  
Listet die Host Computer in der durch den *Namen*angegebenen Clientgruppe auf.  
  
**deletemembers** - *Gruppen Host*\[... \]  
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
  
**File Access @ no__t-1-** <em>Modus</em>  
-   Gibt den Standard Berechtigungs Modus für Dateien an, die auf dem Network File System-\(nfs @ no__t-1-Server erstellt wurden. Das *Mode* -Argument besteht aus drei Ziffern zwischen 0 und 7 \(inclusive @ no__t-2, die die Standard Berechtigungen für den Benutzer, die Gruppe und andere \(MIT @ no__t-4 darstellen. Die Ziffern werden wie folgt in UNIX @ no__t-0style-Berechtigungen übersetzt: 0 @ no__t-0none, 1 @ no__t-1X, 2 @ no__t-2W, 3 @ no__t-3wx, 4 @ no__t-4R, 5 @ no__t-5Rx, 6 @ no__t-6RW und 7 @ no__t-7rwx. Beispielsweise erteilt **FileAccess @ no__t-1750** dem Besitzer, der RX-Berechtigung für die Gruppe und keinen Zugriffsberechtigungen für andere.  
  
**mapsvr @ no__t-1**<em>Server</em>  
Legt *Server* als Benutzernamenzuordnung Server für den Client für NFS fest. Obwohl diese Option weiterhin für die Kompatibilität mit früheren Versionen unterstützt wird, sollten Sie stattdessen das Dienstprogramm **sfuadmin** verwenden.  
  
**mtype @ no__t-1**{**Hard** | **Soft**}  
Gibt den Standard Einstellungstyp an. Bei einer festen Bereitstellung wird der Client für NFS so lange wiederholt, bis er erfolgreich ausgeführt wird. Für eine weiche Bereitstellung gibt Client für NFS einen Fehler an die aufrufende Anwendung zurück, nachdem der Aufruf so oft wie durch die **Wiederholungs** Option angegeben wurde.  
  
**Retry @ no__t-1-** <em>Nummer</em>  
Gibt an, wie oft versucht werden soll, eine Verbindung für eine weiche Feststellung herzustellen. Dieser Wert muss zwischen 1 und 10 (einschließlich) liegen. Der Standardwert ist 1.  
  
**Timeout @ no__t-1**<em>Sekunden</em>  
Gibt die Anzahl der Sekunden an, die auf eine Verbindung gewartet werden soll \(remote PROCEDURE-Befehl @ no__t-1. Dieser Wert muss 0,8, 0,9 oder eine ganze Zahl zwischen 1 und 60 einschließlich sein. Der Standardwert ist 0,8.  
  
**Protokoll @ no__t-1 {TCP | UDP | TCP @ no__t-2udp}**  
Gibt an, welche Transportprotokolle vom Client unterstützt werden. Die Standardeinstellung ist **TCP @ no__t-1udp.**  
  
**rsize @ no__t-1**<em>Größe</em>  
Gibt die Größe des Lese Puffers in Kilobyte an. Dieser Wert kann 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**wsize @ no__t-1**<em>Größe</em>  
Gibt die Größe des Schreib Puffers in Kilobyte an. Dieser Wert kann 0,5, 1, 2, 4, 8, 16 oder 32 sein. Der Standardwert ist 32.  
  
**Perf @ no__t-1default**  
Stellt die folgenden Leistungseinstellungen in den Standardwerten wieder her:  
  
-   **mtype**  
  
-   **Wiederholen Sie**  
  
-   **timeout**  
  
-   **rsize**  
  
-   **wsize**  
  
**File Access @ no__t-1-** <em>Modus</em>  
Gibt den Standard Berechtigungs Modus für Dateien an, die auf dem Network File System-\(nfs @ no__t-1-Server erstellt wurden. Das *Mode* -Argument besteht aus drei Ziffern zwischen 0 und 7 \(inclusive @ no__t-2, die die Standard Berechtigungen für den Benutzer, die Gruppe und andere \(MIT @ no__t-4 darstellen. Die Ziffern werden wie folgt in UNIX @ no__t-0style-Berechtigungen übersetzt: 0 @ no__t-0none, 1 @ no__t-1X, 2 @ no__t-2W, 3 @ no__t-3wx, 4 @ no__t-4R, 5 @ no__t-5Rx, 6 @ no__t-6RW und 7 @ no__t-7rwx. Beispielsweise erteilt **FileAccess @ no__t-1750** dem Besitzer, der RX-Berechtigung für die Gruppe und keinen Zugriffsberechtigungen für andere.  
  
Wenn Sie keine Befehls Option oder ein Argument angeben, zeigt der **NF Sadmin-Client** den aktuellen Client für NFS-Konfigurationseinstellungen an.  
  

