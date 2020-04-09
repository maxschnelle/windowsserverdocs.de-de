---
title: ksetup
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3c61fd81691f9db44330eddbf40d4212d1786ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841253"
---
# <a name="ksetup"></a>ksetup



Führt Aufgaben im Zusammenhang mit der Einrichtung und Wartung des Kerberos-Protokolls und der Schlüsselverteilungscenter (KDC) zur Unterstützung von Kerberos-Bereichen aus, die nicht gleichzeitig als Windows-Domänen dienen. Beispiele dazu, wie dieser Befehl verwendet werden kann, finden Sie im Abschnitt "Beispiele" in den entsprechenden Unterthemen.

## <a name="syntax"></a>Syntax

```
ksetup 
[/setrealm <DNSDomainName>] 
[/mapuser <Principal> <Account>] 
[/addkdc <RealmName> <KDCName>] 
[/delkdc <RealmName> <KDCName>]
[/addkpasswd <RealmName> <KDCPasswordName>] 
[/delkpasswd <RealmName> <KDCPasswordName>]
[/server <ServerName>] 
[/setcomputerpassword <Password>]
[/removerealm <RealmName>]  
[/domain <DomainName>] 
[/changepassword <OldPassword> <NewPassword>] 
[/listrealmflags] 
[/setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/dumpstate]
[/addhosttorealmmap] <HostName> <RealmName>]  
[/delhosttorealmmap] <HostName> <RealmName>]  
[/setenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <DomainName>
[/addenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <DomainName>

```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Ksetup:setrealm](ksetup-setrealm.md)|Dieser Computer ist ein Mitglied eines Kerberos-Bereichs.|
|[Ksetup:mapuser](ksetup-mapuser.md)|Ordnet einem Konto einen Kerberos-Prinzipal zu.|
|[Ksetup:addkdc](ksetup-addkdc.md)|Definiert einen KDC-Eintrag für den angegebenen Bereich.|
|[Ksetup:delkdc](ksetup-delkdc.md)|Löscht einen KDC-Eintrag für den Bereich.|
|[Ksetup:addkpasswd](ksetup-addkpasswd.md)|Fügt eine kpasswd-Server Adresse für einen Bereich hinzu.|
|[Ksetup:delkpasswd](ksetup-delkpasswd.md)|Löscht eine kpasswd-Server Adresse für einen Bereich.|
|[Ksetup:server](ksetup-server.md)|Ermöglicht es Ihnen, den Namen eines Windows-Computers anzugeben, auf dem die Änderungen angewendet werden sollen.|
|[Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)|Legt das Kennwort für das Domänen Konto des Computers (oder den Host Prinzipal) fest.|
|[Ksetup:removerealm](ksetup-removerealm.md)|Löscht alle Informationen für den angegebenen Bereich aus der Registrierung.|
|[Ksetup:domain](ksetup-domain.md)|Ermöglicht das Angeben einer Domäne (wenn \<Domain Name > nicht mithilfe von **/Domain**festgelegt wurde).|
|[Ksetup:changepassword](ksetup-changepassword.md)|Ermöglicht die Verwendung von kpasswd zum Ändern des Kennworts des angemeldeten Benutzers.|
|[Ksetup:listrealmflags](ksetup-listrealmflags.md)|Listet die verfügbaren bereichflags auf, die von **Ksetup** erkannt werden können.|
|[Ksetup:setrealmflags](ksetup-setrealmflags.md)|Legt bereichflags für einen bestimmten Bereich fest.|
|[Ksetup:addrealmflags](ksetup-addrealmflags.md)|Fügt einem Bereich weitere bereichflags hinzu.|
|[Ksetup:delrealmflags](ksetup-delrealmflags.md)|Löscht bereichflags aus einem Bereich.|
|[Ksetup:dumpstate](ksetup-dumpstate.md)|Analysiert die Kerberos-Konfiguration auf dem angegebenen Computer. Fügt der Registrierung einen Host für die Bereichs Zuordnung hinzu.|
|[Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)|Fügt einen Registrierungs Wert hinzu, um den Host dem Kerberos-Bereich zuzuordnen.|
|[Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)|Löscht den Registrierungs Wert, der den Host Computer dem Kerberos-Bereich zugeordnet hat.|
|[Ksetup:setenctypeattr](ksetup-setenctypeattr.md)|Legt ein oder mehrere Vertrauens Attribute der Verschlüsselungstypen für die Domäne fest.|
|[Ksetup:getenctypeattr](ksetup-getenctypeattr.md)|Ruft das Vertrauens Attribut der Verschlüsselungstypen für die Domäne ab.|
|[Ksetup:addenctypeattr](ksetup-addenctypeattr.md)|Fügt Verschlüsselungstypen zum Vertrauens Attribut der Verschlüsselungstypen für die Domäne hinzu.|
|[Ksetup:delenctypeattr](ksetup-delenctypeattr.md)|Löscht das Vertrauens Attribut der Verschlüsselungstypen für die Domäne.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Mithilfe von **Ksetup** werden die Computereinstellungen zum Suchen von Kerberos-Bereichen geändert. Bei nicht von Microsoft Kerberos – basierten Implementierungen werden diese Informationen in der Regel in der Datei krb5. conf gespeichert. In Windows Server-Betriebssystemen wird Sie in der Registrierung gespeichert. Sie können dieses Tool verwenden, um diese Einstellungen zu ändern. Diese Einstellungen werden von Arbeitsstationen zum Suchen von Kerberos-Bereichen und von Domänen Controllern verwendet, um Kerberos-Bereiche für bereichsübergreifende Vertrauens Stellungen zu finden.

**Ksetup** initialisiert Registrierungsschlüssel, die der Kerberos-Security Support Provider (SSP) verwendet, um einen KDC für den Kerberos-Bereich zu suchen, wenn auf dem Computer Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird und kein Mitglied einer Windows-Domäne ist. Nach der Konfiguration kann sich der Benutzer eines Client Computers, auf dem das Windows-Betriebssystem ausgeführt wird, bei Konten im Kerberos-Bereich anmelden.

Das Kerberos 5-Protokoll ist die Standardeinstellung für die Netzwerk Authentifizierung auf Computern, auf denen Windows XP Professional, Windows Vista und Windows 7 ausgeführt wird. Der Kerberos-SSP durchsucht die Registrierung nach dem Domänen Namen des Bereichs des Benutzers und löst dann den Namen in eine IP-Adresse auf, indem er einen DNS-Server abfragt. Das Kerberos-Protokoll kann DNS zum Auffinden von KDCs mithilfe des Bereichs namens verwenden, muss jedoch speziell dafür konfiguriert werden.

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)