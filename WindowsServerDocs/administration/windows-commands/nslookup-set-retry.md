---
title: nslookup set retry
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b95c4c8af2d7960270fd43f7a766b313ddbc07a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838343"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Anzahl der Wiederholungen fest.
## <a name="syntax"></a>Syntax
```
set retry=<Number>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                      Beschreibung                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | Gibt den neuen Wert für die Anzahl der Wiederholungs Versuche an. Die Standard Anzahl von Wiederholungen ist 4. |
| {Help &#124; ?} |                 Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                  |

## <a name="remarks"></a>Hinweise
- Wenn eine Antwort auf eine Anforderung nicht innerhalb einer bestimmten Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Der wiederholen Sie-Wert steuert, wie oft eine Anforderung erneut gesendet wird, bevor Sie den Vorgang aufgibt. Sie können den Timeout Zeitraum mit dem Unterbefehl **Set Timeout** ändern.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Satz Timeout](nslookup-set-timeout.md)
