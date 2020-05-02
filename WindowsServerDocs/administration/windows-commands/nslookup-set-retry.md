---
title: nslookup set retry
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1baeeaefedc211434f46bd0cfad713f093a873bf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723585"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Anzahl der Wiederholungen fest.
## <a name="syntax"></a>Syntax
```
set retry=<Number>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                      BESCHREIBUNG                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | Gibt den neuen Wert für die Anzahl der Wiederholungs Versuche an. Die Standard Anzahl von Wiederholungen ist 4. |
| {Help &#124;?} |                 Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                  |

## <a name="remarks"></a>Bemerkungen
- Wenn eine Antwort auf eine Anforderung nicht innerhalb einer bestimmten Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Der wiederholen Sie-Wert steuert, wie oft eine Anforderung erneut gesendet wird, bevor Sie den Vorgang aufgibt. Sie können den Timeout Zeitraum mit dem Unterbefehl **Set Timeout** ändern.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup Satz Timeout](nslookup-set-timeout.md)
