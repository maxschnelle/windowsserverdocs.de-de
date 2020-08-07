---
title: reset session
description: Referenz Artikel für * * * *-
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2f910dfc1c13b0e8555078acfb4e7ad830049592
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883659"
---
# <a name="reset-session"></a>reset session

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Zurücksetzen (Löschen) einer Sitzung auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).


> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11)) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|\<SessionName>|Gibt den Namen der Sitzung an, die Sie zurücksetzen möchten. Um den Namen der Sitzung zu ermitteln, verwenden Sie den Befehl **Abfrage Sitzung** .|
|\<SessionID>|Gibt die ID der zurück zusetzenden Sitzung an.|
|/server:\<ServerName>|Gibt den Terminal Server mit der Sitzung an, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
-   Sie können jederzeit eigene Sitzungen zurücksetzen, aber Sie müssen über die Berechtigung "Vollzugriff" verfügen, um die Sitzung eines anderen Benutzers zurückzusetzen.
-   Beachten Sie, dass das Zurücksetzen der Sitzung eines Benutzers ohne Warnung den Benutzer zum Verlust von Daten in der Sitzung führen kann.
-   Sie sollten eine Sitzung nur dann zurücksetzen, wenn Sie nicht mehr reagiert oder anscheinend nicht mehr reagiert.
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie die **Reset-Sitzung** von einem Remote Server aus verwenden.

## <a name="examples"></a>Beispiele
- Geben Sie Folgendes ein, um die für RDP-TCP # 6 vorgesehene Sitzung zurückzusetzen:
  ```
  reset session rdp-tcp#6
  ```
- Um die Sitzung zurückzusetzen, die Sitzungs-ID 3 verwendet, geben Sie Folgendes ein:
  ```
  reset session 3
  ```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
