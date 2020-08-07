---
title: bitsadmin info
description: Referenz Artikel für den Befehl bizadmin Info, der zusammenfassende Informationen zum angegebenen Auftrag anzeigt.
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6cd93716b818b3f1981ceb54c0c049933f25a77
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893721"
---
# <a name="bitsadmin-info"></a>bitsadmin info

Zeigt zusammenfassende Informationen zum angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| /verbose | Optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

So rufen Sie Informationen zum Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
