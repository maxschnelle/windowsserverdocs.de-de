---
title: query user
description: Referenz Artikel für den Abfrage Benutzer-Befehl, der Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6929f7828f82c50723ae0a8c658ee2c79e1f1499
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956452"
---
# <a name="query-user"></a>query user

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server an. Mit diesem Befehl können Sie herausfinden, ob ein bestimmter Benutzer an einem bestimmten Remotedesktop-Sitzungshost Server angemeldet ist. Dieser Befehl gibt folgende Information zurück:

- Name des Benutzers

- Name der Sitzung auf dem Remotedesktop-Sitzungshost Server

- Sitzungs-ID

- Status der Sitzung (aktiv oder getrennt)

- Leerlaufzeit (die Anzahl der Minuten seit dem letzten Tastatur Strich oder der Mausbewegung bei der Sitzung)

- Datum und Uhrzeit der Anmeldung des Benutzers

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
query user [<username> | <sessionname> | <sessionID>] [/server:<servername>]
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

- Wenn der **Abfrage Benutzer** Informationen zurückgibt, `(>)` wird vor der aktuellen Sitzung ein größer-als-Symbol angezeigt.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen über alle Benutzer anzuzeigen, die auf dem System angemeldet sind:

```
query user
```

Geben Sie Folgendes ein, um Informationen zum Benutzer *User1* auf Server *Server1*anzuzeigen:

```
query user USER1 /server:Server1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Abfragebefehl](query.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
