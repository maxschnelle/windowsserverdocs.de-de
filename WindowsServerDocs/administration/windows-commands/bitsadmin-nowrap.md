---
title: bitsadmin nowrap
description: Referenz Artikel für den bizadmin-Befehl "nowrap", der jede Zeile von Ausgabetext abschneidet, der über den äußersten rechten Rand des Befehls Fensters hinausgeht.
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72c50bdf7d19ea4603fc232dcf54acdfd97d3f17
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893648"
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
