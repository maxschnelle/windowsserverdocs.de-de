---
title: nslookup set timeout
description: Referenz Artikel für den nslookup-Satz Timeout-Befehl, der die anfängliche Anzahl von Sekunden ändert, die auf eine Antwort auf eine Such Anforderung gewartet werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6df8d1229dd57a84cb0dced3829bb328e41f092c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930348"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Such Anforderung gewartet werden soll. Wenn eine Antwort nicht innerhalb der angegebenen Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Verwenden Sie den Befehl [nslookup Set Wiederholen Sie](nslookup-set-retry.md) , um zu bestimmen, wie oft versucht werden soll, die Anforderung zu senden.

## <a name="syntax"></a>Syntax

```
set timeout=<number>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ---------- |
| `<number>` | Gibt die Anzahl der Sekunden an, die auf eine Antwort gewartet werden soll. Die Standard Anzahl von Sekunden, die gewartet werden soll, ist **5**. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

So legen Sie das Timeout für das erhalten einer Antwort auf 2 Sekunden fest:

```
set timeout=2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set retry](nslookup-set-retry.md)
