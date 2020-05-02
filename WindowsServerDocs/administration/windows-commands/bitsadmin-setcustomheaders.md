---
title: bitsadmin setcustomheaders
description: Referenz Thema für den Befehl "bizadmin setcustomheaders", mit dem eine GET-Anforderung mit einem benutzerdefinierten HTTP-Header hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 92728f8d63a22cf9d13d6c02a69359583a9fc5cc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719325"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

Hinzufügen eines benutzerdefinierten HTTP-Headers zu einer GET-Anforderung, die an einen HTTP-Server gesendet wird Weitere Informationen zu Get-Anforderungen finden Sie unter [Methoden Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) und [Header Feld Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

## <a name="syntax"></a>Syntax

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<header1> <header2>`Und so weiter | Die benutzerdefinierten Header für den Auftrag. |

## <a name="examples"></a>Beispiele

So fügen Sie einen benutzerdefinierten HTTP-Header für den Auftrag *mydownloadjob*hinzu:

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
