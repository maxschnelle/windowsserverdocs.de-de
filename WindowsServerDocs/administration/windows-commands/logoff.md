---
title: Abmelden
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88b3cbbbd52a965fd0a0de3c164e8dbc1f90d053
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437527"
---
# <a name="logoff"></a>Abmelden

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Meldet einen Benutzer aus einer Sitzung auf einem Server Remote Desktop Session Host (rd Session Host), und löscht die Sitzung auf dem Server.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
## <a name="parameters"></a>Parameter

|      Parameter       |                                                                             Beschreibung                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <SessionName>     |                                                                  Gibt den Namen der Sitzung.                                                                  |
|     <SessionID>      |                                                 Gibt an, die numerische ID, die die Sitzung mit dem Server identifiziert.                                                 |
| /server:<ServerName> | Gibt an, den rd-Sitzungshostserver, der die Sitzung enthält, deren Benutzer Sie abmelden möchten. Falls nicht angegeben, wird der Server, auf dem Sie zurzeit aktiv sind, verwendet. |
|          /v          |                                                       Zeigt Informationen zu den Aktionen, die ausgeführt wird.                                                        |
|          /?          |                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                 |

## <a name="remarks"></a>Hinweise
- Sie können immer aus der Sitzung abmelden zu denen Sie derzeit angemeldet sind. Sie müssen jedoch Vollzugriff zum Abmelden von Benutzern aus anderen Sitzungen berechtigt.
- Abmelden eines Benutzers aus einer Sitzung ohne Warnung kann zum Verlust von Daten an die Sitzung des Benutzers führen. Sie sollten eine Nachricht an den Benutzer senden, indem Sie mit der **msg** Befehl aus, um den Benutzer zu warnen, vor dem Ausführen dieser Aktion annehmen.
- Wenn <*SessionID*> oder <*Sitzungsname*> nicht angegeben ist, **Abmeldung** meldet den Benutzer aus der aktuellen Sitzung. Bei Angabe von <*Sitzungsname*>, es muss eine aktiv sein.
- Wenn Sie sich ein Benutzer abmelden, werden alle Prozesse beendet und die Sitzung vom Server gelöscht.
- Sie können keinen Benutzer aus der Konsole-Sitzung abmelden.
  ## <a name="BKMK_examples"></a>Beispiele für
- Um einen Benutzer aus der aktuellen Sitzung abmelden möchten, geben Sie Folgendes ein:
  ```
  logoff
  ```
- Geben Sie zum Abmelden eines Benutzers aus einer Sitzung mit der Sitzung-ID, z. B. 12-Sitzung Folgendes ein:
  ```
  logoff 12
  ```
- Zum Abmelden eines Benutzers aus einer Sitzung mit dem Namen der Sitzung und des Servers, z. B. TERM04 auf Server1 geben:
  ```
  logoff TERM04 /server:Server1
  ```

#### <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
