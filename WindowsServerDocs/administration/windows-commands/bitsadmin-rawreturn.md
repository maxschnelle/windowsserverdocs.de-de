---
title: bitsadmin rawreturn
description: Referenz Artikel für den Befehl bizadmin rawreturn, der für die Verarbeitung geeignete Daten zurückgibt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b537b21678c100364406d4c59eaa02efd143e21
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926465"
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
