---
title: prnport
description: Informationen Sie zum Erstellen, löschen und Auflisten von Druckeranschlüsse.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: eb6ef7632c10217c4fdf114d4e67c8bc52be07e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856891"
---
# <a name="prnport"></a>prnport

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Erstellt, löscht und standard-TCP/IP-Drucker-Ports zusätzlich zum Anzeigen und Ändern der Portkonfiguration aufgeführt.

## <a name="syntax"></a>Syntax
```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <PortName>] 
[-s <ServerName>] [-u <UserName>] [-w <Password>] [-o {raw | lpr}] 
[-h <Hostaddress>] [-q <QueueName>] [-n <PortNumber>] -m{e | d} 
[-i <SNMPIndex>] [-y <CommunityName>] -2{e | -d}
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-a|erstellt einen standardmäßigen TCP/IP-Druckeranschluss.|
|-d|Löscht einen standardmäßigen TCP/IP-Druckeranschluss.|
|-l|Listet alle standardmäßigen TCP/IP Druckeranschlüsse auf dem Computer, die mit angegebenen die **-s** Parameter.|
|-g|Zeigt die Konfiguration der einen standardmäßigen TCP/IP-Druckeranschluss.|
|-t|Konfiguriert die Porteinstellungen für einen standardmäßigen TCP/IP-Druckeranschluss.|
|-R \<PortName >|Gibt den Port, den der Drucker angeschlossen ist.|
|-s \<ServerName >|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|-u \<UserName > -w <Password>|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|
|-o {raw &#124; Lpr}|Gibt an, welches Protokoll der Ports verwendet: TCP-raw oder TCP-Lpr. Bei Verwendung von TCP-raw können Sie optional die Portnummer angeben, indem Sie mit der **- n** Parameter. Die Standardportnummer ist 9100.|
|-h \<Hostaddress>|Gibt an (von IP-Adresse) der Drucker, für den Sie den Port konfigurieren möchten.|
|-q \<QueueName>|Gibt den Warteschlangennamen für einen unformatierten TCP-Port.|
|-n: \<PortNumber >|Gibt die Portnummer für einen raw-TCP-Port an. Die Standardportnummer ist 9100.|
|-m{e &#124; d}|Gibt an, ob SNMP aktiviert ist. Der Parameter **e** SNMP ermöglicht. Der Parameter **d** SNMP deaktiviert.|
|-i \<SNMPIndex|Gibt die SNMP-Index, an, wenn SNMP aktiviert ist. Weitere Informationen finden Sie unter Rfc 1759 in die [Rfc-Editor-Website](https://go.microsoft.com/fwlink/?LinkId=569).|
|/ y \<CommunityName >|Gibt die SNMP-Communitynamen an, wenn SNMP aktiviert ist.|
|-2{e &#124; -d}|Gibt an, ob doppelte spoolvorgänge (auch bekannt als erneutes Spoolen) für Lpr-Ports TCP aktiviert sind. Doppeltes Spoolen ist notwendig, da TCP-Lpr eine exakte Bytezahl in die Benutzersteuerelement-Datei aufnehmen muss, die an den Drucker gesendet wird, aber das Protokoll die Anzahl die vom lokalen Druckanbieter kann nicht abgerufen werden. Aus diesem Grund wird eine Datei gespoolt werden in einem TCP Lpr Warteschlange gedruckt werden, ist auch gespoolt als temporäre Datei im Verzeichnis "System32". TCP-Lpr bestimmt die Größe der temporären Datei und sendet die Größe auf den Server mit LPD. Der Parameter **e** doppelte Spoolen aktiviert. Der Parameter **d** doppelte Spoolen deaktiviert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Prnport** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die Prnport-Datei, oder wechseln in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).
-   Das raw-TCP-Protokoll ist ein höherer Leistung-Protokoll für Windows als den Lpr-Protokoll.

## <a name="BKMK_examples"></a>Beispiele für
Alle standardmäßigen drucken TCP/IP-Ports anzuzeigen, auf dem Server \\\Server1, Typ:
```
cscript prnport -l -s Server1
```
So löschen Sie die standard-TCP/IP-Drucken-Port auf dem Server \\\Server1 die Verbindung mit einem Netzwerkdrucker auf 10.2.3.4, Typ:
```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```
Um einen standardmäßigen TCP/IP-Druckeranschluss auf dem Server hinzufügen \\\Server1, die eine Verbindung mit einem Netzwerkdrucker auf 10.2.3.4 her und verwendet das raw-TCP-Protokoll auf Port 9100, Typ:
```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```
Um SNMP zu aktivieren, geben Sie den "öffentlich" Communitynamen und den SNMP-Index auf 1 festgelegt, auf einem Netzwerkdrucker auf 10.2.3.4 durch den Server freigegeben \\\Server1, Typ:
```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```
Um einen standardmäßigen TCP/IP-Druckeranschluss auf dem lokalen Computer hinzuzufügen, die eine Verbindung mit einem Netzwerkdrucker auf 10.2.3.4 her, und erhalten automatisch die Einstellungen für Geräte vom Drucker, geben Sie Folgendes ein:
```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
