---
title: Deaktivieren-Transportserver
description: Windows-Befehls Thema für "deaktivieren-Transportserver", mit dem alle Dienste für einen Transport Server deaktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39f930a464364cda680098ef4e7e1081d0995503
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831623"
---
# <a name="disable-transportserver"></a>Deaktivieren-Transportserver

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des zu deaktivierenden Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um den Server zu deaktivieren, geben Sie Folgendes ein:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls Enable-Transportserver](using-the-enable-transportserver-command.md)
[mithilfe des Befehls Get-TransportServer](using-the-get-transportserver-command.md)
[Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-stop-transportserver.md)
