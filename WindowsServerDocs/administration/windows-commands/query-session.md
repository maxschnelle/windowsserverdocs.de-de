---
title: query session
description: Referenz Artikel für den Abfrage Sitzungs Befehl, der Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 75cb8deb61ebfe3a4b0db665da4353339ee8d314
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956502"
---
# <a name="query-session"></a>query session

Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server an. Die Liste enthält nicht nur Informationen zu aktiven Sitzungen, sondern auch zu anderen Sitzungen, die vom Server ausgeführt werden.

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
query session [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<sessionname>` | Gibt den Namen der Sitzung an, die Sie Abfragen möchten. |
| `<username>` | Gibt den Namen des Benutzers an, dessen Sitzungen Sie Abfragen möchten. |
| `<sessionID>` | Gibt die ID der Sitzung an, die Sie Abfragen möchten. |
| /server:`<servername>` | Identifiziert den Remote Desktop-Sitzungs Host Server für die Abfrage. Der Standardwert ist der aktuelle Server. |
| /Mode | Zeigt die aktuellen Zeilen Einstellungen an. |
| /flow | Zeigt die aktuellen Einstellungen für die Fluss Steuerung an. |
| /Connect | Zeigt die aktuellen Verbindungseinstellungen an. |
| /Counter | Zeigt aktuelle Zähler Informationen an, einschließlich der Gesamtzahl der erstellten, getrennten Sitzungen und der Wiederherstellung der Verbindung. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Ein Benutzer kann immer die Sitzung Abfragen, an der der Benutzer zurzeit angemeldet ist. Um andere Sitzungen abzufragen, muss der Benutzer über eine spezielle Zugriffsberechtigung verfügen.

- Wenn Sie keine Sitzung mit den Parametern <*username*>, <*Sessionname*> oder *SessionID* angeben, werden in dieser Abfrage Informationen zu allen aktiven Sitzungen im System angezeigt.

- Wenn die **Abfrage Sitzung** Informationen zurückgibt, `(>)` wird vor der aktuellen Sitzung ein größer-als-Symbol angezeigt. Beispiel:

    ```
    C:\>query session
        SESSIONNAME     USERNAME        ID STATE    TYPE    DEVICE
        console         Administrator1  0 active    wdcon
        >rdp-tcp#1      User1           1 active    wdtshare
        rdp-tcp                         2 listen    wdtshare
                                        4 idle
                                        5 idle
    ```

    Hierbei gilt:
  - **Sessionname** gibt den Namen an, der der Sitzung zugewiesen ist.
  - **Username** gibt den Benutzernamen des Benutzers an, der mit der Sitzung verbunden ist.
  - **State** enthält Informationen zum aktuellen Status der Sitzung.
  - **Typ** gibt den Sitzungstyp an.
  - Das **Gerät**, das für die Konsolen-oder Netzwerkverbindung nicht vorhanden ist, ist der Gerätename, der der Sitzung zugewiesen ist.
  - Alle Sitzungen, in denen der anfängliche Zustand als deaktiviert konfiguriert ist, werden erst dann in der Liste der **Abfrage** Sitzungen angezeigt, wenn Sie aktiviert sind.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu allen aktiven Sitzungen auf dem Server *Server2*anzuzeigen:

```
query session /server:Server2
```

Geben Sie Folgendes ein, um Informationen zu aktiven Sitzungs- *modeM02*anzuzeigen:

```
query session modeM02
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Abfragebefehl](query.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
