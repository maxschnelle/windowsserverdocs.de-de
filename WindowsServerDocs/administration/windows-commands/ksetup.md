---
title: ksetup
description: Referenz Thema für den Ksetup-Befehl, der Aufgaben im Zusammenhang mit der Einrichtung und Wartung des Kerberos-Protokolls und der Schlüsselverteilungscenter (KDC) zur Unterstützung von Kerberos-Bereichen ausführt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82b1627a8ddbc9e51ac32825c5a42c3df9effbf7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817350"
---
# <a name="ksetup"></a>ksetup

Führt Aufgaben im Zusammenhang mit der Einrichtung und Wartung des Kerberos-Protokolls und der Schlüsselverteilungscenter (KDC) zur Unterstützung von Kerberos-Bereichen aus. Der folgende Befehl wird speziell für Folgendes verwendet:

- Ändern Sie die Computereinstellungen für das Suchen von Kerberos-Bereichen. In Kerberos – basierten Implementierungen, die nicht von Microsoft sind, werden diese Informationen in der Regel in der Datei krb5. conf gespeichert. In Windows Server-Betriebssystemen wird es in der Registrierung gespeichert. Sie können dieses Tool verwenden, um diese Einstellungen zu ändern. Diese Einstellungen werden von Arbeitsstationen zum Suchen von Kerberos-Bereichen und von Domänen Controllern verwendet, um Kerberos-Bereiche für bereichsübergreifende Vertrauens Stellungen zu finden.

- Initialisieren Sie die Registrierungsschlüssel, die der Kerberos-Security Support Provider (SSP) zum Suchen eines KDC für den Kerberos-Bereich verwendet, wenn der Computer kein Mitglied einer Windows-Domäne ist. Nach der Konfiguration kann sich der Benutzer eines Client Computers, auf dem das Windows-Betriebssystem ausgeführt wird, bei Konten im Kerberos-Bereich anmelden.

- Durchsuchen Sie die Registrierung nach dem Domänen Namen des Bereichs des Benutzers, und lösen Sie dann den Namen in eine IP-Adresse, indem Sie einen DNS-Server Abfragen. Das Kerberos-Protokoll kann DNS zum Auffinden von KDCs mithilfe des Bereichs namens verwenden, muss jedoch speziell dafür konfiguriert werden.

## <a name="syntax"></a>Syntax

```
ksetup
[/setrealm <DNSdomainname>]
[/mapuser <principal> <account>]
[/addkdc <realmname> <KDCname>]
[/delkdc <realmname> <KDCname>]
[/addkpasswd <realmname> <KDCPasswordName>]
[/delkpasswd <realmname> <KDCPasswordName>]
[/server <servername>]
[/setcomputerpassword <password>]
[/removerealm <realmname>]
[/domain <domainname>]
[/changepassword <oldpassword> <newpassword>]
[/listrealmflags]
[/setrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/dumpstate]
[/addhosttorealmmap] <hostname> <realmname>]
[/delhosttorealmmap] <hostname> <realmname>]
[/setenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <domainname>
[/addenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [Ksetup setrealm](ksetup-setrealm.md) | Dieser Computer ist ein Mitglied eines Kerberos-Bereichs. |
| [Ksetup-addkdc](ksetup-addkdc.md) | Definiert einen KDC-Eintrag für den angegebenen Bereich. |
| [Ksetup-Delta Controller](ksetup-delkdc.md) | Löscht einen KDC-Eintrag für den Bereich. |
| [Ksetup addkpasswd](ksetup-addkpasswd.md) | Fügt eine kpasswd-Server Adresse für einen Bereich hinzu. |
| [Ksetup-Delta Pass WD](ksetup-delkpasswd.md) | Löscht eine kpasswd-Server Adresse für einen Bereich. |
| [Ksetup-Server](ksetup-server.md) | Ermöglicht es Ihnen, den Namen eines Windows-Computers anzugeben, auf dem die Änderungen angewendet werden sollen. |
| [Ksetup setcomputerpassword](ksetup-setcomputerpassword.md) | Legt das Kennwort für das Domänen Konto des Computers (oder den Host Prinzipal) fest. |
| [Ksetup removerealm](ksetup-removerealm.md) | Löscht alle Informationen für den angegebenen Bereich aus der Registrierung. |
| [Ksetup-Domäne](ksetup-domain.md) | Ermöglicht das Angeben einer Domäne (wenn das `<domainname>` nicht bereits durch den **/Domain** -Parameter festgelegt wurde). |
| [Kennwort für Ksetup](ksetup-changepassword.md) | Ermöglicht die Verwendung von kpasswd zum Ändern des Kennworts des angemeldeten Benutzers. |
| [Ksetup listrealmflags](ksetup-listrealmflags.md) | Listet die verfügbaren bereichflags auf, die von **Ksetup** erkannt werden können. |
| [ksetup setrealmflags](ksetup-setrealmflags.md) | Legt bereichflags für einen bestimmten Bereich fest. |
| [Ksetup-adressalm-Flags](ksetup-addrealmflags.md) | Fügt einem Bereich weitere bereichflags hinzu. |
| [Ksetup-Delta Flags](ksetup-delrealmflags.md) | Löscht bereichflags aus einem Bereich. |
| [Ksetup dumpstate](ksetup-dumpstate.md) | Analysiert die Kerberos-Konfiguration auf dem angegebenen Computer. Fügt der Registrierung einen Host für die Bereichs Zuordnung hinzu. |
| [Ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md) | Fügt einen Registrierungs Wert hinzu, um den Host dem Kerberos-Bereich zuzuordnen. |
| [Ksetup Delta Host-Karte](ksetup-delhosttorealmmap.md) | Löscht den Registrierungs Wert, der den Host Computer dem Kerberos-Bereich zugeordnet hat. |
| [Ksetup setenctypeattr](ksetup-setenctypeattr.md) | Legt ein oder mehrere Vertrauens Attribute der Verschlüsselungstypen für die Domäne fest. |
| [Ksetup getenctypeattr](ksetup-getenctypeattr.md) | Ruft das Vertrauens Attribut der Verschlüsselungstypen für die Domäne ab. |
| [Ksetup addenctypeattr](ksetup-addenctypeattr.md) | Fügt Verschlüsselungstypen zum Vertrauens Attribut der Verschlüsselungstypen für die Domäne hinzu. |
| [Ksetup-Delta TYPEATTR](ksetup-delenctypeattr.md) | Löscht das Vertrauens Attribut der Verschlüsselungstypen für die Domäne. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)