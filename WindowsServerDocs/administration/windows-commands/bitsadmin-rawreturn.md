---
title: bitsadmin rawreturn
description: Referenz Artikel für den Befehl bizadmin rawreturn, der für die Verarbeitung geeignete Daten zurückgibt.
ms.topic: reference
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 286e84c16087cc000a6af29b3be53d529425dfde
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631216"
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
