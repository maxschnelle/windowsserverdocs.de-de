---
title: list providers
description: Referenz Artikel für den Befehl list Providers, der Schattenkopieanbieter auflistet, die derzeit auf dem System registriert sind.
ms.topic: article
ms.assetid: 844b4036-c0b9-449d-8347-7d58ef9bf16d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81ca0a90276eeab824846f441ea9aa2a7396a009
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887627"
---
# <a name="list-providers"></a>list providers

Listet Schattenkopieanbieter auf, die derzeit auf dem System registriert sind.

## <a name="syntax"></a>Syntax

```
list providers
```

### <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)