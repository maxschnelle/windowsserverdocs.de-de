---
title: Abmelden
description: Referenz Artikel für den Befehl "Abmelden", bei dem ein Benutzer von einer Sitzung auf einem Remotedesktop-Sitzungshost Server abgemeldet und die Sitzung gelöscht wird.
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b8eb1b13d7eeddc03ead24bcda10062aea5e1cfe
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887075"
---
# <a name="logoff"></a>Abmelden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Protokolliert einen Benutzer aus einer Sitzung auf einem Remotedesktop-Sitzungshost Server und löscht die Sitzung.

## <a name="syntax"></a>Syntax
```
logoff [<sessionname> | <sessionID>] [/server:<servername>] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<sessionname>` | Gibt den Namen der Sitzung an. Dabei muss es sich um eine aktive Sitzung handeln.|
| `<sessionID>` | Gibt die numerische ID an, die die Sitzung mit dem Server identifiziert. |
| /server:`<servername>` | Gibt den Remotedesktop-Sitzungshost Server an, der die Sitzung enthält, deren Benutzer Sie abmelden möchten. Wenn nicht angegeben, wird der Server verwendet, auf dem Sie zurzeit aktiv sind. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Sie können sich jederzeit von der Sitzung abmelden, an der Sie gerade angemeldet sind. Sie müssen jedoch über die Berechtigung " **voll** Zugriff" verfügen, um Benutzer von anderen Sitzungen abzumelden.

- Wenn Sie einen Benutzer ohne Warnung aus einer Sitzung abmelden, kann dies zu Datenverlusten in der Sitzung des Benutzers führen. Sie sollten eine Nachricht an den Benutzer senden, indem Sie den Befehl " **msg** " verwenden, um den Benutzer vor der Durchführung dieser Aktion zu warnen.

- Wenn `<sessionID>` oder `<sessionname>` nicht angegeben wird **logoff** , protokolliert die Abmeldung den Benutzer aus der aktuellen Sitzung.

- Nachdem Sie einen Benutzer abmelden, werden alle Prozesse beendet, und die Sitzung wird vom Server gelöscht.

- Es ist nicht möglich, einen Benutzer von der Konsolen Sitzung aus abzumelden.

### <a name="examples"></a>Beispiele

Wenn Sie einen Benutzer aus der aktuellen Sitzung abmelden möchten, geben Sie Folgendes ein:

```
logoff
```

Wenn Sie einen Benutzer mithilfe der Sitzungs-ID von einer Sitzung abmelden möchten, z. b. *Sitzung 12*, geben Sie Folgendes ein:

```
logoff 12
```

Wenn Sie einen Benutzer mithilfe des Namens der Sitzung und des Servers von einer Sitzung abmelden möchten, z. b. Session *TERM04* on *Server1*, geben Sie Folgendes ein:

```
logoff TERM04 /server:Server1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
