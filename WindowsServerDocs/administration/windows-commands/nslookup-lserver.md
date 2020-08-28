---
title: nslookup lserver
description: Referenz Artikel für den nslookup lserver-Befehl, der den ursprünglichen Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: reference
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99d3dbeac4073b35abd540c185e4cf69b723b61e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023474"
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

| Parameter | Beschreibung |
| --------- | ----------- |
| `<DNSdomain>` | Gibt die DNS-Domäne für den ursprünglichen Server an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup server](nslookup-server.md)
