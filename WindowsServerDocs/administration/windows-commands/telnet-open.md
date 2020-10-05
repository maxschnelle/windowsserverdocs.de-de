---
title: telnet open
description: Referenz Artikel für den Telnet Open-Befehl, der eine Verbindung mit einem Telnet-Server herstellt.
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6db7f428f4b8c85c6e953a8fe4a9328b965898f8
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91718007"
---
# <a name="telnet-open"></a>Telnet: offen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einem Telnet-Server her.

## <a name="syntax"></a>Syntax

```
o[pen] <hostname> [<port>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<hostname>` | Gibt den Computernamen oder die IP-Adresse an. |
| `[<port>]` | Gibt den TCP-Port an, an dem der Telnet-Server lauscht. Der Standardwert ist TCP-Port 23. |

## <a name="examples"></a>Beispiele

Zum Herstellen einer Verbindung mit einem Telnet-Server unter *Telnet.Microsoft.com*geben Sie Folgendes ein:

```
o telnet.microsoft.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
