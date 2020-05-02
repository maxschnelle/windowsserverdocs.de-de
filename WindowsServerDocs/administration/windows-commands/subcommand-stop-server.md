---
title: Unterbefehl "Ende-Server"
description: Referenz Thema für den Unterbefehl "Stopp-Server", der alle Dienste auf einem Windows-Bereitstellungsdiensteserver stoppt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68cc73ac016e2ffded774567034801e1c11944d1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721631"
---
# <a name="subcommand-stop-server"></a>Unterbefehl: "Ende-Server"

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem](using-the-disable-server-command.md)
Befehl "Enable-Server" unter Verwendung des Befehls "[enable](using-the-enable-server-command.md)
-Server" mithilfe des Befehls "[Get-Server](using-the-get-server-command.md)
" mit dem[Befehl "](subcommand-set-server.md)
[Subcommand: start-Server](subcommand-start-server.md)
[The uninitialize-Server Option](the-uninitialize-server-option.md) [Initialize-Server](using-the-initialize-server-command.md)
"
