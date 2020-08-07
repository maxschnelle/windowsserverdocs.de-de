---
title: prnport
description: Referenz Artikel zum prnport-Befehl, der die TCP/IP-Standarddrucker Anschlüsse erstellt, löscht und auflistet, zusätzlich zum Anzeigen und Ändern der Port Konfiguration.
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8aa1729c84b54393a6154dd5fc4ba5a5e6834fc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884700"
---
# <a name="prnport"></a>prnport

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden standardmäßige TCP/IP-Drucker Anschlüsse erstellt, gelöscht und aufgelistet, zusätzlich zum Anzeigen und Ändern der Port Konfiguration. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad der prnport-Datei ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport`.

## <a name="syntax"></a>Syntax

```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <portname>] [-s <Servername>] [-u <Username>] [-w <password>] [-o {raw | lpr}] [-h <Hostaddress>] [-q <Queuename>] [-n <portnumber>] -m{e | d} [-i <SNMPindex>] [-y <communityname>] -2{e | -d}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -a | Erstellt einen standardmäßigen TCP/IP-Druckerport. |
| -d | Löscht einen standardmäßigen TCP/IP-Druckerport. |
| -l | Listet alle standardmäßigen TCP/IP-Drucker Anschlüsse auf dem Computer auf, der durch den **-s-** Parameter angegeben wird. |
| -g | Hiermit wird die Konfiguration eines standardmäßigen TCP/IP-Drucker Ports angezeigt. |
| -t | Konfiguriert die Port Einstellungen für einen Standard-TCP/IP-Druckerport. |
| -r`<portname>` | Gibt den Port an, mit dem der Drucker verbunden ist. |
| -s `<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -u `<Username>` -w`<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| -o`{raw|lpr}` | Gibt an, welches Protokoll der Port verwendet: TCP-RAW oder TCP LPR. Das TCP-RAW-Protokoll ist ein höheres Leistungs Protokoll unter Windows als das lpr-Protokoll. Wenn Sie TCP RAW verwenden, können Sie optional die Portnummer angeben, indem Sie den Parameter **-n** verwenden. Die Standard Portnummer ist 9100. |
| -h`<Hostaddress>` | Gibt (nach IP-Adresse) den Drucker an, für den Sie den Port konfigurieren möchten. |
| -q`<Queuename>` | Gibt den Warteschlangen Namen für einen TCP-rohport an. |
| -n`<portnumber>` | Gibt die Portnummer für einen TCP-rohport an. Die Standard Portnummer ist 9100. |
| -m`{e|d}` | Gibt an, ob SNMP aktiviert ist. Der Parameter **e** aktiviert SNMP. Der Parameter **d** deaktiviert SNMP. |
| -i`<SNMPindex` | Gibt den SNMP-Index an, wenn SNMP aktiviert ist. Weitere Informationen finden Sie unter **RFC 1759** auf der [RFC-Editor-Website](https://www.ietf.org/rfc/rfc1759.txt?number=1759). |
| -y`<communityname>` | Gibt den SNMP-Communitynamen an, wenn SNMP aktiviert ist. |
| -2`{e|-d}` | Gibt an, ob doppelte Spool (auch als "respoolung" bezeichnet) für TCP LPR-Ports aktiviert sind. Doppelte Spool sind erforderlich, da TCP LPR eine genaue Byte Anzahl in der Steuerungs Datei enthalten muss, die an den Drucker gesendet wird, aber das Protokoll kann die Anzahl nicht vom lokalen Druckanbieter erhalten. Wenn eine Datei in eine TCP LPR-Druck Warteschlange gestellt wird, wird Sie daher auch als temporäre Datei im Verzeichnis "System32" gespoolt. TCP LPR bestimmt die Größe der temporären Datei und sendet die Größe an den Server, auf dem LPD ausgeführt wird. Der Parameter **e** aktiviert doppelte spools. Der Parameter **d** deaktiviert doppelte spools. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

### <a name="examples"></a>Beispiele

Wenn Sie alle standardmäßigen TCP/IP-druckports auf dem Server Server1 anzeigen möchten, geben Sie Folgendes ein \\ :

```
cscript prnport -l -s Server1
```

Geben Sie Folgendes ein, um den standardmäßigen TCP/IP-druckport auf dem Server zu löschen server1 der eine Verbindung mit \\ einem Netzwerkdrucker unter 10.2.3.4 herstellt:

```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```

Um einen standardmäßigen TCP/IP-druckport auf dem Server hinzuzufügen server1 der eine Verbindung \\ mit einem Netzwerkdrucker unter 10.2.3.4 herstellt und das TCP-RAW-Protokoll an Port 9100 verwendet, geben Sie Folgendes ein:

```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```

Um SNMP zu aktivieren, geben Sie den öffentlichen Namen der Community an, und legen Sie den SNMP-Index auf einem Netzwerkdrucker bei 10.2.3.4, der vom Server verwendet wird Server1 auf 1 fest. Geben Sie Folgendes ein \\ :

```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```

Um einen standardmäßigen TCP/IP-druckport auf dem lokalen Computer hinzuzufügen, der unter 10.2.3.4 eine Verbindung mit einem Netzwerkdrucker herstellt und automatisch die Geräteeinstellungen vom Drucker erhält, geben Sie Folgendes ein:

```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
