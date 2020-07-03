---
title: qwinsta
description: Referenz Artikel für den qwinsta-Befehl, der Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a793212a-7ecd-44cb-a77b-c5c2edb34979
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9b79495d3fa142fd343b9c521563e093d20fc68
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931998"
---
# <a name="qwinsta"></a>qwinsta

Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Sitzungen auf einem Remotedesktop-Sitzungshost Server an. Die Liste enthält nicht nur Informationen zu aktiven Sitzungen, sondern auch zu anderen Sitzungen, die vom Server ausgeführt werden.

> [!NOTE]
> Dieser Befehl ist mit dem [Abfrage Sitzungs Befehl](query-session.md)identisch. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
qwinsta [<sessionname> | <username> | <sessionID>] [/server:<servername>] [/mode] [/flow] [/connect] [/counter]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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

#### <a name="remarks"></a>Hinweise

- Ein Benutzer kann immer die Sitzung Abfragen, an der der Benutzer zurzeit angemeldet ist. Um andere Sitzungen abzufragen, muss der Benutzer über eine spezielle Zugriffsberechtigung verfügen.

- Wenn Sie keine Sitzung mit den Parametern <*username*>, <*Sessionname*> oder *SessionID* angeben, werden in dieser Abfrage Informationen zu allen aktiven Sitzungen im System angezeigt.

- Wenn **qwinsta** Informationen zurückgibt, `(>)` wird vor der aktuellen Sitzung ein größer-als-Symbol angezeigt. Beispiel:

    ```
    C:\>qwinsta
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
  - Alle Sitzungen, in denen der anfängliche Zustand als deaktiviert konfiguriert ist, werden erst dann in der **qwinsta** -Liste angezeigt, wenn Sie aktiviert sind.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu allen aktiven Sitzungen auf dem Server *Server2*anzuzeigen:

```
qwinsta /server:Server2
```

Geben Sie Folgendes ein, um Informationen zu aktiven Sitzungs- *modeM02*anzuzeigen:

```
qwinsta modeM02
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Abfrage Sitzungs Befehl](query-session.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
