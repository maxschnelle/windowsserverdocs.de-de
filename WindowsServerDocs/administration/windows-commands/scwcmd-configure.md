---
title: scwcmd configure
description: Referenz Artikel für den Befehl scwcmd configure, bei dem eine Sicherheitsrichtlinie, die vom Sicherheitskonfigurations-Assistenten (SCW) generiert wurde, auf einen Computer angewendet wird.
ms.topic: reference
ms.assetid: 6528b9dc-3d82-4228-b734-ed717458d74c
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a57d2142f8fc7fd788a5669c5318ff6444c34734
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388587"
---
# <a name="scwcmd-configure"></a>scwcmd configure

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Wendet eine Sicherheitsrichtlinie, die vom Sicherheitskonfigurations-Assistenten (SCW) generiert wurde, auf einen Computer an. Dieses Befehlszeilen Tool akzeptiert auch eine Liste von Computernamen als Eingabe.

## <a name="syntax"></a>Syntax

```
scwcmd configure [[[/m:<computername> | /ou:<OuName>] /p:<policy>] | /i:<computerlist>] [/u:<username>] [/pw:<password>] [/t:<threads>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /m`<computername>` | Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse des zu konfigurierenden Computers an. Wenn der **/m** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. |
| /ou`<OuName>` | Gibt den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) einer Organisationseinheit (OE) in Active Directory Domain Services an. Wenn der **/OU** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. Alle Computer in der Organisationseinheit werden für die jeweilige Richtlinie konfiguriert. |
| /p`<policy>` | Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die zum Ausführen der Konfiguration verwendet werden soll. |
| /i`<computerlist>` | Gibt den Pfad und den Dateinamen einer XML-Datei an, die eine Liste von Computern sowie die erwarteten Richtlinien Dateien enthält. Alle Computer in der XML-Datei werden anhand ihrer entsprechenden Richtlinien Dateien analysiert. Eine XML-Beispieldatei ist `%windir%\security\SampleMachineList.xml` . |
| /u`<username>` | Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Konfiguration auf einem Remote Computer verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer. |
| /PW`<password>` | Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Konfiguration auf einem Remote Computer verwendet werden sollen. Der Standardwert ist das Kennwort des angemeldeten Benutzers. |
| /t:`<threads>` | Gibt die Anzahl von gleichzeitigen ausstehenden Konfigurations Vorgängen an, die während der Analyse gewartet werden sollen. Der Wertebereich ist 1-1000 und hat den Standardwert 40. |
| /l | Bewirkt, dass der Analyseprozess protokolliert wird. Für jeden Computer, der analysiert wird, wird eine Protokolldatei generiert. Die Protokolldateien werden im selben Verzeichnis wie die Ergebnisdateien gespeichert. Verwenden Sie die Option **/o** , um das Verzeichnis für die Ergebnisdateien anzugeben. |
| /e | Protokolliert ein Ereignis im Anwendungs Ereignisprotokoll, wenn keine Übereinstimmung gefunden wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei *webpolicy.xml*zu konfigurieren:

```
scwcmd configure /p:webpolicy.xml
```

Geben Sie Folgendes ein, um mithilfe der Anmelde Informationen des *webadmin* -Kontos eine Sicherheitsrichtlinie für den Computer unter *172.16.0.0* für die Datei *webpolicy.xml* zu konfigurieren:

```
scwcmd configure /m:172.16.0.0 /p:webpolicy.xml /u:webadmin
```

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf allen Computern in der Liste *campusmachines.xml* mit *maximal 100 Threads*zu konfigurieren:

```
scwcmd configure /i:campusmachines.xml /t:100
```

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die *Webservers* -Organisationseinheit mit *den Anmelde Informationen für die Datei* *webpolicy.xml* zu konfigurieren:

```
scwcmd configure /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Analyse Befehl](scwcmd-analyze.md)

- [scwcmd-register Befehl](scwcmd-register.md)

- [scwcmd-rollback-Befehl](scwcmd-rollback.md)

- [Befehl "Scwcmd Transform"](scwcmd-transform.md)

- [scwcmd-Ansichts Befehl](scwcmd-view.md)