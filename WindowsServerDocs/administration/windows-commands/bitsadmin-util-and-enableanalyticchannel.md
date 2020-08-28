---
title: bitsadmin util and enableanalyticchannel
description: Referenz Artikel zum Befehl "BITSAdmin util" und "enableanalyticchannel", der den analysekanal des BITS-Clients aktiviert oder deaktiviert.
ms.topic: reference
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b4b6dd18fada99d63fcea7e3ca7338567fcb3894
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033338"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util and enableanalyticchannel

Aktiviert oder deaktiviert den analysekanal des BITS-Clients.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| Parameter | Beschreibung |
| --------- | ---------- |
| TRUE oder FALSE | **True** schaltet die Inhalts Überprüfung für die angegebene Datei ein, während **false** Sie deaktiviert. |

## <a name="examples"></a>Beispiele

, Um den analysekanal des BITS-Clients ein-oder auszuschalten.

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "BIFS admin util"](bitsadmin-util.md)

- [Bider admin-Befehl](bitsadmin.md)
