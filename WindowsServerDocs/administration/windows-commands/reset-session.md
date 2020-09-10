---
title: reset session
description: Referenz Artikel zum Befehl zum Zurücksetzen der Sitzung, mit dem Sie eine Sitzung auf einem Remotedesktop-Sitzungshost Server zurücksetzen können.
ms.topic: reference
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 745a3ba51714ad3f5431dedbe9cebedf77e4ae72
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626913"
---
# <a name="reset-session"></a>reset session

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Zurücksetzen (Löschen) einer Sitzung auf einem Remotedesktop-Sitzungshost Server. Sie sollten eine Sitzung nur dann zurücksetzen, wenn Sie nicht mehr reagiert oder anscheinend nicht mehr reagiert.

> [!NOTE]
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
reset session {<sessionname> | <sessionID>} [/server:<servername>] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<sessionname>` | Gibt den Namen der Sitzung an, die Sie zurücksetzen möchten. Um den Namen der Sitzung zu ermitteln, verwenden Sie den [Befehl Abfrage Sitzung](query-session.md). |
| `<sessionID>` | Gibt die ID der zurück zusetzenden Sitzung an. |
| /server:`<servername>` | Gibt den Terminal Server mit der Sitzung an, die Sie zurücksetzen möchten. Andernfalls wird der aktuelle Remotedesktop-Sitzungshost Server verwendet. Dieser Parameter ist nur erforderlich, wenn Sie diesen Befehl von einem Remote Server aus verwenden. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="remarks"></a>Hinweise

- Sie können jederzeit eigene Sitzungen zurücksetzen, aber Sie müssen über die Berechtigung " **voll** Zugriff" verfügen, um die Sitzung eines anderen Benutzers zurückzusetzen. Beachten Sie, dass das Zurücksetzen der Sitzung eines Benutzers ohne Warnung den Benutzer zum Verlust von Daten in der Sitzung führen kann.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die für *RDP-TCP # 6*vorgesehene Sitzung zurückzusetzen:

```
reset session rdp-tcp#6
```

Um die Sitzung zurückzusetzen, die *Sitzungs-ID 3*verwendet, geben Sie Folgendes ein:

```
reset session 3
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
