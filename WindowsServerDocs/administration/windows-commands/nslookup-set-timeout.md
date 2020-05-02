---
title: nslookup set timeout
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68e9630b9690c9b6c9d4c316f8b328897289362c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723544"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Such Anforderung gewartet werden soll.
## <a name="syntax"></a>Syntax
```
set timeout=<Number>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                           BESCHREIBUNG                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | Gibt die Anzahl der Sekunden an, die auf eine Antwort gewartet werden soll. Die Standard Anzahl von Sekunden, die gewartet werden soll, ist 5. |
| {Help &#124;?} |                      Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                       |

## <a name="remarks"></a>Bemerkungen
- Wenn eine Antwort auf eine Anforderung nicht innerhalb des angegebenen Zeitraums empfangen wird, wird das Timeout verdoppelt, und die Anforderung wird erneut gesendet. Sie können den Befehl **Set Wiederholen Sie** verwenden, um die Anzahl der Wiederholungen zu steuern.
  ## <a name="examples"></a>Beispiele
  So legen Sie das Timeout für das erhalten einer Antwort auf 2 Sekunden fest:
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup Set Wiederholungsversuch](nslookup-set-retry.md)
