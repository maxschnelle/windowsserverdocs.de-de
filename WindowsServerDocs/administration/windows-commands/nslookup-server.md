---
title: nslookup server
description: Referenz Artikel zum nslookup-Server-Befehl, der den Standard Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: reference
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 64d1383dd5c4fa86a62fad91bae0ed5e4eb1454b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635625"
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

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<DNSdomain>` | Gibt die DNS-Domäne für den Standard Server an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup lserver](nslookup-lserver.md)
