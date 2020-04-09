---
title: Scwcmd konfigurieren
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6528b9dc-3d82-4228-b734-ed717458d74c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac4333628c33b60daabbb6cff55575d6ec8cd5f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835183"
---
# <a name="scwcmd-configure"></a>scwcmd: configure

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet eine Sicherheitsrichtlinie, die vom Sicherheitskonfigurations-Assistenten (SCW) generiert wurde, auf einen Computer an. Dieses Befehlszeilen Tool akzeptiert auch eine Liste von Computernamen als Eingabe.

## <a name="syntax"></a>Syntax

```
scwcmd configure [[[/m:<ComputerName> | /ou:<OuName>] /p:<Policy>] | /i:<ComputerList>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m:\<Computername >|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse des zu konfigurierenden Computers an. Wenn der **/m** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden.|
|/OU:\<OUNAME >|Gibt den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) einer Organisationseinheit (OE) in Active Directory Domain Services an. Wenn der **/OU** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. Alle Computer in der Organisationseinheit werden gemäß der angegebenen Richtlinie analysiert.|
|/p:\<Richtlinien >|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die zum Ausführen der Konfiguration verwendet werden soll.|
|/i:\<Computer List >|Gibt den Pfad und den Dateinamen einer XML-Datei an, die eine Liste von Computern sowie die erwarteten Richtlinien Dateien enthält. Alle Computer in der XML-Datei werden entsprechend den entsprechenden Richtlinien Dateien konfiguriert. Eine XML-Beispieldatei ist%windir%\Security\SampleMachineList.Xml.|
|/u:\<Benutzername >|Gibt alternative Benutzer Anmelde Informationen an, die beim Konfigurieren eines Remote Computers verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/PW:\<Kennwort >|Gibt alternative Benutzer Anmelde Informationen an, die beim Konfigurieren eines Remote Computers verwendet werden sollen. Der Standardwert ist das Kennwort des angemeldeten Benutzers.|
|/t:\<Threads >|Gibt die Anzahl von gleichzeitigen ausstehenden Konfigurations Vorgängen an, die während des Konfigurationsprozesses (DefaultValue = 40, MinValue = 1, MaxValue = 1000) beibehalten werden sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd. exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei "webpolicy. xml" zu konfigurieren:
```
scwcmd configure /p:webpolicy.xml
```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für den Computer unter 172.16.0.0 für die Datei webpolicy. XML mithilfe der Anmelde Informationen für das webadmin-Konto zu konfigurieren:
```
scwcmd configure /m:172.16.0.0 /p:webpolicy.xml /u:webadmin
```
Um eine Sicherheitsrichtlinie auf allen Computern in der Liste "campusmachines. xml" mit maximal 100 Threads zu konfigurieren, geben Sie Folgendes ein:
```
scwcmd configure /i:campusmachines.xml /t:100
```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf allen Computern in der Organisationseinheit Webservers mithilfe der Anmelde Informationen des DomainAdmin-Kontos für die Datei "webpolicy. xml" zu konfigurieren:
```
scwcmd configure /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)