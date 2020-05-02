---
title: Anbieter auflisten
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 844b4036-c0b9-449d-8347-7d58ef9bf16d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761099e3b399aeb9e6a3fe1ddd53ed1a667a4ccb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724503"
---
# <a name="list-providers"></a>Anbieter auflisten



Listet Schattenkopieanbieter auf, die derzeit auf dem System registriert sind.



## <a name="syntax"></a>Syntax

```
list providers
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die derzeit registrierten Schattenkopieanbieter aufzulisten:
```
list providers
```
Ausgabe, die den folgenden anzeigen ähnelt:
```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)