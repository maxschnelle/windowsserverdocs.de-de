---
title: Telnet geöffnet
description: Referenz Thema für Telnet Open, das eine Verbindung mit einem Telnet-Server herstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
s.topic: article
ms.assetid: e30ad68c-2366-4754-ac36-311a2392902a vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed2c00b44143942ba1ccb77eec17ca975f23b498
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821320"
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
