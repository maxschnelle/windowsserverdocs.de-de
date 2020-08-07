---
title: quser
description: Referenz Artikel für den Befehl quser, der Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server anzeigt.
ms.topic: article
ms.assetid: 8056204f-ed11-4c91-bb1d-c799283a48a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd56263e65ed9b6749f6d3d63c60bce32bb8ed53
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884384"
---
# <a name="quser"></a>quser

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server an. Mit diesem Befehl können Sie herausfinden, ob ein bestimmter Benutzer an einem bestimmten Remotedesktop-Sitzungshost Server angemeldet ist. Dieser Befehl gibt folgende Information zurück:

- Name des Benutzers

- Name der Sitzung auf dem Remotedesktop-Sitzungshost Server

- Sitzungs-ID

- Status der Sitzung (aktiv oder getrennt)

- Leerlaufzeit (die Anzahl der Minuten seit dem letzten Tastatur Strich oder der Mausbewegung bei der Sitzung)

- Datum und Uhrzeit der Anmeldung des Benutzers

> [!NOTE]
> Dieser Befehl ist mit dem Befehl für die [Abfrage Benutzer](query-user.md)identisch. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
quser [<username> | <sessionname> | <sessionID>] [/server:<servername>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<username>` | Gibt den Anmelde Namen des Benutzers an, den Sie Abfragen möchten. |
| `<sessionname>` | Gibt den Namen der Sitzung an, die Sie Abfragen möchten. |
| `<sessionID>` | Gibt die ID der Sitzung an, die Sie Abfragen möchten. |
| /server:`<servername>` | Gibt den Remotedesktop-Sitzungshost Server an, den Sie Abfragen möchten. Andernfalls wird der aktuelle Remotedesktop-Sitzungshost Server verwendet. Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl auf einem Remote Server verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Um diesen Befehl verwenden zu können, müssen Sie über die Berechtigung "Vollzugriff" oder eine spezielle Zugriffsberechtigung verfügen.

- Wenn Sie keinen Benutzer mit den Parametern <*username*>, <*Sessionname*> oder *SessionID* angeben, wird eine Liste aller Benutzer zurückgegeben, die beim Server angemeldet sind. Alternativ können Sie auch den Befehl **Abfrage Sitzung** verwenden, um eine Liste aller Sitzungen auf einem Server anzuzeigen.

- Wenn **quser** Informationen zurückgibt, `(>)` wird vor der aktuellen Sitzung ein größer-als-Symbol angezeigt.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen über alle Benutzer anzuzeigen, die auf dem System angemeldet sind:

```
quser
```

Geben Sie Folgendes ein, um Informationen zum Benutzer *User1* auf Server *Server1*anzuzeigen:

```
quser USER1 /server:Server1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Abfrage Benutzer"](query-user.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
