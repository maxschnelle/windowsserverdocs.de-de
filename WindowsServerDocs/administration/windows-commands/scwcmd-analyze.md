---
title: Scwcmd-Analyse
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0259271b-be5b-48d7-a51d-8b9b6786efb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 017363ff2a60f9348290813c357560fe9fe3ba2a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722158"
---
# <a name="scwcmd-analyze"></a>Scwcmd: analyze

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Bestimmt, ob ein Computer mit einer Richtlinie konform ist. Die Ergebnisse werden in einer XML-Datei zurückgegeben. Akzeptiert auch eine Liste von Computernamen als Eingabe. Um die Ergebnisse in Ihrem Browser anzuzeigen, verwenden Sie die **scwcmd-Ansicht** , und geben Sie **%windir%\security\msscw\transformfiles\scwanalysis.xsl** als XSL-Transformation an.

## <a name="syntax"></a>Syntax

```
scwcmd analyze [[[/m:<ComputerName> | /ou:<Ou>] /p:<Policy>] | /i:<ComputerList>] [/o:
<ResultDir>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>] [/l] [/e]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/m:\<Computername>|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse des zu analysierenden Computers an. Wenn der **/m** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden.|
|/OU:\<OUNAME>|Gibt den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) einer Organisationseinheit (OE) in Active Directory Domain Services an. Wenn der **/OU** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. Alle Computer in der Organisationseinheit werden anhand der angegebenen Richtlinie analysiert.|
|/p:\<Richtlinien>|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die zum Durchführen der Analyse verwendet werden soll.|
|/i:\<Computer List>|Gibt den Pfad und den Dateinamen einer XML-Datei an, die eine Liste von Computern sowie die erwarteten Richtlinien Dateien enthält. Alle Computer in der XML-Datei werden anhand ihrer entsprechenden Richtlinien Dateien analysiert. Eine XML-Beispieldatei ist%windir%\Security\SampleMachineList.Xml.|
|/o:\<resultdir->|Gibt den Pfad und das Verzeichnis an, in dem die Analyseergebnis Dateien gespeichert werden sollen. Der Standardwert ist das aktuelle Verzeichnis.|
|/u:\<username->|Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Analyse auf einem Remote Computer verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/PW:\<Kennwort>|Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Analyse auf einem Remote Computer verwendet werden sollen. Der Standardwert ist das Kennwort des angemeldeten Benutzers.|
|/t:\<Threads>|Gibt die Anzahl von gleichzeitigen ausstehenden Analyse Vorgängen an, die während der Analyse gewartet werden sollen (DefaultValue = 40, MinValue = 1, MaxValue = 1000).|
|/l|Bewirkt, dass der Analyseprozess protokolliert wird. Für jeden Computer, der analysiert wird, wird eine Protokolldatei generiert. Die Protokolldateien werden im selben Verzeichnis wie die Ergebnisdateien gespeichert. Verwenden Sie die Option **/o** , um das Verzeichnis für die Ergebnisdateien anzugeben.|
|/e|Protokolliert ein Ereignis im Anwendungs Ereignisprotokoll, wenn keine Übereinstimmung gefunden wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei webpolicy. XML zu analysieren:
```
scwcmd analyze /p:webpolicy.xml

```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf dem Computer mit dem Namen Webserver für die Datei webpolicy. XML mithilfe der Anmelde Informationen des webadmin-Kontos zu analysieren:
```
scwcmd analyze /m:webserver /p:webpolicy.xml /u:webadmin

```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei "webpolicy. xml" mit maximal 100 Threads zu analysieren und die Ergebnisse in eine Datei mit dem Namen "Results" in der resultserver-Freigabe auszugeben:
```
scwcmd analyze /i:webpolicy.xml /t:100 /o:\\resultserver\results

```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Webserver-Organisationseinheit mit der Datei "webpolicy. xml" zu analysieren
```
scwcmd analyze /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)