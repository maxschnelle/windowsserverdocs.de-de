---
title: nslookup set timeout
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8506511fc203f94d395851471f6a981ef0765928
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838273"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Such Anforderung gewartet werden soll.
## <a name="syntax"></a>Syntax
```
set timeout=<Number>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                           Beschreibung                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | Gibt die Anzahl der Sekunden an, die auf eine Antwort gewartet werden soll. Die Standard Anzahl von Sekunden, die gewartet werden soll, ist 5. |
| {Help &#124; ?} |                      Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                       |

## <a name="remarks"></a>Hinweise
- Wenn eine Antwort auf eine Anforderung nicht innerhalb des angegebenen Zeitraums empfangen wird, wird das Timeout verdoppelt, und die Anforderung wird erneut gesendet. Sie können den Befehl **Set Wiederholen Sie** verwenden, um die Anzahl der Wiederholungen zu steuern.
  ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
  Im folgenden Beispiel wird das Timeout für das erhalten einer Antwort auf 2 Sekunden festgelegt:
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Satz Wiederholung](nslookup-set-retry.md)
