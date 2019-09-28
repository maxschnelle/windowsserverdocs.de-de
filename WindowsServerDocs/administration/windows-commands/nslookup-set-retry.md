---
title: nslookup set retry
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 306bcc4f5e7ac98767c3c2e274100cf917874a8e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372858"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Legt die Anzahl der Wiederholungen fest.
## <a name="syntax"></a>Syntax
```
set retry=<Number>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                      Beschreibung                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | Gibt den neuen Wert für die Anzahl der Wiederholungs Versuche an. Die Standard Anzahl von Wiederholungen ist 4. |
| {Help &#124; ?} |                 Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                  |

## <a name="remarks"></a>Hinweise
- Wenn eine Antwort auf eine Anforderung nicht innerhalb einer bestimmten Zeitspanne empfangen wird, wird der Timeout Zeitraum verdoppelt, und die Anforderung wird erneut gesendet. Der wiederholen Sie-Wert steuert, wie oft eine Anforderung erneut gesendet wird, bevor Sie den Vorgang aufgibt. Sie können den Timeout Zeitraum mit dem Unterbefehl **Set Timeout** ändern.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Satz Timeout](nslookup-set-timeout.md)
