---
title: prnport
description: Erfahren Sie, wie Sie Drucker Anschlüsse erstellen, löschen und auflisten.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17f81b127927a41e60c290535032876def109989
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837223"
---
# <a name="prnport"></a>prnport

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden standardmäßige TCP/IP-Drucker Anschlüsse erstellt, gelöscht und aufgelistet, zusätzlich zum Anzeigen und Ändern der Port Konfiguration.

## <a name="syntax"></a>Syntax
```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <PortName>] 
[-s <ServerName>] [-u <UserName>] [-w <Password>] [-o {raw | lpr}] 
[-h <Hostaddress>] [-q <QueueName>] [-n <PortNumber>] -m{e | d} 
[-i <SNMPIndex>] [-y <CommunityName>] -2{e | -d}
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                                                                                                                                                                                     Beschreibung                                                                                                                                                                                                                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -a              |                                                                                                                                                                                                                                                                                       erstellt einen standardmäßigen TCP/IP-Druckerport.                                                                                                                                                                                                                                                                                        |
|              -d              |                                                                                                                                                                                                                                                                                       Löscht einen standardmäßigen TCP/IP-Druckerport.                                                                                                                                                                                                                                                                                        |
|              -l              |                                                                                                                                                                                                                                                             Listet alle standardmäßigen TCP/IP-Drucker Anschlüsse auf dem Computer auf, der mit dem Parameter **-s** angegeben wird.                                                                                                                                                                                                                                                             |
|              -g              |                                                                                                                                                                                                                                                                            Hiermit wird die Konfiguration eines standardmäßigen TCP/IP-Drucker Ports angezeigt.                                                                                                                                                                                                                                                                             |
|              -t              |                                                                                                                                                                                                                                                                           Konfiguriert die Port Einstellungen für einen Standard-TCP/IP-Druckerport.                                                                                                                                                                                                                                                                           |
|        -r \<Portname >        |                                                                                                                                                                                                                                                                                Gibt den Port an, mit dem der Drucker verbunden ist.                                                                                                                                                                                                                                                                                 |
|       -s \<Servername >       |                                                                                                                                                                                                                               Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.                                                                                                                                                                                                                                |
| -u \<Benutzername >-w <Password> |                                                                                                              Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.                                                                                                               |
|     -o {RAW &#124; LPR}      |                                                                                                                                                                                                              Gibt an, welches Protokoll der Port verwendet: TCP-RAW oder TCP LPR. Wenn Sie TCP RAW verwenden, können Sie optional die Portnummer angeben, indem Sie den Parameter **-n** verwenden. Die Standard Portnummer ist 9100.                                                                                                                                                                                                              |
|      -h \<Host >       |                                                                                                                                                                                                                                                                   Gibt (nach IP-Adresse) den Drucker an, für den Sie den Port konfigurieren möchten.                                                                                                                                                                                                                                                                    |
|       -q \<QueueName >        |                                                                                                                                                                                                                                                                                     Gibt den Warteschlangen Namen für einen TCP-rohport an.                                                                                                                                                                                                                                                                                     |
|       -n \<portNumber >       |                                                                                                                                                                                                                                                                    Gibt die Portnummer für einen TCP-rohport an. Die Standard Portnummer ist 9100.                                                                                                                                                                                                                                                                    |
|        -m {e &#124; d}        |                                                                                                                                                                                                                                                       Gibt an, ob SNMP aktiviert ist. Der Parameter **e** aktiviert SNMP. Der Parameter **d** deaktiviert SNMP.                                                                                                                                                                                                                                                        |
|        -i \<snmpindex        |                                                                                                                                                                                                                             Gibt den SNMP-Index an, wenn SNMP aktiviert ist. Weitere Informationen finden Sie unter RFC 1759 auf der [RFC-Editor](https://go.microsoft.com/fwlink/?LinkId=569)-Website.                                                                                                                                                                                                                              |
|     -y \<Communityname >      |                                                                                                                                                                                                                                                                                Gibt den SNMP-Communitynamen an, wenn SNMP aktiviert ist.                                                                                                                                                                                                                                                                                |
|       -2 {e &#124; -d}        | Gibt an, ob doppelte Spool (auch als "respoolung" bezeichnet) für TCP LPR-Ports aktiviert sind. Doppelte Spool sind erforderlich, da TCP LPR eine genaue Byte Anzahl in der Steuerungs Datei enthalten muss, die an den Drucker gesendet wird, aber das Protokoll kann die Anzahl nicht vom lokalen Druckanbieter erhalten. Wenn eine Datei in eine TCP LPR-Druck Warteschlange gestellt wird, wird Sie daher auch als temporäre Datei im Verzeichnis "System32" gespoolt. TCP LPR bestimmt die Größe der temporären Datei und sendet die Größe an den Server, auf dem LPD ausgeführt wird. Der Parameter **e** aktiviert doppelte spools. Der Parameter **d** deaktiviert doppelte spools. |
|              /?              |                                                                                                                                                                                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                         |

## <a name="remarks"></a>Hinweise
-   Der **prnport** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\<language>" befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der prnport-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).
-   Das TCP-RAW-Protokoll ist ein höheres Leistungs Protokoll unter Windows als das lpr-Protokoll.

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Wenn Sie alle standardmäßigen TCP/IP-druckports auf dem Server \\\server1 anzeigen möchten, geben Sie Folgendes ein:
```
cscript prnport -l -s Server1
```
Geben Sie Folgendes ein, um den standardmäßigen TCP/IP-druckport auf dem Server \\\server1 zu löschen, der eine Verbindung mit einem Netzwerkdrucker auf 10.2.3.4 herstellt:
```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```
Um einen standardmäßigen TCP/IP-druckport auf dem Server \\\server1 hinzuzufügen, der eine Verbindung mit einem Netzwerkdrucker auf 10.2.3.4 herstellt und das TCP-RAW-Protokoll an Port 9100 verwendet, geben Sie Folgendes ein:
```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```
Um SNMP zu aktivieren, geben Sie den öffentlichen Namen der Community an, und legen Sie den SNMP-Index auf einem Netzwerkdrucker auf 10.2.3.4, der vom Server \\\server1 gemeinsam genutzt wird, auf 1 fest:
```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```
Um einen standardmäßigen TCP/IP-druckport auf dem lokalen Computer hinzuzufügen, der unter 10.2.3.4 eine Verbindung mit einem Netzwerkdrucker herstellt und automatisch die Geräteeinstellungen vom Drucker erhält, geben Sie Folgendes ein:
```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
