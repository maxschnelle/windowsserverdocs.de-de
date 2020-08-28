---
title: nslookup server
description: Referenz Artikel zum nslookup-Server-Befehl, der den Standard Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: reference
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32450197fe7d3c04258b7fb3f77f8e17cd1c113e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038761"
---
# <a name="nslookup-server"></a>nslookup server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).

Dieser Befehl verwendet den aktuellen Standard Server, um die Informationen zur angegebenen DSN-Domäne zu suchen. Wenn Sie Informationen mithilfe des ersten Servers suchen möchten, verwenden Sie den Befehl [nslookup lserver](nslookup-lserver.md) .

## <a name="syntax"></a>Syntax

```
server <DNSdomain>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<DNSdomain>` | Gibt die DNS-Domäne für den Standard Server an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
