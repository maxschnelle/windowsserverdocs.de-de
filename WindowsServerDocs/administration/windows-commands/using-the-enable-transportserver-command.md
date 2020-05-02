---
title: Enable-Transportserver
description: Referenz Thema zu enable-Transportserver, das alle Dienste für den Transport-Server aktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50cc381b1c178628be7d135868027b4f37787cdd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720920"
---
# <a name="enable-transportserver"></a>Enable-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für den Transport-Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Name angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-TransportServer
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "deaktivierte Transportserver](using-the-disable-transportserver-command.md)
[mit dem Befehl "Get-TransportServer Command](using-the-get-transportserver-command.md)
[unter Command": Set-TransportServer](subcommand-set-transportserver.md)
[unter Command: Start-TransportServer](subcommand-start-transportserver.md)
[unter Command:](subcommand-stop-transportserver.md) "Start-TransportServer"
