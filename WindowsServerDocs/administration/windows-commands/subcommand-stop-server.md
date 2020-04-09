---
title: Unterbefehl "Ende-Server"
description: Windows-Befehls Artikel für den Unterbefehl "Stopp-Server", der alle Dienste auf einem Windows-Bereitstellungsdiensteserver stoppt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2671e7a2c2e5bb542cecd9374ad6364d68ff5bd4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833713"
---
# <a name="subcommand-stop-server"></a>Unterbefehl: "Ende-Server"

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md) Befehls "Enable-Server"
mithilfe des Befehls " [enable-](using-the-enable-server-command.md) Server"
[mithilfe des Befehls "Get-Server](using-the-get-server-command.md) "
mit dem Befehl " [Initialize-Server](using-the-initialize-server-command.md) "
[Unterbefehl "Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[die Option" Uninitialize-Server](the-uninitialize-server-option.md) "
