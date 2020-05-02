---
title: Unterbefehl "Ende-Transportserver"
description: Referenz Thema für "Ende-Transportserver"
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4321ec991b2c20911f992e4c3c38e5c9cfa5f165
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721620"
---
# <a name="subcommand-stop-transportserver"></a>Unterbefehl: "beendet-Transportserver"

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Transport Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Server angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe[des](using-the-disable-transportserver-command.md)
Befehls "Enable-Transportserver" mit dem Befehl "[enable-Transportserver](using-the-enable-transportserver-command.md)
" mit dem Befehl "[Get-TransportServer Command](using-the-get-transportserver-command.md)
[unter Command": Set-TransportServer](subcommand-set-transportserver.md)
[unter Command: Start-TransportServer](subcommand-start-transportserver.md)
