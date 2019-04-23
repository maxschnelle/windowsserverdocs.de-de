---
title: ksetup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0194cf81d069d7a5c1223f0a514d593e4870d397
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868841"
---
# <a name="ksetup"></a>ksetup



Führt Aufgaben aus, die im Zusammenhang mit einrichten und Verwalten von Kerberos-Protokoll und das Schlüsselverteilungscenter (KDC) zur Unterstützung von Kerberos-Bereiche, die nicht auch die Windows-Domänen sind. Beispiele wie dieser Befehl verwendet werden kann finden Sie im Abschnitt "Beispiele" in den einzelnen zugehörigen Unterthemen.

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

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[Ksetup:setrealm](ksetup-setrealm.md)|Wird dieser Computer Mitglied einer Kerberos-Bereich.|
|[Ksetup:mapuser](ksetup-mapuser.md)|Ordnet einen Kerberos-Prinzipal mit einem Konto an.|
|[Ksetup:addkdc](ksetup-addkdc.md)|Definiert einen KDC-Eintrag für den angegebenen Bereich.|
|[Ksetup:delkdc](ksetup-delkdc.md)|Löscht einen KDC-Eintrag für den Bereich an.|
|[Ksetup:addkpasswd](ksetup-addkpasswd.md)|Fügt eine Kpasswd-Serveradresse für einen Bereich hinzu.|
|[Ksetup:delkpasswd](ksetup-delkpasswd.md)|Löscht eine Kpasswd-Serveradresse für einen Bereich an.|
|[Ksetup:server](ksetup-server.md)|Ermöglicht Ihnen die Angabe der Name eines Windows-Computers, auf dem die Änderungen zu übernehmen.|
|[Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)|Legt das Kennwort für den Computer des Domäne-Konto (oder Hostprinzipal).|
|[Ksetup:removerealm](ksetup-removerealm.md)|Löscht alle Informationen für den angegebenen Bereich aus der Registrierung.|
|[Ksetup:domain](ksetup-domain.md)|Ermöglicht Ihnen die Angabe eine Domäne (Wenn \<DomainName > wurde nicht festgelegt wurde, mithilfe von **/Domain**).|
|[Ksetup:changepassword](ksetup-changepassword.md)|Können Sie die Kpasswd verwenden, um das Kennwort des angemeldeten Benutzers zu ändern.|
|[Ksetup:listrealmflags](ksetup-listrealmflags.md)|Listet die verfügbaren Bereich kennzeichnet, **Ksetup** erkennen können.|
|[Ksetup:setrealmflags](ksetup-setrealmflags.md)|Realm-Flags für einen bestimmten Bereich festgelegt.|
|[Ksetup:addrealmflags](ksetup-addrealmflags.md)|Fügt zusätzliche Realm-Flags in einen Bereich hinzu.|
|[Ksetup:delrealmflags](ksetup-delrealmflags.md)|Bereich Flags aus einem Bereich gelöscht.|
|[Ksetup:dumpstate](ksetup-dumpstate.md)|Analysiert die Kerberos-Konfiguration auf dem angegebenen Computer an. Fügt einen Host für die Zuordnung der Bereich der Registrierung hinzu.|
|[Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)|Fügt einen Registrierungswert, um den Host in den Kerberos-Bereich zuzuordnen.|
|[Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)|Löscht den Wert des Registrierungsschlüssels, der den Hostcomputer der Kerberos-Bereich zugeordnet.|
|[Ksetup:setenctypeattr](ksetup-setenctypeattr.md)|Legt eine oder mehrere Verschlüsselungstypen Trust-Attribute für die Domäne fest.|
|[Ksetup:getenctypeattr](ksetup-getenctypeattr.md)|Ruft die Encryption-Typen-Trust-Attribut für die Domäne ab.|
|[Ksetup:addenctypeattr](ksetup-addenctypeattr.md)|Verschlüsselungstypen und die Verschlüsselung Typen Trust-Attribut für die Domäne hinzugefügt.|
|[Ksetup:delenctypeattr](ksetup-delenctypeattr.md)|Löscht die Verschlüsselung Typen Trust-Attribut für die Domäne.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

**Ksetup** wird verwendet, um die Einstellungen des Computers zu ändern, für die Suche nach Kerberos-Bereiche. In nicht-Microsoft Kerberos-basierte Implementierungen bleibt diese Informationen in der Regel in der Datei Krb5.conf. In Windows Server-Betriebssysteme ist es in der Registrierung gespeichert. Sie können dieses Tool verwenden, um diese Einstellungen zu ändern. Diese Einstellungen dienen Arbeitsstationen Kerberos-Bereiche zu finden und von Domänencontrollern, um Kerberos-Bereiche für bereichsübergreifende Vertrauensstellung Beziehungen zu suchen.

**Ksetup** initialisiert, die die Kerberos-Security Support Provider (SSP) verwendet, um einen KDC-Dienst für die Kerberos-Bereich zu suchen, wenn der Computer Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, und nicht Mitglied einer Windows ist-Registrierungsschlüssel die Domäne. Nach der Konfiguration der Kerberos-Bereich-Konten der Benutzer von einem Clientcomputer, die dem Windows ausgeführt wird, sich beim Betriebssystem anmelden können.

Das Kerberos V5-Protokoll ist der Standardwert für die Netzwerkauthentifizierung auf Computern unter Windows XP Professional, Windows Vista und Windows 7. Der Kerberos-SSP durchsucht die Registrierung für den Domänennamen des Bereichs des Benutzers darstellt, und löst dann den Namen einer IP-Adresse durch einen DNS-Server Abfragen. Das Kerberos-Protokoll kann DNS verwenden, um KDCs suchen mit nur den Bereichsnamen, jedoch müssen speziell zu diesem Zweck konfigurieren.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)