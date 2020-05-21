---
title: Abfrage Sitzung
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b0d122beac43abfd826cb406adac4aa277fc72e
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436275"
---
# <a name="query-session"></a>Abfrage Sitzung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) an.
Die Liste enthält nicht nur Informationen zu aktiven Sitzungen, sondern auch zu anderen Sitzungen, die vom Server ausgeführt werden.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query session [<SessionName> | <UserName> | <SessionID>] [/server:<ServerName>] [/mode] [/flow] [/connect] [/counter]
> ```
> ### <a name="parameters"></a>Parameter
>
> |      Parameter       |                                                      Beschreibung                                                      |
> |----------------------|-----------------------------------------------------------------------------------------------------------------------|
> |    <SessionName>     |                               Gibt den Namen der Sitzung an, die Sie Abfragen möchten.                               |
> |      <UserName>      |                           Gibt den Namen des Benutzers an, dessen Sitzungen Sie Abfragen möchten.                            |
> |     <SessionID>      |                                Gibt die ID der Sitzung an, die Sie Abfragen möchten.                                |
> | /server:<ServerName> |                  Identifiziert den Remote Desktop-Sitzungs Host Server für die Abfrage. Der Standardwert ist der aktuelle Server.                   |
> |        /Mode         |                                            Zeigt die aktuellen Zeilen Einstellungen an.                                            |
> |        /flow         |                                        Zeigt die aktuellen Einstellungen für die Fluss Steuerung an.                                        |
> |       /Connect       |                                          Zeigt die aktuellen Verbindungseinstellungen an.                                           |
> |       /Counter       | Zeigt aktuelle Zähler Informationen an, einschließlich der Gesamtzahl der erstellten, getrennten Sitzungen und der Wiederherstellung der Verbindung. |
> |          /?          |                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                          |
>
>#### <a name="remarks"></a>Hinweise
> - Ein Benutzer kann immer die Sitzung Abfragen, an der der Benutzer zurzeit angemeldet ist. Um andere Sitzungen abzufragen, muss der Benutzer über die Berechtigung "spezielle Zugriffsberechtigung für Abfrage Informationen" verfügen.
> - Wenn Sie keine Sitzung angeben, indem Sie <*Sessionname*>, <*username*> oder <*SessionID*> verwenden, werden in der **Abfrage Sitzung** Informationen zu allen aktiven Sitzungen im System angezeigt.
> - Wenn die **Abfrage Sitzung** Informationen zurückgibt, wird vor der aktuellen Sitzung ein größer-als-Symbol (>) angezeigt. Im folgenden finden Sie eine Beispielausgabe für die **Abfrage Sitzung**:
>   ```
>   C:\>query session
>    SESSIONNAME    USERNAME       ID STATE  TYPE   DEVICE
>   console        Administrator1  0 active wdcon
>    rdp-tcp#1      User1           1 active wdtshare
>    rdp-tcp                        2 listen wdtshare
>                                   4 idle
>                                   5 idle
>   ```
>   Das Symbol "größer als (>)" gibt die aktuelle Sitzung an. Sessionname gibt den Namen an, der der Sitzung zugewiesen ist. USERNAME gibt den Benutzernamen des Benutzers an, der mit der Sitzung verbunden ist. State enthält Informationen zum aktuellen Status der Sitzung. Typ gibt den Sitzungstyp an. Das Gerät, das für die-Konsole oder die mit dem Netzwerk verbundenen Sitzungen nicht vorhanden ist, ist der Gerätename, der der Sitzung zugewiesen ist. Der Kommentar nach den Sitzungsinformationen wird aus dem Sitzungs Profil entfernt. Alle Sitzungen, in denen der Anfangszustand als deaktiviert konfiguriert ist, werden erst dann in der Liste der **Abfrage** Sitzungen angezeigt, wenn Sie aktiviert sind.
>   ## <a name="examples"></a>Beispiele
> - Geben Sie Folgendes ein, um Informationen zu allen aktiven Sitzungen auf dem Server SERver2 anzuzeigen:
>   ```
>   query session /server:SERver2
>   ```
> - Geben Sie Folgendes ein, um Informationen zu aktiven Sitzungs-modeM02 anzuzeigen:
>   ```
>   query session modeM02
>   ```
>   ## <a name="additional-references"></a>Zusätzliche Referenzen
>   - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
>    [Abfrage](query.md) 
>    [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
