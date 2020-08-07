---
title: bitsadmin util and enableanalyticchannel
description: Referenz Artikel zum Befehl "BITSAdmin util" und "enableanalyticchannel", der den analysekanal des BITS-Clients aktiviert oder deaktiviert.
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c4577f635444c1830e232e1baeb12fac8c75476
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880957"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util and enableanalyticchannel

Aktiviert oder deaktiviert den analysekanal des BITS-Clients.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| Parameter | BESCHREIBUNG |
| --------- | ---------- |
| TRUE oder false | **True** schaltet die Inhalts Überprüfung für die angegebene Datei ein, während **false** Sie deaktiviert. |

## <a name="examples"></a>Beispiele

, Um den analysekanal des BITS-Clients ein-oder auszuschalten.

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
