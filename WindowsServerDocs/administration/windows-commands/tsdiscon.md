---
title: tsdiscon
description: Referenz Thema für "zdiscon", das eine Sitzung von einem Remote Desktop-Sitzungs Host Server trennt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2a97d1b157445fd43acce5a80f3d793ed5ae5af
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721264"
---
# <a name="tsdiscon"></a>tsdiscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Trennt eine Sitzung von einem Remotedesktop-Sitzungshost Server.



> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|\<SessionID->|Gibt die ID der Sitzung an, die getrennt werden soll.|
|\<Sessionname->|Gibt den Namen der Sitzung an, die getrennt werden soll.|
|/Server:\<Servername>|Gibt den Terminal Server an, der die Sitzung enthält, die Sie trennen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
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
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste Befehls Verweis (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
