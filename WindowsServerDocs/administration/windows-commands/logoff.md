---
title: Abmelden
description: Referenz Thema für den Befehl "Abmelden", bei dem ein Benutzer von einer Sitzung auf einem Remotedesktop-Sitzungshost Server abgemeldet und die Sitzung gelöscht wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 636591843ce878bc85c5cccf6faece6652e25424
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222738"
---
# <a name="logoff"></a>Abmelden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Protokolliert einen Benutzer aus einer Sitzung auf einem Remotedesktop-Sitzungshost Server und löscht die Sitzung.

## <a name="syntax"></a>Syntax
```
logoff [<sessionname> | <sessionID>] [/server:<servername>] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<sessionname>` | Gibt den Namen der Sitzung an. Dabei muss es sich um eine aktive Sitzung handeln.|
| `<sessionID>` | Gibt die numerische ID an, die die Sitzung mit dem Server identifiziert. |
| /server:`<servername>` | Gibt den Remotedesktop-Sitzungshost Server an, der die Sitzung enthält, deren Benutzer Sie abmelden möchten. Wenn nicht angegeben, wird der Server verwendet, auf dem Sie zurzeit aktiv sind. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
