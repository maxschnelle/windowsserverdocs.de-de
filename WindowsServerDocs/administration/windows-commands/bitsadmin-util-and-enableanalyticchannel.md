---
title: bitsadmin util and enableanalyticchannel
description: Referenz Artikel zum Befehl "BITSAdmin util" und "enableanalyticchannel", der den analysekanal des BITS-Clients aktiviert oder deaktiviert.
ms.topic: reference
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 391b53694fcb21d1c17085d487908b090ad88f0a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630560"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util and enableanalyticchannel

Aktiviert oder deaktiviert den analysekanal des BITS-Clients.

## <a name="syntax"></a>Syntax

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| Parameter | BESCHREIBUNG |
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
