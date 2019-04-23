---
title: nslookup set retry
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 63d72a45c33da099c5936d625b27aa71ef002280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857661"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Legt die Anzahl von Wiederholungen fest.
## <a name="syntax"></a>Syntax
```
set retry=<Number>
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<Number>|Gibt den neuen Wert für die Anzahl der Wiederholungsversuche an. Die Standardanzahl von Wiederholungen ist 4.|
|{help &#124; ?}|Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.|
## <a name="remarks"></a>Hinweise
-   Wenn eine Antwort auf eine Anforderung nicht innerhalb einer bestimmten Zeitspanne empfangen wird, der Timeoutzeitraum verdoppelt, und die Anforderung erneut gesendet wird. Der Retry-Wert steuert, wie oft eine Anforderung gesendet wird, bevor aufgegeben wird. Sie können ändern, dass das Timeout mit der **Timeout festlegen** Unterbefehl.
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Nslookup Timeout festlegen](nslookup-set-timeout.md)
