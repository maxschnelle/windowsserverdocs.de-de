---
title: tlntadmn
description: Referenz Artikel für den tlntadmn-Befehl, der einen lokalen oder Remote Computer verwaltet, der den Telnet-Server Dienst ausgeführt wird.
ms.topic: reference
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a4de6903d5a9979f45677176d023c694e20cdfd
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156448"
---
# <a name="tlntadmn"></a>tlntadmn

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwaltet einen lokalen oder Remote Computer, auf dem der Telnet-Server Dienst ausgeführt wird. Bei Verwendung ohne Parameter zeigt **tlntadmn** die aktuellen Servereinstellungen an.

Dieser Befehl erfordert, dass Sie sich auf dem lokalen Computer mit Administrator Anmelde Informationen anmelden. Um einen Remote Computer zu verwalten, müssen Sie auch administrative Anmelde Informationen für den Remote Computer angeben. Melden Sie sich auf dem lokalen Computer mit einem Konto an, das über Administrator Anmelde Informationen für den lokalen Computer und den Remote Computer verfügt. Wenn Sie diese Methode nicht verwenden können, können Sie die Parameter **-u** und **-p** verwenden, um administrative Anmelde Informationen für den Remote Computer bereitzustellen.

## <a name="syntax"></a>Syntax

```
tlntadmn [<computername>] [-u <username>] [-p <password>] [{start | stop | pause | continue}] [-s {<sessionID> | all}] [-k {<sessionID> | all}] [-m {<sessionID> | all}  <message>] [config [dom = <domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <connections>] [port = <number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<computername>` | Gibt den Namen des Servers an, mit dem eine Verbindung hergestellt werden soll. Die Standardeinstellung ist der lokale Computer. |
| -u `<username> -p <password>` | Gibt administrative Anmelde Informationen für einen Remote Server an, den Sie verwalten möchten. Dieser Parameter ist erforderlich, wenn Sie einen Remote Server verwalten möchten, für den Sie nicht mit administrativen Anmelde Informationen angemeldet sind. |
| start | startet den Telnet-Server Dienst. |
| stop | Beendet den Telnet-Server Dienst. |
| pause | Hält den Telnet-Server Dienst an. Es werden keine neuen Verbindungen akzeptiert. |
| continue | Setzt den Telnet-Server Dienst fort. |
| -s `{<sessionID> | all}` | Zeigt aktive Telnet-Sitzungen an. |
| -k `{<sessionID> | all}` | Beendet Telnet-Sitzungen. Geben Sie die Sitzungs-ID ein, um eine bestimmte Sitzung zu beenden, oder geben Sie alle ein, um alle Sitzungen zu beenden. |
| -m `{<sessionID> | all}  <message>` | Sendet eine Nachricht an eine oder mehrere Sitzungen. Geben Sie die Sitzungs-ID ein, um eine Nachricht an eine bestimmte Sitzung zu senden, oder geben Sie all ein, um eine Nachricht an alle Sitzungen zu senden. Geben Sie die Nachricht ein, die Sie zwischen Anführungszeichen senden möchten. |
| config-Dom = `<domain>` | Konfiguriert die Standard Domäne für den Server. |
| config CtrlAKeyMap = `{yes | no}` | Gibt an, ob der Telnet-Server STRG + A als alt interpretieren soll. Geben Sie **Yes** ein, um die Tastenkombination zuzuordnen, oder geben Sie **Nein** ein, um die Zuordnung zu verhindern. |
| config-Timeout = `<hh>:<mm>:<ss>` | Legt den Timeout Zeitraum in Stunden, Minuten und Sekunden fest. |
| config TimeOutActive = `{yes | no}` | Aktiviert das Timeout für Leerlauf Sitzungen. |
| config MaxFail = `<attempts>` | Legt die maximale Anzahl von fehlgeschlagenen Anmelde versuchen fest, bevor die Verbindung getrennt wird. |
| config maxconn = `<connections>` | Legt die maximale Anzahl von Verbindungen fest. |
| config-Port = `<number>` | Legt den Telnet-Port fest. Sie müssen den Port mit einer ganzen Zahl angeben, die kleiner als 1024 ist. |
| config-Sek. `{+ | -}NTLM {+ | -}passwd` | Gibt an, ob Sie zum Authentifizieren von Anmelde versuchen NTLM, ein Kennwort oder beides verwenden möchten. Wenn Sie einen bestimmten Authentifizierungstyp verwenden möchten, geben Sie **+** vor diesem Authentifizierungstyp ein Pluszeichen () ein. Um einen bestimmten Authentifizierungstyp zu vermeiden, geben Sie **-** vor diesem Authentifizierungstyp ein Minuszeichen () ein. |
| config-Modus = `{console | stream}` | Gibt den Modus des Vorgangs an. |
| -? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Zum Konfigurieren des Timeouts für Leerlauf Sitzungen auf 30 Minuten geben Sie Folgendes ein:

```
tlntadmn config timeout=0:30:0
```

Geben Sie Folgendes ein, um aktive Telnet-Sitzungen anzuzeigen:

```
tlntadmn -s
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Telnet-Betriebshandbuch](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753164(v=ws.10))
