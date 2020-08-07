---
title: Unterbefehl Start-Server
description: Referenz Artikel für den Unterbefehl Start-Server, mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver gestartet werden.
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53fbc5ed80d69077efad49682368fbf3877361a0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882066"
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-enable-server-command.md) 
 "Enable-Server" [Verwenden des Befehls](using-the-get-server-command.md) 
 Get-Server [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Set-Server](subcommand-set-server.md) 
 [Unterbefehl: "Ende-Server](subcommand-stop-server.md) 
 " [Die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
