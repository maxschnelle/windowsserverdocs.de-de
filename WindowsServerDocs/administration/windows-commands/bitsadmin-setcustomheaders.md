---
title: bitsadmin setcustomheaders
description: Referenz Artikel für den Befehl "bizadmin setcustomheaders", mit dem eine GET-Anforderung mit einem benutzerdefinierten HTTP-Header hinzugefügt wird.
ms.topic: reference
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84622cba8bb2bcb6a9ebfe782fdadc33a388fdb2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031278"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

Hinzufügen eines benutzerdefinierten HTTP-Headers zu einer GET-Anforderung, die an einen HTTP-Server gesendet wird Weitere Informationen zu Get-Anforderungen finden Sie unter [Methoden Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) und [Header Feld Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

## <a name="syntax"></a>Syntax

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<header1> <header2>` Und so weiter | Die benutzerdefinierten Header für den Auftrag. |

## <a name="examples"></a>Beispiele

So fügen Sie einen benutzerdefinierten HTTP-Header für den Auftrag *mydownloadjob*hinzu:

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
