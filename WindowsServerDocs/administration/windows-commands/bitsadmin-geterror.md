---
title: bitsadmin geterror
description: Referenz Artikel für den bizadmin getError-Befehl, mit dem ausführliche Fehlerinformationen für den angegebenen Auftrag abgerufen werden.
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae0b2391267ddc1508d8343b909b9739a0e01ffb
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894358"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

Ruft ausführliche Fehlerinformationen für den angegebenen Auftrag ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Fehlerinformationen für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
