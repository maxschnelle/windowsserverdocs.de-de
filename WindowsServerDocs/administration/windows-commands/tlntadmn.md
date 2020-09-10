---
title: tlntadmn
description: Referenz Artikel zu tlntadmn, bei dem ein lokaler Computer oder ein Remote Computer verwaltet wird, auf dem der Telnet-Server Dienst ausgeführt wird.
ms.topic: reference
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d7cadac684b8cba2ea0120946f174d2cba0342f7
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640412"
---
# <a name="tlntadmn"></a>tlntadmn

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwaltet einen lokalen oder Remote Computer, auf dem der Telnet-Server Dienst ausgeführt wird.

## <a name="syntax"></a>Syntax
```
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]
```
#### <a name="parameters"></a>Parameter

|                   Parameter                    |                                                                                                                                                       BESCHREIBUNG                                                                                                                                                        |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                \<computerName>                 |                                                                                                                    Gibt den Namen des Servers an, mit dem eine Verbindung hergestellt werden soll. Die Standardeinstellung ist der lokale Computer.                                                                                                                    |
|         -u \<UserName> -p \<Password>          |                                                Gibt administrative Anmelde Informationen für einen Remote Server an, den Sie verwalten möchten. Dieser Parameter ist erforderlich, wenn Sie einen Remote Server verwalten möchten, für den Sie nicht mit administrativen Anmelde Informationen angemeldet sind.                                                |
|                     start                      |                                                                                                                                            startet den Telnet-Server Dienst.                                                                                                                                             |
|                      stop                      |                                                                                                                                             Beendet den Telnet-Server Dienst.                                                                                                                                              |
|                     pause                      |                                                                                                                          hält den Telnet-Server Dienst an. Es werden keine neuen Verbindungen akzeptiert.                                                                                                                          |
|                    continue                    |                                                                                                                                            Setzt den Telnet-Server Dienst fort.                                                                                                                                            |
|          -s { \<SessionID> &#124; alle}          |                                                                                                                                             Zeigt aktive Telnet-Sitzungen an.                                                                                                                                             |
|          -k { \<SessionID> &#124; alle}          |                                                                                                        Beendet Telnet-Sitzungen. Geben Sie die Sitzungs-ID ein, um eine bestimmte Sitzung zu beenden, oder geben Sie alle ein, um alle Sitzungen zu beenden.                                                                                                         |
|    -m { \<SessionID> &#124; alle}  <Message>     |                                                   Sendet eine Nachricht an eine oder mehrere Sitzungen. Geben Sie die Sitzungs-ID ein, um eine Nachricht an eine bestimmte Sitzung zu senden, oder geben Sie all ein, um eine Nachricht an alle Sitzungen zu senden. Geben Sie die Nachricht ein, die Sie zwischen Anführungszeichen senden möchten.                                                   |
|             config-Dom = \<Domain>             |                                                                                                                                      Konfiguriert die Standard Domäne für den Server.                                                                                                                                       |
|      config CtrlAKeyMap = {yes &#124; No}      |                                                                                     Gibt an, ob der Telnet-Server STRG + A als alt interpretieren soll. Geben Sie **Yes** ein, um die Tastenkombination zuzuordnen, oder geben Sie **Nein** ein, um die Zuordnung zu verhindern.                                                                                     |
|       config Timeout = \<hh> : \<mm> :\<ss>       |                                                                                                                                 Legt den Timeout Zeitraum in Stunden, Minuten und Sekunden fest.                                                                                                                                 |
|     config TimeOutActive = {yes &#124; No      |                                                                                                                                            Aktiviert das Timeout für Leerlauf Sitzungen.                                                                                                                                             |
|          config MaxFail = \<attempts>          |                                                                                                                          Legt die maximale Anzahl von fehlgeschlagenen Anmelde versuchen fest, bevor die Verbindung getrennt wird.                                                                                                                          |
|        config maxconn = \<Connections>         |                                                                                                                                         Legt die maximale Anzahl von Verbindungen fest.                                                                                                                                          |
|            config Port = < \number>             |                                                                                                                    Legt den Telnet-Port fest. Sie müssen den Port mit einer ganzen Zahl angeben, die kleiner als 1024 ist.                                                                                                                    |
| config Sek. {+ &#124;-} NTLM {+ &#124;-} passwd | Gibt an, ob Sie zum Authentifizieren von Anmelde versuchen NTLM, ein Kennwort oder beides verwenden möchten. Wenn Sie einen bestimmten Authentifizierungstyp verwenden möchten, geben Sie **+** vor diesem Authentifizierungstyp ein Pluszeichen () ein. Um einen bestimmten Authentifizierungstyp zu vermeiden, geben Sie **-** vor diesem Authentifizierungstyp ein Minuszeichen () ein. |
|     config Mode = {Console &#124; Stream}      |                                                                                                                                             Gibt den Modus des Vorgangs an.                                                                                                                                             |
|                       -?                       |                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                           |

## <a name="remarks"></a>Hinweise
-   Zum Anzeigen der Servereinstellungen geben Sie **tlntadmn** ohne Parameter ein.
-   Wenn Sie den Befehl " **tlntadmn** " verwenden möchten, müssen Sie sich mit Administrator Anmelde Informationen am lokalen Computer anmelden. Um einen Remote Computer zu verwalten, müssen Sie auch administrative Anmelde Informationen für den Remote Computer angeben. Melden Sie sich auf dem lokalen Computer mit einem Konto an, das über Administrator Anmelde Informationen für den lokalen Computer und den Remote Computer verfügt. Wenn Sie diese Methode nicht verwenden können, können Sie die Parameter **-u** und **-p** verwenden, um administrative Anmelde Informationen für den Remote Computer bereitzustellen.

## <a name="examples"></a>Beispiele
Konfigurieren Sie das Timeout für Leerlauf Sitzungen auf 30 Minuten.
```
tlntadmn config timeout=0:30:0
```
Aktive Telnet-Sitzungen anzeigen.
```
tlntadmn -s
```

## <a name="additional-references"></a>Weitere Verweise
-   [Telnet-Betriebshandbuch](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753164(v=ws.10))
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
