---
title: nslookup set retry
description: Referenz Artikel für den Befehl nslookup Set Wiederholen Sie, mit dem die Anzahl der Versuche zum Abrufen von Informationen von einem angegebenen Server festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ef38be2abfd423bb093ccf2b2ee6d701df28df3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935706"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn eine Antwort nicht innerhalb einer bestimmten Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Mit diesem Befehl wird festgelegt, wie oft eine Anforderung erneut an einen Server gesendet wird, um weitere Informationen zu erhalten.

> [!NOTE]
> Verwenden Sie den Befehl [nslookup Set Timeout](nslookup-set-timeout.md) , um die Zeitspanne zu ändern, bevor das Timeout der Anforderung abgelaufen ist.

## <a name="syntax"></a>Syntax

```
set retry=<number>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ---------- | ---------- |
| `<number>` | Gibt den neuen Wert für die Anzahl der Wiederholungs Versuche an. Die Standard Anzahl von Wiederholungen ist **4**. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set timeout](nslookup-set-timeout.md)
