---
title: nslookup set timeout
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1f6c8863d0a9330fd3a8499b0e6dbc802bd95022
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436508"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert die anfängliche Anzahl von Sekunden zu warten, bis eine Antwort an eine suchanforderung an.
## <a name="syntax"></a>Syntax
```
set timeout=<Number>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                           Beschreibung                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | Gibt die Anzahl von Sekunden auf eine Antwort warten. Die Standardanzahl von Sekunden ist 5. |
| {help &#124; ?} |                      Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.                       |

## <a name="remarks"></a>Hinweise
- Wenn eine Antwort auf eine Anforderung nicht innerhalb des angegebenen Zeitraums empfangen wird, wird das Timeout verdoppelt, und die Anforderung erneut gesendet wird. Können Sie die **Satz Wiederholung** Befehl aus, um die Anzahl von Wiederholungen zu steuern.
  ## <a name="BKMK_examples"></a>Beispiele für
  Im folgenden Beispiel wird das Timeout für das Empfangen einer Antwort auf 2 Sekunden:
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Nslookup legen Sie "Wiederholen"](nslookup-set-retry.md)
