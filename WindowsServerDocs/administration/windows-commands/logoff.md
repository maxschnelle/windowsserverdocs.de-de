---
title: Abmelden
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1661a9dd6cc89ea05980fd9085aa8fa67b8fe2c0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840413"
---
# <a name="logoff"></a>Abmelden

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Protokolliert einen Benutzer von einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host Server) und löscht die Sitzung vom Server.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
### <a name="parameters"></a>Parameter

|      Parameter       |                                                                             Beschreibung                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <SessionName>     |                                                                  Gibt den Namen der Sitzung an.                                                                  |
|     <SessionID>      |                                                 Gibt die numerische ID an, die die Sitzung mit dem Server identifiziert.                                                 |
| /server:<ServerName> | Gibt den RD-Sitzungs Host Server an, der die Sitzung enthält, deren Benutzer Sie abmelden möchten. Wenn nicht angegeben, wird der Server verwendet, auf dem Sie zurzeit aktiv sind. |
|          /v          |                                                       Zeigt Informationen zu den Aktionen an, die ausgeführt werden.                                                        |
|          /?          |                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                 |

## <a name="remarks"></a>Hinweise
- Sie können sich jederzeit von der Sitzung abmelden, an der Sie gerade angemeldet sind. Sie müssen jedoch über die Berechtigung "Vollzugriff" verfügen, um Benutzer von anderen Sitzungen abzumelden.
- Wenn Sie einen Benutzer ohne Warnung aus einer Sitzung abmelden, kann dies zu Datenverlusten in der Sitzung des Benutzers führen. Sie sollten eine Nachricht an den Benutzer senden, indem Sie den Befehl " **msg** " verwenden, um den Benutzer vor der Durchführung dieser Aktion zu warnen.
- Wenn <*SessionID*> oder <*Sessionname*> nicht angegeben **ist, protokolliert** die Abmeldung den Benutzer aus der aktuellen Sitzung. Wenn Sie <*Sessionname*> angeben, muss es sich um einen aktiven Wert handeln.
- Wenn Sie einen Benutzer abmelden, werden alle Prozesse beendet, und die Sitzung wird vom Server gelöscht.
- Es ist nicht möglich, einen Benutzer von der Konsolen Sitzung aus abzumelden.
  ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
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

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
