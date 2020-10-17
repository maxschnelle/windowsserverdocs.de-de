---
title: tskill
description: Referenz Artikel für den tskills-Befehl, mit dem ein Prozess beendet wird, der in einer Sitzung auf einem Remotedesktop-Sitzungshost Server ausgeführt wird.
ms.topic: reference
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b281df4852bc5fbc0756e7b052d82ea2f9bab6d5
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156373"
---
# <a name="tskill"></a>tskill

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet einen Prozess, der in einer Sitzung auf einem Remotedesktop-Sitzungshost Server ausgeführt wird.

> [!NOTE]
> Sie können diesen Befehl verwenden, um nur die Prozesse zu beenden, die Ihnen angehören, es sei denn, Sie sind ein Administrator. Administratoren haben Vollzugriff auf alle **tskills** -Funktionen und können Prozesse beenden, die in anderen Benutzersitzungen ausgeführt werden.
>
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
tskill {<processID> | <processname>} [/server:<servername>] [/id:<sessionID> | /a] [/v]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<processID>` | Gibt die ID des Prozesses an, den Sie beenden möchten. |
| `<processname>` | Gibt den Namen des Prozesses an, den Sie beenden möchten. Dieser Parameter kann Platzhalter Zeichen enthalten. |
| /server:`<servername>` | Gibt den Terminal Server an, der den Prozess enthält, den Sie beenden möchten. Wenn **/Server** nicht angegeben ist, wird der aktuelle Remotedesktop-Sitzungshost Server verwendet. |
| /ID`<sessionID>` | Beendet den Prozess, der in der angegebenen Sitzung ausgeführt wird. |
| /a | Beendet den Prozess, der in allen Sitzungen ausgeführt wird. |
| /v | Zeigt Informationen zu den Aktionen an, die ausgeführt werden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn alle Prozesse, die in einer Sitzung ausgeführt werden, beendet werden, wird die Sitzung ebenfalls beendet.

- Wenn Sie den `<processname>` -Parameter und den- `/server:<servername>` Parameter verwenden, müssen Sie auch den- `/id:<sessionID>` Parameter oder den **/a** -Parameter angeben.

## <a name="examples"></a>Beispiele

Um den Prozess 6543 zu beenden, geben Sie Folgendes ein:

```
tskill 6543
```

Geben Sie Folgendes ein, um den Prozess-Explorer in Sitzung 5 zu beenden:

```
tskill explorer /id:5
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
