---
title: nslookup server
description: Referenz Artikel zum nslookup-Server-Befehl, der den Standard Server in die angegebene Domain Name System Domäne (DNS) ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec66534d475502ee68f9fabb58b214d25e6e0aaf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931258"
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
