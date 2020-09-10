---
title: bitsadmin info
description: Referenz Artikel für den Befehl bizadmin Info, der zusammenfassende Informationen zum angegebenen Auftrag anzeigt.
ms.topic: reference
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 815fdc719d584f7d25f88705056e4d5c0c3405aa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631535"
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
| /verbose | (Optional) Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

So rufen Sie Informationen zum Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
