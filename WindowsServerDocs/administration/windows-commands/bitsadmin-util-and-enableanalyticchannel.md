---
title: bitsadmin util and enableanalyticchannel
description: Referenz Artikel zum Befehl "BITSAdmin util" und "enableanalyticchannel", der den analysekanal des BITS-Clients aktiviert oder deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 515402f42dee54baa662f37718841f70b1cd2882
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927410"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util and enableanalyticchannel

Aktiviert oder deaktiviert den analysekanal des BITS-Clients.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| Parameter | Beschreibung |
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
