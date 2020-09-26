---
title: scwcmd analyze
description: Referenz Artikel für den scwcmd-Befehl "analysieren", der bestimmt, ob ein Computer mit einer Richtlinie konform ist.
ms.topic: reference
ms.assetid: 0259271b-be5b-48d7-a51d-8b9b6786efb4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0d891262ebf04b1b8e604bc4756a3ca05888f8fa
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388606"
---
# <a name="scwcmd-analyze"></a>scwcmd analyze

> Gilt für: Windows Server 2012 R2 und Windows Server 2012

Bestimmt, ob ein Computer mit einer Richtlinie konform ist. Die Ergebnisse werden in einer XML-Datei zurückgegeben.

Mit diesem Befehl wird auch eine Liste von Computernamen als Eingabe akzeptiert. Um die Ergebnisse in Ihrem Browser anzuzeigen, verwenden Sie die **scwcmd-Ansicht** , und geben Sie `%windir%\security\msscw\TransformFiles\scwanalysis.xsl` als XSL-Transformation an.

## <a name="syntax"></a>Syntax

```
scwcmd analyze [[[/m:<computername> | /ou:<OuName>] /p:<policy>] | /i:<computerlist>] [/o:<resultdir>] [/u:<username>] [/pw:<password>] [/t:<threads>] [/l] [/e]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /m`<computername>` | Gibt den NetBIOS-Namen, den DNS-Namen oder die IP-Adresse des zu analysierenden Computers an. Wenn der **/m** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. |
| /ou`<OuName>` | Gibt den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) einer Organisationseinheit (OE) in Active Directory Domain Services an. Wenn der **/OU** -Parameter angegeben wird, muss auch der **/p** -Parameter angegeben werden. Alle Computer in der Organisationseinheit werden anhand der angegebenen Richtlinie analysiert. |
| /p`<policy>` | Gibt den Pfad und den Dateinamen der XML-Richtlinien Datei an, die zum Durchführen der Analyse verwendet werden soll. |
| /i`<computerlist>` | Gibt den Pfad und den Dateinamen einer XML-Datei an, die eine Liste von Computern sowie die erwarteten Richtlinien Dateien enthält. Alle Computer in der XML-Datei werden anhand ihrer entsprechenden Richtlinien Dateien analysiert. Eine XML-Beispieldatei ist `%windir%\security\SampleMachineList.xml` . |
| /o`<resultdir>` | Gibt den Pfad und das Verzeichnis an, in dem die Analyseergebnis Dateien gespeichert werden sollen. Der Standardwert ist das aktuelle Verzeichnis. |
| /u`<username>` | Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Analyse auf einem Remote Computer verwendet werden sollen. Der Standardwert ist der angemeldete Benutzer. |
| /PW`<password>` | Gibt alternative Benutzer Anmelde Informationen an, die beim Ausführen der Analyse auf einem Remote Computer verwendet werden sollen. Der Standardwert ist das Kennwort des angemeldeten Benutzers. |
| /t:`<threads>` | Gibt die Anzahl von gleichzeitigen ausstehenden Analyse Vorgängen an, die während der Analyse gewartet werden sollen. Der Wertebereich ist 1-1000 und hat den Standardwert 40. |
| /l | Bewirkt, dass der Analyseprozess protokolliert wird. Für jeden Computer, der analysiert wird, wird eine Protokolldatei generiert. Die Protokolldateien werden im selben Verzeichnis wie die Ergebnisdateien gespeichert. Verwenden Sie die Option **/o** , um das Verzeichnis für die Ergebnisdateien anzugeben. |
| /e | Protokolliert ein Ereignis im Anwendungs Ereignisprotokoll, wenn keine Übereinstimmung gefunden wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei *webpolicy.xml*zu analysieren:

```
scwcmd analyze /p:webpolicy.xml
```

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie auf dem Computer mit dem Namen *Webserver* für die Datei *webpolicy.xml* mithilfe der Anmelde Informationen des *webadmin* -Kontos zu analysieren:

```
scwcmd analyze /m:webserver /p:webpolicy.xml /u:webadmin
```

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die Datei *webpolicy.xml*mit *maximal 100 Threads*zu analysieren und die Ergebnisse in eine Datei mit dem Namen results in der *resultserver* -Freigabe auszugeben. Geben Sie Folgendes ein:

```
scwcmd analyze /i:webpolicy.xml /t:100 /o:\\resultserver\results
```

Geben Sie Folgendes ein, um eine Sicherheitsrichtlinie für die *Webservers* -Organisationseinheit mit der Datei *webpolicy.xml* mithilfe der *Domänen Administrator* -Anmelde Informationen zu analysieren:

```
scwcmd analyze /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [scwcmd-Befehl "configure"](scwcmd-configure.md)

- [scwcmd-register Befehl](scwcmd-register.md)

- [scwcmd-rollback-Befehl](scwcmd-rollback.md)

- [Befehl "Scwcmd Transform"](scwcmd-transform.md)

- [scwcmd-Ansichts Befehl](scwcmd-view.md)