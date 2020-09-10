---
title: tsdiscon
description: Referenz Artikel zu "zdiscon", der eine Sitzung von einem Remote Desktop-Sitzungs Host Server trennt.
ms.topic: reference
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b116dfe8dc5ac3a689cae23ebba17b202b509897
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628558"
---
# <a name="tsdiscon"></a>tsdiscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Trennt eine Sitzung von einem Remotedesktop-Sitzungshost Server.



> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11)) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|\<SessionId>|Gibt die ID der Sitzung an, die getrennt werden soll.|
|\<SessionName>|Gibt den Namen der Sitzung an, die getrennt werden soll.|
|/server:\<ServerName>|Gibt den Terminal Server an, der die Sitzung enthält, die Sie trennen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie müssen über die Berechtigung "Vollzugriff" verfügen oder eine spezielle Zugriffsberechtigung trennen, um einen anderen Benutzer von einer Sitzung zu trennen.
-   Wenn keine Sitzungs-ID oder kein Sitzungsname angegeben ist, wird die aktuelle Sitzung **von zdiscon** getrennt.
-   Alle Anwendungen, die ausgeführt wurden, als Sie die Sitzung getrennt haben, werden automatisch ausgeführt, wenn Sie die Verbindung zu dieser Sitzung ohne Datenverlust wiederherstellen. Verwenden Sie die **Reset-Sitzung** , um die ausgewendenden Anwendungen der getrennten Sitzung zu beenden, aber beachten Sie, dass dies zu einem Datenverlust in der Sitzung führen kann.
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie "out" von einem Remote **Server verwenden.**
-   Die Verbindung mit der Konsolen Sitzung kann nicht getrennt werden.

## <a name="examples"></a>Beispiele
- Geben Sie zum Trennen der aktuellen Sitzung Folgendes ein:
  ```
  tsdiscon
  ```
- Zum Trennen der Sitzung 10 geben Sie Folgendes ein:
  ```
  tsdiscon 10
  ```
- Geben Sie Folgendes ein, um die Sitzung mit dem Namen TERM04 zu trennen
  ```
  tsdiscon TERM04
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
