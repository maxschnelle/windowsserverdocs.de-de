---
title: Scwcmd konfigurieren
description: Referenz Artikel für * * * *-
ms.topic: reference
ms.assetid: 6528b9dc-3d82-4228-b734-ed717458d74c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54faae6fd24aac91a94ec9ab1f373737569dda78
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89036188"
---
# <a name="scwcmd-configure"></a>Scwcmd: Konfigurieren

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet eine Sicherheitsrichtlinie, die vom Sicherheitskonfigurations-Assistenten (SCW) generiert wurde, auf einen Computer an. Dieses Befehlszeilen Tool akzeptiert auch eine Liste von Computernamen als Eingabe.

## <a name="syntax"></a>Syntax

```
scwcmd configure [[[/m:<ComputerName> | /ou:<OuName>] /p:<Policy>] | /i:<ComputerList>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m\<ComputerName>|Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse des zu konfigurierenden Computers an. Wenn der **/m** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden.|
|/ou\<OuName>|Gibt den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) einer Organisationseinheit (OE) in Active Directory Domain Services an. Wenn der **/OU** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. Alle Computer in der Organisationseinheit werden gemäß der angegebenen Richtlinie analysiert.|
|/p\<Policy>|Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die zum Ausführen der Konfiguration verwendet werden soll.|
|/i\<ComputerList>|Gibt den Pfad und den Dateinamen einer XML-Datei an, die eine Liste von Computern sowie die erwarteten Richtlinien Dateien enthält. Alle Computer in der XML-Datei werden entsprechend den entsprechenden Richtlinien Dateien konfiguriert. Eine XML-Beispieldatei ist% windir% \security\SampleMachineList.xml.|
|/u\<UserName>|Gibt alternative Benutzer Anmelde Informationen an, die beim Konfigurieren eines Remote Computers verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer.|
|/PW\<Password>|Gibt alternative Benutzer Anmelde Informationen an, die beim Konfigurieren eines Remote Computers verwendet werden sollen. Der Standardwert ist das Kennwort des angemeldeten Benutzers.|
|/t:\<Threads>|Gibt die Anzahl von gleichzeitigen ausstehenden Konfigurations Vorgängen an, die während des Konfigurationsprozesses (DefaultValue = 40, MinValue = 1, MaxValue = 1000) beibehalten werden sollen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Scwcmd.exe ist nur auf Computern verfügbar, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei webpolicy.xml zu konfigurieren:
```
scwcmd configure /p:webpolicy.xml
```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für den Computer unter 172.16.0.0 für die Datei webpolicy.xml mithilfe der Anmelde Informationen für das webadmin-Konto zu konfigurieren:
```
scwcmd configure /m:172.16.0.0 /p:webpolicy.xml /u:webadmin
```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf allen Computern in der Liste campusmachines.xml mit maximal 100 Threads zu konfigurieren:
```
scwcmd configure /i:campusmachines.xml /t:100
```
Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf allen Computern in der Organisationseinheit Webservers mit den Datei webpolicy.xml zu konfigurieren, indem Sie die Anmelde Informationen des DomainAdmin-Kontos verwenden:
```
scwcmd configure /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)