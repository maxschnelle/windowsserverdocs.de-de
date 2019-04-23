---
title: Scwcmd konfigurieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6528b9dc-3d82-4228-b734-ed717458d74c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 31838ac7299cc30a7b7dde3beb47669df772487c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857501"
---
# <a name="scwcmd-configure"></a>scwcmd: configure

> Gilt für: Windows Server 2012 R2, Windows Server 2012

Wendet eine Sicherheitskonfigurations-Assistenten generierte Sicherheitsrichtlinie auf einem Computer an. Dieses Befehlszeilentool werden auch eine Liste mit Computernamen als Eingabe akzeptiert.

## <a name="syntax"></a>Syntax

```
scwcmd configure [[[/m:<ComputerName> | /ou:<OuName>] /p:<Policy>] | /i:<ComputerList>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/m:\<ComputerName>|Gibt an, den NetBIOS-Namen, DNS-Name oder IP-Adresse des Computers zu konfigurieren. Wenn die **/m** Parameter angegeben wird, und klicken Sie dann die **/p** Parameter muss auch angegeben werden.|
|/ou:\<OuName>|Gibt den vollqualifizierten Domänennamen (FQDN) von einer Organisationseinheit (OU) in Active Directory Domain Services an. Wenn die **OU** Parameter angegeben wird, und klicken Sie dann die **/p** Parameter muss auch angegeben werden. Alle Computer in der Organisationseinheit werden entsprechend der angegebenen Richtlinie analysiert werden.|
|/ p:\<Richtlinie >|Gibt den Pfad und Dateinamen Namen von der XML-Richtliniendatei, die verwendet werden, um die Konfiguration durchzuführen.|
|/i:\<ComputerList>|Gibt an, der Pfad und Dateiname einer XML-Datei, die eine Liste von Computern sowie deren erwartete Richtliniendateien enthält. Alle Computer in der XML-Datei werden entsprechend ihren entsprechenden Dateien für Gruppenrichtlinien konfiguriert werden. Eine Beispiel-XML-Datei ist % windir%\security\SampleMachineList.xml.|
|/ u:\<Benutzername >|Gibt eine alternative Anmeldeinformationen verwenden, wenn Sie einen Remotecomputer konfigurieren. Der Standardwert ist der angemeldete Benutzer.|
|PW:\<Kennwort >|Gibt eine alternative Anmeldeinformationen verwenden, wenn Sie einen Remotecomputer konfigurieren. Der Standardwert ist das Kennwort des angemeldeten Benutzers.|
|/t:\<Threads>|Gibt die Anzahl der gleichzeitigen ausstehende Konfigurationsvorgänge, die bei der Konfiguration beibehalten werden soll (Standardwert = 40 "," MinValue = 1, MaxValue = 1000).|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Scwcmd.exe ist nur auf Computern unter Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 verfügbar.

## <a name="BKMK_Examples"></a>Beispiele für

Um eine Sicherheitsrichtlinie für die Datei webpolicy.xml zu konfigurieren, geben Sie Folgendes ein:
```
scwcmd configure /p:webpolicy.xml
```
Um eine Sicherheitsrichtlinie für den Computer mithilfe von Anmeldeinformationen für das Webadmin am 172.16.0.0 für die Datei webpolicy.xml zu konfigurieren, geben Sie Folgendes ein:
```
scwcmd configure /m:172.16.0.0 /p:webpolicy.xml /u:webadmin
```
Um eine Sicherheitsrichtlinie auf allen Computern in der Liste campusmachines.xml mit maximal 100 Threads zu konfigurieren, geben Sie Folgendes ein:
```
scwcmd configure /i:campusmachines.xml /t:100
```
Um eine Sicherheitsrichtlinie auf allen Computern in der WebServers OU für die Datei webpolicy.xml mithilfe der Anmeldeinformationen des Kontos DomainAdmin konfigurieren möchten, geben Sie Folgendes ein:
```
scwcmd configure /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)