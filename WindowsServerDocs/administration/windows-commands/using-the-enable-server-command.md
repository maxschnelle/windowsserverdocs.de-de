---
title: Enable-Server
description: Referenz Thema für Enable-Server, das alle Dienste für die Windows-Bereitstellungs Dienste ermöglicht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf7bf57c0784fa16719b9f77da50212bca0ef850
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720931"
---
# <a name="enable-server"></a>Enable-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für die Windows-Bereitstellungs Dienste.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "deaktivierte Server](using-the-disable-server-command.md)
" mithilfe des Befehls "[Get-Server](using-the-get-server-command.md)
[mit dem Befehl "Initialize-Server Command](using-the-initialize-server-command.md)
"[: Set-Server](subcommand-set-server.md)
[subcommand: Start-Server](subcommand-start-server.md)
[unter Command: beenden-Server](subcommand-stop-server.md)
[die Option "Uninitialize-Server](the-uninitialize-server-option.md) "
