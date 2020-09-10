---
title: telnet open
description: Referenz Artikel für Telnet Open, das eine Verbindung mit einem Telnet-Server herstellt.
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 892d797c4b56acb46e8119237fd38296e4ae411c
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636784"
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
