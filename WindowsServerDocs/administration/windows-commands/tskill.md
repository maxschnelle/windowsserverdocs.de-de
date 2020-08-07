---
title: tskill
description: Referenz Artikel zu tskills, der einen Prozess beendet, der in einer Sitzung auf einem Remotedesktop-Sitzungshost Server ausgeführt wird.
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9fe3db1f218bc95fab4f3f2d917575679ab81931
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896678"
---
# <a name="tskill"></a>tskill

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet einen Prozess, der in einer Sitzung auf einem Remotedesktop-Sitzungshost Server ausgeführt wird.


> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11)) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|-------|--------|
|\<ProcessID>|Gibt die ID des Prozesses an, den Sie beenden möchten.|
|\<ProcessName>|Gibt den Namen des Prozesses an, den Sie beenden möchten. Dieser Parameter kann Platzhalter Zeichen enthalten.|
|/server:\<ServerName>|Gibt den Terminal Server an, der den Prozess enthält, den Sie beenden möchten. Wenn **/Server** nicht angegeben ist, wird der aktuelle RD-Sitzungshost Server verwendet.|
|/ID\<SessionID>|Beendet den Prozess, der in der angegebenen Sitzung ausgeführt wird.|
|/a|Beendet den Prozess, der in allen Sitzungen ausgeführt wird.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen
- Sie können **tskills** verwenden, um nur die Prozesse zu beenden, die Ihnen angehören, es sei denn, Sie sind ein Administrator. Administratoren haben Vollzugriff auf alle **tskills** -Funktionen und können Prozesse beenden, die in anderen Benutzersitzungen ausgeführt werden.
- Wenn alle Prozesse, die in einer Sitzung ausgeführt werden, beendet werden, wird die Sitzung ebenfalls beendet.
- Wenn Sie die Parameter " *ProcessName* " und " **/Server:**<em>Servername</em> " verwenden, müssen Sie auch den Parameter " **/ID:**<em>SessionID</em> " oder " **/a** " angeben.

## <a name="examples"></a>Beispiele
- Um den Prozess 6543 zu beenden, geben Sie Folgendes ein:
  ```
  tskill 6543
  ```
- Geben Sie Folgendes ein, um den Prozess-Explorer in Sitzung 5 zu beenden:
  ```
  tskill explorer /id:5
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
