---
title: tlntadmn
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b4423e35d0c26819188001dea8d3d8497add7f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440956"
---
# <a name="tlntadmn"></a>tlntadmn

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verwaltet einen lokalen oder remote-Computer, auf dem der Telnet-Server-Dienst ausgeführt wird.   
## <a name="syntax"></a>Syntax  
```  
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]  
```  
### <a name="parameters"></a>Parameter  

|                   Parameter                    |                                                                                                                                                       Beschreibung                                                                                                                                                        |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                \<computerName>                 |                                                                                                                    Gibt den Namen des Servers für die Verbindung. Der Standardwert ist der lokale Computer.                                                                                                                    |
|         -u \<Benutzername >-p \<Kennwort >          |                                                Gibt die administrativen Anmeldeinformationen für einen Remoteserver, den Sie verwalten möchten. Dieser Parameter ist erforderlich, sollten Sie einen Remoteserver zu verwalten, zu dem Sie nicht mit Administratorrechten angemeldet sind.                                                |
|                     start                      |                                                                                                                                            Startet die Telnet-Server-Dienst.                                                                                                                                             |
|                      stop                      |                                                                                                                                             Beendet die Telnet-Server-Dienst                                                                                                                                              |
|                     pause                      |                                                                                                                          Hält den Telnet-Server-Dienst. Es werden keine neuen Verbindungen akzeptiert werden.                                                                                                                          |
|                    Fortsetzen                    |                                                                                                                                            Der Telnet-Server-Dienst wird fortgesetzt.                                                                                                                                            |
|          -s {\<SessionID > &#124; alle}          |                                                                                                                                             Zeigt aktive Telnetsitzungen.                                                                                                                                             |
|          -k {\<SessionID > &#124; alle}          |                                                                                                        Telnet-Sitzung wird beendet. Geben Sie die Sitzungs-ID, um eine bestimmte Sitzung zu beenden, oder geben Sie alle auf alle Sitzungen zu beenden.                                                                                                         |
|    -m {\<SessionID > &#124; alle}  <Message>     |                                                   Sendet eine Nachricht an eine oder mehrere Sitzungen. Geben Sie die Sitzungs-ID zum Senden einer Nachricht an eine bestimmte Sitzung aus, oder geben Sie alle zum Senden einer Nachricht zu allen Sitzungen. Geben Sie die Meldung, die Sie zwischen Anführungszeichen senden möchten.                                                   |
|             config dom = \<Domain>             |                                                                                                                                      Konfiguriert die Standarddomäne für den Server an.                                                                                                                                       |
|      config ctrlakeymap = {yes &#124; no}      |                                                                                     Gibt an, ob es sich bei den Telnet-Server, STRG + A, wie ALT interpretiert werden sollen. Typ **Ja** Zuordnung die Tastenkombination oder Typ **keine** um die Zuordnung zu verhindern.                                                                                     |
|       config timeout = \<hh>:\<mm>:\<ss>       |                                                                                                                                 Legt den Timeout-Zeitraum in Stunden, Minuten und Sekunden fest.                                                                                                                                 |
|     config timeoutactive = {yes &#124; no      |                                                                                                                                            Ermöglicht das Timeout für leerlaufsitzungen.                                                                                                                                             |
|          config maxfail = \<attempts>          |                                                                                                                          Legt die maximale Anzahl fehlgeschlagener Anmeldeversuche vor dem Trennen der Verbindung fest.                                                                                                                          |
|        config maxconn = \<Connections>         |                                                                                                                                         Legt die maximale Anzahl von Verbindungen.                                                                                                                                          |
|            Config Port = < \Number >             |                                                                                                                    Legt den Telnet-Port fest. Sie müssen den Port angeben, durch eine ganze Zahl kleiner als 1024.                                                                                                                    |
| Config s {+ &#124; -} NTLM {+ &#124; -} Passwd | Gibt an, ob NTLM und/oder ein Kennwort zu verwenden, um die Anmeldeversuche authentifiziert werden sollen. Um einen bestimmten Typ von Authentifizierung zu verwenden, geben Sie ein Pluszeichen ( **+** ) bevor Sie diesen Typ der Authentifizierung. Um zu verhindern, verwenden einen bestimmten Typ von Authentifizierung, geben Sie ein Minuszeichen ( **-** ) bevor Sie diesen Typ der Authentifizierung. |
|     config mode = {console &#124; stream}      |                                                                                                                                             Gibt den Modus des Vorgangs.                                                                                                                                             |
|                       -?                       |                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                           |

## <a name="remarks"></a>Hinweise  
-   Geben Sie zum Anzeigen der servereinstellungen **Tlntadmn** ohne Parameter.  
-   Verwenden der **Tlntadmn** können Sie auf dem lokalen Computer mit administrativen Anmeldeinformationen anmelden müssen. Um zu einen Remotecomputer zu verwalten, müssen Sie auch die Administratoranmeldeinformationen für den Remotecomputer bereitstellen. Sie können durch Anmelden bei dem lokalen Computer mit einem Konto dafür die Administratoranmeldeinformationen für den lokalen Computer und dem Remotecomputer verfügt. Wenn Sie diese Methode verwenden können, können Sie mithilfe der **-u** und **-p** Parameter für die administrative Anmeldeinformationen für den Remotecomputer.  

## <a name="BKMK_Examples"></a>Beispiele für  
Konfigurieren Sie das Timeout für leerlaufsitzungen auf 30 Minuten.  
```  
tlntadmn config timeout=0:30:0  
```  
Zeigen Sie aktive Telnetsitzungen.  
```  
tlntadmn -s  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   [Telnet-Betriebshandbuch](https://technet.microsoft.com/library/cc753164(v=ws.10).aspx)  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
