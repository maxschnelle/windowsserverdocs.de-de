---
title: bdehdcfg restart
description: Referenz Artikel für den Befehl bdehdcfg Restart, der bdehdcfg mitteilt, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll.
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67d2a3dd7b4304c26543840d6681b4ec6e655651
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895100"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: neu starten

Informiert das Befehlszeilen Tool bdehdcfg darüber, dass der Computer nach Abschluss der Laufwerks Vorbereitung neu gestartet werden soll. Wenn andere Benutzer am Computer angemeldet sind und der Befehl **quiet** nicht angegeben ist, wird eine Eingabeaufforderung angezeigt, um zu bestätigen, dass der Computer neu gestartet werden muss.

## <a name="syntax"></a>Syntax

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge} -restart
```

#### <a name="parameters"></a>Parameter

Dieser Befehl weist keine zusätzlichen Parameter auf.

## <a name="examples"></a>Beispiele

So verwenden Sie den **Restart** -Befehl:

```
bdehdcfg -target default -restart
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
