---
title: nslookup lserver
description: Referenz Artikel für den nslookup lserver-Befehl, der den ursprünglichen Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7c478b6c9f3ae299559a556629e53f9eb852ee
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885794"
---
# <a name="nslookup-lserver"></a>nslookup lserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den ursprünglichen Server in die angegebene Domain Name System Domäne (DNS).

Dieser Befehl verwendet den anfänglichen Server, um die Informationen zur angegebenen DSN-Domäne zu suchen. Wenn Sie Informationen mithilfe des aktuellen Standard Servers suchen möchten, verwenden Sie den Befehl [nslookup Server](nslookup-server.md) .

## <a name="syntax"></a>Syntax

```
lserver <DNSdomain>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<DNSdomain>` | Gibt die DNS-Domäne für den ursprünglichen Server an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup server](nslookup-server.md)
