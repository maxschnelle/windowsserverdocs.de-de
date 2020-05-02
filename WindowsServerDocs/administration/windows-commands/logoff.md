---
title: Abmelden
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86acf174bfdebdeab6db7476713dd2d91f21b1a0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724265"
---
# <a name="logoff"></a>Abmelden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Protokolliert einen Benutzer von einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host Server) und löscht die Sitzung vom Server.


> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                             BESCHREIBUNG                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <SessionName>     |                                                                  Gibt den Namen der Sitzung an.                                                                  |
|     <SessionID>      |                                                 Gibt die numerische ID an, die die Sitzung mit dem Server identifiziert.                                                 |
| /server:<ServerName> | Gibt den RD-Sitzungs Host Server an, der die Sitzung enthält, deren Benutzer Sie abmelden möchten. Wenn nicht angegeben, wird der Server verwendet, auf dem Sie zurzeit aktiv sind. |
|          /v          |                                                       Zeigt Informationen zu den Aktionen an, die ausgeführt werden.                                                        |
|          /?          |                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                 |

## <a name="remarks"></a>Bemerkungen
- Sie können sich jederzeit von der Sitzung abmelden, an der Sie gerade angemeldet sind. Sie müssen jedoch über die Berechtigung "Vollzugriff" verfügen, um Benutzer von anderen Sitzungen abzumelden.
- Wenn Sie einen Benutzer ohne Warnung aus einer Sitzung abmelden, kann dies zu Datenverlusten in der Sitzung des Benutzers führen. Sie sollten eine Nachricht an den Benutzer senden, indem Sie den Befehl " **msg** " verwenden, um den Benutzer vor der Durchführung dieser Aktion zu warnen.
- Wenn <*SessionID*> oder <*Sessionname*> nicht angegeben **ist, protokolliert** die Abmeldung den Benutzer aus der aktuellen Sitzung. Wenn Sie <*Sessionname*> angeben, muss es sich um einen aktiven Wert handeln.
- Wenn Sie einen Benutzer abmelden, werden alle Prozesse beendet, und die Sitzung wird vom Server gelöscht.
- Es ist nicht möglich, einen Benutzer von der Konsolen Sitzung aus abzumelden.
  ## <a name="examples"></a>Beispiele
- Wenn Sie einen Benutzer aus der aktuellen Sitzung abmelden möchten, geben Sie Folgendes ein:
  ```
  logoff
  ```
- Wenn Sie einen Benutzer mithilfe der Sitzungs-ID von einer Sitzung abmelden möchten, z. b. Sitzung 12, geben Sie Folgendes ein:
  ```
  logoff 12
  ```
- Wenn Sie einen Benutzer mithilfe des Namens der Sitzung und des Servers von einer Sitzung abmelden möchten, z. b. Session TERM04 on Server1, geben Sie Folgendes ein:
  ```
  logoff TERM04 /server:Server1
  ```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
