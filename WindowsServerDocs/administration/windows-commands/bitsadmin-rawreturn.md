---
title: bitsadmin rawreturn
description: Referenz Artikel für den Befehl bizadmin rawreturn, der für die Verarbeitung geeignete Daten zurückgibt.
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88b1e45d7fad2820a77d9f445065ae0ca182abb6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893425"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

Gibt Daten zurück, die für die-Verarbeitung geeignet sind. In der Regel verwenden Sie diesen Befehl zusammen mit den Switches **/Create** und **/Get***, um nur den Wert zu erhalten. Dieser Switch muss vor anderen Schaltern angegeben werden.

> [!NOTE]
> Dieser Befehl entfernt Zeilen mit Zeilen und Formatierungen aus der Ausgabe.

## <a name="syntax"></a>Syntax

```
bitsadmin /rawreturn
```

## <a name="examples"></a>Beispiele

So rufen Sie die Rohdaten für den Status des Auftrags mit dem Namen *mydownloadjob*ab:

```
bitsadmin /rawreturn /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
