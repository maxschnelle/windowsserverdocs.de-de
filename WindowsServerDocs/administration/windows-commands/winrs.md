---
title: winrs
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9c612a7c6f5d0935223b3c193c52fe970c970d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440053"
---
# <a name="winrs"></a>winrs

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Windows-Remoteverwaltung können Sie verwalten und Programme remote ausführen.   
## <a name="syntax"></a>Syntax  
```  
winrs [/<parameter>[:<value>]] <command>  
```  
### <a name="parameters"></a>Parameter  

|           Parameter            |                                                                                                                                                                                    Beschreibung                                                                                                                                                                                     |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      / remote:\<Endpunkt >       |                                                                                          Gibt an, der Zielendpunkt mit einem NetBIOS-Namen oder die standard-Verbindung:<br /><br />-   <url>: [\<Transport > ://]\<Ziel > [:\<Port >]<br /><br />Wenn nicht angegeben, **/r:localhost** verwendet wird.                                                                                          |
|          /unencrypted          | Gibt an, dass die Nachrichten an die Remoteshell werden nicht verschlüsselt. Dies ist nützlich für die Problembehandlung oder wenn der Netzwerkdatenverkehr mit bereits verschlüsselt ist **Ipsec**, oder wenn die physischer Sicherheit erzwungen wird.<br /><br />Standardmäßig werden die Nachrichten mit Kerberos oder NTLM-Schlüsseln verschlüsselt.<br /><br />Diese Befehlszeilenoption wird ignoriert, wenn HTTPS-Transport aktiviert ist. |
|     Section:\<Benutzername >      |                                                                                Gibt den Benutzernamen in Befehlszeile an.<br /><br />Wenn nicht angegeben, wird das Tool Negotiate-Authentifizierung oder die Eingabeaufforderung für den Namen verwenden.<br /><br />Wenn **Section** angegeben wird, **/Password** muss auch angegeben werden.                                                                                 |
|     /password:\<password>      |                                                                           Gibt das Kennwort auf der Befehlszeile an.<br /><br />Wenn **/Password** nicht angegeben ist, aber **Section** ist, wird das Tool für das Kennwort aufgefordert.<br /><br />Wenn **/Password** angegeben wird, **Section** muss auch angegeben werden.                                                                            |
|      /timeout:\<seconds>       |                                                                                                                                                                             Diese Option ist veraltet.                                                                                                                                                                             |
|       /directory:\<path>       |                                                                                            Gibt das Startverzeichnis für remote-Shell an.<br /><br />Wenn nicht angegeben wird, startet die Remoteshell im Basisverzeichnis von des Benutzers durch die Umgebungsvariable definiert **% USERPROFILE%** .                                                                                             |
| /environment:\<string>=<value> |                                                                          Gibt eine einzelne Umgebungsvariable festgelegt werden, wenn shell-Shell gestartet wird, die ermöglicht das Ändern der standardumgebung.<br /><br />Wenn mehrfaches Vorkommen der diese Option müssen verwendet werden, mehrere Umgebungsvariablen angeben.                                                                          |
|            /noecho             |                                                                                                    Gibt an, diese Echo deaktiviert werden soll. Dies ist möglicherweise erforderlich, um sicherzustellen, dass Antworten auf remote-eingabeaufforderungen des Benutzers lokal nicht angezeigt werden.<br /><br />Standardmäßig ist die Echo "on".                                                                                                    |
|           /noprofile           |                                              Gibt an, dass das Profil des Benutzers nicht geladen werden soll.<br /><br />Standardmäßig versucht der Server das Benutzerprofil laden.<br /><br />Wenn der Remotebenutzer kein lokaler Administrator auf dem Zielsystem, wird diese Option ist nicht erforderlich (die Standardeinstellung führt zu Fehler).                                               |
|         /allowdelegate         |                                                                                                                  Gibt an, dass die Anmeldeinformationen des Benutzers verwendet werden können auf einer Remotefreigabe befindet, z. B. auf einem anderen Computer als dem Zielendpunkt gefunden.                                                                                                                   |
|          /compression          |                                                                           Komprimierung aktivieren.  Ältere Installationen auf Remotecomputern können die Komprimierung nicht unterstützen, damit es standardmäßig deaktiviert ist.<br /><br />Standardeinstellung ist deaktiviert, da ältere Installationen auf Remotecomputern Komprimierung möglicherweise nicht unterstützt.                                                                           |
|            /UseSSL             |                                                                                                               Verwenden Sie eine SSL-Verbindung, wenn einen Remoteendpunkt zu verwenden.  Durch diese anstelle des Transports Angabe **Https:** verwenden die standardmäßige **WinRM** Standardport.                                                                                                                |
|               /?               |                                                                                                                                                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                        |

## <a name="remarks"></a>Hinweise  
-   Alle Befehlszeilenoptionen akzeptiert entweder Kurzform oder lange Form. Z. B. sowohl **/r** und **/remote** gültig sind.  
-   Beendet die **/remote** Befehl, der Benutzer eingeben kann **STRG + C** oder **STRG + UNTBR**, die an die Remoteshell gesendet werden. Die zweite **STRG + C** erzwingt eine Beendigung der **winrs.exe**.  
-   Um aktive Remoteshells oder Winrs-Konfiguration zu verwalten, verwenden Sie den WinRM-Tool.  Der URI ist der Alias zum Verwalten von active Shells **Shell/Cmd**.  Der URI für Winrs-Konfiguration ist ein alias ist **Winrm/Config/Winrs**.  

## <a name="BKMK_Examples"></a>Beispiele für  
```  
winrs /r:https://contoso.com command  
```  
```  
winrs /r:contoso.com /usessl command  
```  
```  
winrs /r:myserver command  
```  
```  
winrs /r:http://127.0.0.1 command  
```  
```  
winrs /r:http://169.51.2.101:80 /unencrypted command  
```  
```  
winrs /r:https://[::FFFF:129.144.52.38] command  
```  
```  
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command  
```  
```  
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig  
```  
```  
winrs /r:myserver /env:path=^%path^%;c:\tools /env:TEMP=d:\temp config.cmd  
```  
```  
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789  
```  
```  
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  

