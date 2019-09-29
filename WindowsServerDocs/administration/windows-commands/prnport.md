---
title: prnport
description: Erfahren Sie, wie Sie Drucker Anschlüsse erstellen, löschen und auflisten.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9c162cef2a3ae2f3de1e891691572130ae68f93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372553"
---
# <a name="prnport"></a>prnport

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit werden standardmäßige TCP/IP-Drucker Anschlüsse erstellt, gelöscht und aufgelistet, zusätzlich zum Anzeigen und Ändern der Port Konfiguration.

## <a name="syntax"></a>Syntax
```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <PortName>] 
[-s <ServerName>] [-u <UserName>] [-w <Password>] [-o {raw | lpr}] 
[-h <Hostaddress>] [-q <QueueName>] [-n <PortNumber>] -m{e | d} 
[-i <SNMPIndex>] [-y <CommunityName>] -2{e | -d}
```

## <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                                                                                                                                                                                     Beschreibung                                                                                                                                                                                                                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -a              |                                                                                                                                                                                                                                                                                       erstellt einen standardmäßigen TCP/IP-Druckerport.                                                                                                                                                                                                                                                                                        |
|              -d              |                                                                                                                                                                                                                                                                                       Löscht einen standardmäßigen TCP/IP-Druckerport.                                                                                                                                                                                                                                                                                        |
|              -l              |                                                                                                                                                                                                                                                             Listet alle standardmäßigen TCP/IP-Drucker Anschlüsse auf dem Computer auf, der mit dem Parameter **-s** angegeben wird.                                                                                                                                                                                                                                                             |
|              -g              |                                                                                                                                                                                                                                                                            Hiermit wird die Konfiguration eines standardmäßigen TCP/IP-Drucker Ports angezeigt.                                                                                                                                                                                                                                                                             |
|              -t              |                                                                                                                                                                                                                                                                           Konfiguriert die Port Einstellungen für einen Standard-TCP/IP-Druckerport.                                                                                                                                                                                                                                                                           |
|        -r \<portname >        |                                                                                                                                                                                                                                                                                Gibt den Port an, mit dem der Drucker verbunden ist.                                                                                                                                                                                                                                                                                 |
|       -s \<servername >       |                                                                                                                                                                                                                               Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.                                                                                                                                                                                                                                |
| -u \<username >-w <Password> |                                                                                                              Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.                                                                                                               |
|     -o {RAW &#124; LPR}      |                                                                                                                                                                                                              Gibt an, welches Protokoll der Port verwendet: TCP-Rohdaten oder TCP-LPR. Wenn Sie TCP RAW verwenden, können Sie optional die Portnummer angeben, indem Sie den Parameter **-n** verwenden. Die Standard Portnummer ist 9100.                                                                                                                                                                                                              |
|      -h \<hustaddress >       |                                                                                                                                                                                                                                                                   Gibt (nach IP-Adresse) den Drucker an, für den Sie den Port konfigurieren möchten.                                                                                                                                                                                                                                                                    |
|       -q \<queuename >        |                                                                                                                                                                                                                                                                                     Gibt den Warteschlangen Namen für einen TCP-rohport an.                                                                                                                                                                                                                                                                                     |
|       -n \<portnumber >       |                                                                                                                                                                                                                                                                    Gibt die Portnummer für einen TCP-rohport an. Die Standard Portnummer ist 9100.                                                                                                                                                                                                                                                                    |
|        -m {e &#124; d}        |                                                                                                                                                                                                                                                       Gibt an, ob SNMP aktiviert ist. Der Parameter **e** aktiviert SNMP. Der Parameter **d** deaktiviert SNMP.                                                                                                                                                                                                                                                        |
|        -i \<snmpindex        |                                                                                                                                                                                                                             Gibt den SNMP-Index an, wenn SNMP aktiviert ist. Weitere Informationen finden Sie unter RFC 1759 auf der [RFC-Editor](https://go.microsoft.com/fwlink/?LinkId=569)-Website.                                                                                                                                                                                                                              |
|     -y \<communityname >      |                                                                                                                                                                                                                                                                                Gibt den SNMP-Communitynamen an, wenn SNMP aktiviert ist.                                                                                                                                                                                                                                                                                |
|       -2 {e &#124; -d}        | Gibt an, ob doppelte Spool (auch als "respoolung" bezeichnet) für TCP LPR-Ports aktiviert sind. Doppelte Spool sind erforderlich, da TCP LPR eine genaue Byte Anzahl in der Steuerungs Datei enthalten muss, die an den Drucker gesendet wird, aber das Protokoll kann die Anzahl nicht vom lokalen Druckanbieter erhalten. Wenn eine Datei in eine TCP LPR-Druck Warteschlange gestellt wird, wird Sie daher auch als temporäre Datei im Verzeichnis "System32" gespoolt. TCP LPR bestimmt die Größe der temporären Datei und sendet die Größe an den Server, auf dem LPD ausgeführt wird. Der Parameter **e** aktiviert doppelte spools. Der Parameter **d** deaktiviert doppelte spools. |
|              /?              |                                                                                                                                                                                                                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                         |

## <a name="remarks"></a>Hinweise
-   Der **prnport** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis%WINdir%\System32\printing_Admin_Scripts @ no__t-1 @ no__t-2 befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad der prnport-Datei, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).
-   Das TCP-RAW-Protokoll ist ein höheres Leistungs Protokoll unter Windows als das lpr-Protokoll.

## <a name="BKMK_examples"></a>Beispiele
Wenn Sie alle standardmäßigen TCP/IP-druckports auf dem Server \\ \ Server1 anzeigen möchten, geben Sie Folgendes ein:
```
cscript prnport -l -s Server1
```
Geben Sie Folgendes ein, um den standardmäßigen TCP/IP-druckport auf dem Server \\ \ Server1, der eine Verbindung mit einem Netzwerkdrucker unter 10.2.3.4 herstellt, zu löschen:
```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```
Um einen standardmäßigen TCP/IP-druckport auf dem Server \\ \ Server1 hinzuzufügen, der eine Verbindung mit einem Netzwerkdrucker unter 10.2.3.4 herstellt und das TCP-RAW-Protokoll an Port 9100 verwendet, geben Sie Folgendes ein:
```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```
Um SNMP zu aktivieren, geben Sie den öffentlichen Namen der Community an, und legen Sie den SNMP-Index auf einem Netzwerkdrucker bei 10.2.3.4, der vom Server verwendet wird \\ \ Server1 auf 1 fest. Geben Sie Folgendes ein:
```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```
Um einen standardmäßigen TCP/IP-druckport auf dem lokalen Computer hinzuzufügen, der unter 10.2.3.4 eine Verbindung mit einem Netzwerkdrucker herstellt und automatisch die Geräteeinstellungen vom Drucker erhält, geben Sie Folgendes ein:
```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Druck Befehlsreferenz](print-command-reference.md)
