---
title: bitsadmin nowrap
description: Referenz Artikel für den bizadmin-Befehl "nowrap", der jede Zeile von Ausgabetext abschneidet, der über den äußersten rechten Rand des Befehls Fensters hinausgeht.
ms.topic: reference
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e5724f3dedb808898cd070026e2e4a944d4731b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631421"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

Verkürzt jede Zeile von Ausgabetext, der über den rechten Rand des Befehls Fensters hinausgeht. Standardmäßig wird die Ausgabe durch alle Switches außer dem **Monitor** Switch umschlossen. Geben Sie den Schalter " **nowrap** " vor anderen Switches an.

## <a name="syntax"></a>Syntax

```
bitsadmin /nowrap
```

## <a name="examples"></a>Beispiele

So rufen Sie den Status des Auftrags mit dem Namen " *mydownloadjob* " ab, ohne die Ausgabe zu umbenennen:

```
bitsadmin /nowrap /getstate myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
