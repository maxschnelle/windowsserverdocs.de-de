---
title: lpq
description: Referenz Artikel für den lpq-Befehl, der den Status einer Druck Warteschlange auf einem Computer anzeigt, auf dem der liniendrucksdaemon (LPD) ausgeführt wird.
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 550e94455ed7c57e723edb6608c42820e81fba0b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887063"
---
# <a name="lpq"></a>lpq

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt den Status einer Druck Warteschlange auf einem Computer an, auf dem der Line Printer Daemon (LPD) ausgeführt wird.

## <a name="syntax"></a>Syntax

```
lpq -S <servername> -P <printername> [-l]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -S`<servername>` | Gibt (anhand des Namens oder der IP-Adresse) das Computer-oder Druckerfreigabe Gerät an, das die LPD-Drucker Warteschlange mit einem Status hostet, den Sie anzeigen möchten. Dieser Parameter ist erforderlich und muss groß geschrieben werden. |
| -P`<Printername>` | Gibt (nach Name) den Drucker für die Druck Warteschlange mit einem Status an, den Sie anzeigen möchten. Dieser Parameter ist erforderlich und muss groß geschrieben werden. |
| -l | Gibt an, dass Details zum Status der Druck Warteschlange angezeigt werden sollen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Wenn Sie den Status der *Laserprinter1* -Drucker Warteschlange auf einem LPD-Host unter *10.0.0.45*anzeigen möchten, geben Sie Folgendes ein:

```
lpq -S 10.0.0.45 -P Laserprinter1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
