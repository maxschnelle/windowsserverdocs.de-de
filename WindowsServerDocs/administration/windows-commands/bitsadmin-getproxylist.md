---
title: 'BI-admin getproxylist: Ruft die Proxy Liste für den angegebenen Auftrag ab.'
description: Referenz Artikel für den bizadmin getproxylist-Befehl, der die Proxy Liste für den angegebenen Auftrag abruft.
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bcd94c65a11006a795f071224397d8b3081b7548
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893976"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

Ruft die durch Trennzeichen getrennte Liste der Proxy Server ab, die für den angegebenen Auftrag verwendet werden sollen.

## <a name="syntax"></a>Syntax

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

Zum Abrufen der Proxy Liste für den Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
