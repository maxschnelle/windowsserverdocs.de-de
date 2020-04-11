---
title: bitadmin setcustomheaders
description: Windows-Befehls Thema für **BI-admin setcustomheaders**, das einer GET-Anforderung einen benutzerdefinierten HTTP-Header hinzufügt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5b1a28f03815a22a3f8d10b2c3d1d4a3a2ae635
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123025"
---
# <a name="bitsadmin-setcustomheaders"></a>bitadmin setcustomheaders

Hinzufügen eines benutzerdefinierten HTTP-Headers zu einer GET-Anforderung, die an einen HTTP-Server gesendet wird

## <a name="syntax"></a>Syntax

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| `<header1> <header2>` usw. | Die benutzerdefinierten Header für den Auftrag. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird ein benutzerdefinierter HTTP-Header für den Auftrag mit dem Namen *mydownloadjob*hinzugefügt. Weitere Informationen zu Get-Anforderungen finden Sie unter [Methoden Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) und [Header Feld Definitionen](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

```
C:\>bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)