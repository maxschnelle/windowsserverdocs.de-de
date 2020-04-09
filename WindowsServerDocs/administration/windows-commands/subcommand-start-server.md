---
title: Unterbefehl Start-Server
description: Windows-Befehls Thema für den Unterbefehl Start-Server, der alle Dienste für einen Windows-Bereitstellungsdiensteserver startet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc3e0d11348dd6b531671e62139f2ce2c884c5ee
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833743"
---
# <a name="subcommand-start-server"></a>Unterbefehl: Start-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an, der gestartet werden soll. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md) Befehls "Enable-Server"
mithilfe des Befehls " [enable-](using-the-enable-server-command.md) Server"
[mithilfe des Befehls "Get-Server](using-the-get-server-command.md) "
mit dem Befehl " [Initialize-Server](using-the-initialize-server-command.md) "
[Unterbefehl "Set-Server](subcommand-set-server.md)
[Unterbefehl: beenden-Server](subcommand-stop-server.md)
[die Option" nicht initialisieren-Server](the-uninitialize-server-option.md) "
