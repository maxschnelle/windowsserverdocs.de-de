---
title: Scwcmd analysieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0259271b-be5b-48d7-a51d-8b9b6786efb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cce3428b281ede582ed781afbdee9dea495b52ae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873911"
---
# <a name="scwcmd-analyze"></a>scwcmd: analyze

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Bestimmt, ob ein Computer mit der eine Richtlinie konform ist. Ergebnisse werden in eine XML-Datei zurückgegeben. Eine Liste mit Computernamen werden auch als Eingabe akzeptiert. Verwenden Sie zum Anzeigen der Ergebnisse in Ihrem Browser **Scwcmd-Ansicht** , und geben Sie **%windir%\security\msscw\TransformFiles\scwanalysis.xsl** als die XSL-Transformation. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
scwcmd analyze [[[/m:<ComputerName> | /ou:<Ou>] /p:<Policy>] | /i:<ComputerList>] [/o:
<ResultDir>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>] [/l] [/e]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m:\<ComputerName>|Gibt an, den NetBIOS-Namen, die DNS-Namen oder die IP-Adresse des zu analysierenden Computers an. Wenn die **/m** Parameter angegeben wird, und klicken Sie dann die **/p** Parameter muss auch angegeben werden.|
|/ou:\<OuName>|Gibt den vollqualifizierten Domänennamen (FQDN) von einer Organisationseinheit (OU) in Active Directory Domain Services an. Wenn die **OU** Parameter angegeben wird, und klicken Sie dann die **/p** Parameter muss auch angegeben werden. Alle Computer in der Organisationseinheit werden anhand der angegebenen Richtlinie analysiert werden.|
|/ p:\<Richtlinie >|Gibt an, der Pfad und Dateiname der XML-Richtliniendatei zum Durchführen der Analyse verwendet werden.|
|/i:\<ComputerList>|Gibt an, der Pfad und Dateiname einer XML-Datei, die eine Liste von Computern sowie deren erwartete Richtliniendateien enthält. Alle Computer in der XML-Datei werden für die entsprechende Richtliniendateien analysiert werden. Eine Beispiel-XML-Datei ist % windir%\security\SampleMachineList.xml.|
|/o:\<ResultDir>|Gibt den Pfad und das Verzeichnis, in die Ergebnisdateien der Analyse gespeichert werden soll. Der Standardwert ist das aktuelle Verzeichnis.|
|/ u:\<Benutzername >|Gibt einen alternativen Benutzeranmeldeinformationen, die beim Durchführen der Analysis auf einem Remotecomputer verwenden. Der Standardwert ist der angemeldete Benutzer.|
|PW:\<Kennwort >|Gibt einen alternativen Benutzeranmeldeinformationen, die beim Durchführen der Analysis auf einem Remotecomputer verwenden. Der Standardwert ist das Kennwort des angemeldeten Benutzers.|
|/t:\<Threads>|Gibt die Anzahl der gleichzeitigen ausstehenden Analysevorgänge, die während der Analyse beibehalten werden soll (Standardwert = 40 "," MinValue = 1, MaxValue = 1000).|
|/l|Bewirkt, dass den Analyseprozess protokolliert werden. Für jeden Computer, die analysiert werden eine Protokolldatei generiert. Die Protokolldateien werden im gleichen Verzeichnis wie die Ergebnisdateien gespeichert werden. Verwenden der **/o** verwenden, um das Verzeichnis für die Dateien anzugeben.|
|/ e|Wenn ein Konflikt vorliegt, wird protokollieren Sie ein Ereignis in das Anwendungsereignisprotokoll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Um eine Sicherheitsrichtlinie für die Datei webpolicy.xml zu analysieren, geben Sie Folgendes ein:
```
scwcmd analyze /p:webpolicy.xml

```
Um eine Sicherheitsrichtlinie auf dem Computer mit dem Namen der Webserver für die Datei webpolicy.xml mithilfe der Anmeldeinformationen des Kontos Webadmin zu analysieren, geben Sie Folgendes ein:
```
scwcmd analyze /m:webserver /p:webpolicy.xml /u:webadmin

```
Um eine Sicherheitsrichtlinie für die webpolicy.xml Datei mit einem Maximum von 100 Threads analysieren und die Ergebnisse in eine Datei namens "Results" in der Freigabe Resultserver, geben Sie Folgendes ein:
```
scwcmd analyze /i:webpolicy.xml /t:100 /o:\\resultserver\results

```
Um eine Sicherheitsrichtlinie für die OU WebServers für die Datei webpolicy.xml mithilfe der Anmeldeinformationen DomainAdmin analysieren möchten, geben Sie Folgendes ein:
```
scwcmd analyze /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)