---
title: Unterbefehl Start-Server
description: Referenz Thema für den Unterbefehl Start-Server, mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver gestartet werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2a6de007e62bf3be5544f97b53a4fcc13118985
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721650"
---
# <a name="subcommand-start-server"></a>Unterbefehl: Start-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an, der gestartet werden soll. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem](using-the-disable-server-command.md)
Befehl "Enable-Server" unter Verwendung des Befehls "[enable](using-the-enable-server-command.md)
-Server" mithilfe des Befehls "[Get-Server](using-the-get-server-command.md)
" mit dem[Subcommand: stop-Server](subcommand-stop-server.md)
[The uninitialize-Server Option](the-uninitialize-server-option.md) [Befehl "](subcommand-set-server.md)
[Initialize-Server](using-the-initialize-server-command.md)
"
