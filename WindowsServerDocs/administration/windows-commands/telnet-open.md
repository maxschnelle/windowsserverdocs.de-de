---
title: telnet open
description: Referenz Artikel für Telnet Open, das eine Verbindung mit einem Telnet-Server herstellt.
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11498b2d2f38b96725608e6e72d30d0d563fd88a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881706"
---
# <a name="telnet-open"></a>Telnet: offen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Stellt eine Verbindung mit einem Telnet-Server her.

## <a name="syntax"></a>Syntax
```
o[pen] <hostname> [<Port>]
```
#### <a name="parameters"></a>Parameter

| Parameter  |                                        BESCHREIBUNG                                         |
|------------|--------------------------------------------------------------------------------------------|
| <hostname> |                         Gibt den Computernamen oder die IP-Adresse an.                         |
|  [<Port>]  | Gibt den TCP-Port an, an dem der Telnet-Server lauscht. Der Standardwert ist TCP-Port 23. |

## <a name="examples"></a>Beispiele
Herstellen einer Verbindung mit einem Telnet-Server unter Telnet.Microsoft.com.
```
o telnet.microsoft.com
```
## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
