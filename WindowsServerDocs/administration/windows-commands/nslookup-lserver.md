---
title: nslookup lserver
description: Referenz Artikel für den nslookup lserver-Befehl, der den ursprünglichen Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: reference
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d1f507b1a61e9fd4fc506fb4e74f869c83e95335
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635673"
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
