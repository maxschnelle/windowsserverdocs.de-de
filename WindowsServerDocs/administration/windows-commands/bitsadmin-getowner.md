---
title: bitsadmin getowner
description: Referenz Artikel für den Befehl "bizadmin GetOwner", der den Besitzer des angegebenen Auftrags abruft.
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91dd63dcba8b41fee01c17e87c817e32a9dbba39
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894041"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Zeigt den anzeigen Amen oder die GUID des Besitzers des angegebenen Auftrags an.

## <a name="syntax"></a>Syntax

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So zeigen Sie den Besitzer des Auftrags mit dem Namen *mydownloadjob*an:

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
