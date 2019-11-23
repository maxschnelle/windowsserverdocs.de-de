---
title: nslookup set timeout
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32fcfcaeccb6599e9aaca21f9c085bb00857479c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372765"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Such Anforderung gewartet werden soll.
## <a name="syntax"></a>Syntax
```
set timeout=<Number>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                           Beschreibung                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | Gibt die Anzahl der Sekunden an, die auf eine Antwort gewartet werden soll. Die Standard Anzahl von Sekunden, die gewartet werden soll, ist 5. |
| {Help &#124; ?} |                      Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                       |

## <a name="remarks"></a>Hinweise
- Wenn eine Antwort auf eine Anforderung nicht innerhalb des angegebenen Zeitraums empfangen wird, wird das Timeout verdoppelt, und die Anforderung wird erneut gesendet. Sie können den Befehl **Set Wiederholen Sie** verwenden, um die Anzahl der Wiederholungen zu steuern.
  ## <a name="BKMK_examples"></a>Beispiele
  Im folgenden Beispiel wird das Timeout für das erhalten einer Antwort auf 2 Sekunden festgelegt:
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Satz Wiederholung](nslookup-set-retry.md)
