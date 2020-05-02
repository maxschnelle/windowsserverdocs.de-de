---
title: Deaktivieren-Transportserver
description: Referenz Thema für "deaktivieren-Transportserver", mit dem alle Dienste für einen Transport Server deaktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81ae150b4f8e4de577e377a2d10a7a69675adac7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720957"
---
# <a name="disable-transportserver"></a>Deaktivieren-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des zu deaktivierenden Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu deaktivieren, geben Sie Folgendes ein:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Enable-Transportserver](using-the-enable-transportserver-command.md)
[mit dem Befehl Get-TransportServer Command](using-the-get-transportserver-command.md)
[unter Command: Set-TransportServer](subcommand-set-transportserver.md)
[unter Command: Start-TransportServer](subcommand-start-transportserver.md)
[unter Command:-Transportserver](subcommand-stop-transportserver.md)
