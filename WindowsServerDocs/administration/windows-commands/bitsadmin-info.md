---
title: bitsadmin info
description: Referenz Artikel für den Befehl bizadmin Info, der zusammenfassende Informationen zum angegebenen Auftrag anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b9a284ee1e0ab8501f0fb6bc3417ca399996a08
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926555"
---
# <a name="bitsadmin-info"></a>bitsadmin info

Zeigt zusammenfassende Informationen zum angegebenen Auftrag an.

## <a name="syntax"></a>Syntax

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| /verbose | Dies ist optional. Stellt ausführliche Informationen zu jedem Auftrag bereit. |

## <a name="examples"></a>Beispiele

So rufen Sie Informationen zum Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
