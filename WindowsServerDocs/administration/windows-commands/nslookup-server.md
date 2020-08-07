---
title: nslookup server
description: Referenz Artikel zum nslookup-Server-Befehl, der den Standard Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eacb1807810627956fcf75455e861d3ac381cf13
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885780"
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
