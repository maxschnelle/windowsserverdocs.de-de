---
title: Enable-Transportserver
description: Referenz Artikel zu enable-Transportserver, mit dem alle Dienste für den Transport Server aktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d4cd87b78e7a84255593464fede553bc294138c7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936270"
---
# <a name="enable-transportserver"></a>Enable-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für den Transport-Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Name angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-TransportServer
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-transportserver-command.md) 
 "deaktivierte Transport Server" [Verwenden des Befehls](using-the-get-transportserver-command.md) 
 Get-TransportServer [Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md) 
 [Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md) 
 [Unterbefehl: "beendet-Transportserver](subcommand-stop-transportserver.md) "
