---
title: tsdiscon
description: Referenz Artikel für "zdiscon", der eine Sitzung von einem Remotedesktop-Sitzungshost Server trennt.
ms.topic: reference
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8b7126e2e9d1f5185ea64566843c523bf0570891
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156388"
---
# <a name="tsdiscon"></a>tsdiscon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Trennt eine Sitzung von einem Remotedesktop-Sitzungshost Server. Wenn Sie keine Sitzungs-ID oder Sitzungsname angeben, trennt dieser Befehl die Verbindung mit der aktuellen Sitzung.

> [!IMPORTANT]
> Sie müssen über die Berechtigung " **Vollzugriff** " verfügen oder eine **spezielle Zugriffsberechtigung trennen** , um einen anderen Benutzer von einer Sitzung zu trennen.

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
tsdiscon [<sessionID> | <sessionname>] [/server:<servername>] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<sessionID>` | Gibt die ID der Sitzung an, die getrennt werden soll. |
| `<sessionname>` | Gibt den Namen der Sitzung an, die getrennt werden soll. |
| /server:`<servername>` | Gibt den Terminal Server an, der die Sitzung enthält, die Sie trennen möchten. Andernfalls wird der aktuelle Remotedesktop-Sitzungshost Server verwendet. Dieser Parameter ist nur erforderlich, wenn Sie den Befehl " **sdiscon** " von einem Remote Server aus ausführen. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Alle Anwendungen, die ausgeführt werden, wenn Sie die Sitzung getrennt haben, werden automatisch ausgeführt, wenn Sie die Verbindung zu dieser Sitzung ohne Datenverlust wiederherstellen. Mit dem [Befehl Sitzung zurücksetzen](reset-session.md) können Sie die ausgewendenden Anwendungen der getrennten Sitzung beenden, dies kann jedoch zu einem Datenverlust in der Sitzung führen.

- Die Konsolen Sitzung kann nicht getrennt werden.

## <a name="examples"></a>Beispiele

Geben Sie zum Trennen der aktuellen Sitzung Folgendes ein:

```
tsdiscon
```

Zum Trennen der *Sitzung 10*geben Sie Folgendes ein:

```
tsdiscon 10
```

Geben Sie Folgendes ein, um die Sitzung mit dem Namen *TERM04*zu trennen

```
tsdiscon TERM04
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)

- [Sitzungs Befehl Zurücksetzen](reset-session.md)
