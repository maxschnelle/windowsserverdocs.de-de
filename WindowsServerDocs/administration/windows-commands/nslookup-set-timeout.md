---
title: nslookup set timeout
description: Referenz Thema für den nslookup-Satz Timeout-Befehl, der die anfängliche Anzahl von Sekunden ändert, die auf eine Antwort auf eine Such Anforderung gewartet werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d8fd0d96226e193ba723cc0a726ddf5362a538c
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721385"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert die anfängliche Anzahl von Sekunden, die auf eine Antwort auf eine Such Anforderung gewartet werden soll. Wenn eine Antwort nicht innerhalb der angegebenen Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Verwenden Sie den Befehl [nslookup Set Wiederholen Sie](nslookup-set-retry.md) , um zu bestimmen, wie oft versucht werden soll, die Anforderung zu senden.

## <a name="syntax"></a>Syntax

```
set timeout=<number>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| ---------- | ---------- |
| `<number>` | Gibt die Anzahl der Sekunden an, die auf eine Antwort gewartet werden soll. Die Standard Anzahl von Sekunden, die gewartet werden soll, ist **5**. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

So legen Sie das Timeout für das erhalten einer Antwort auf 2 Sekunden fest:

```
set timeout=2
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set retry](nslookup-set-retry.md)
