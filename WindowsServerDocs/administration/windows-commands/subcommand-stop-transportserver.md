---
title: Unterbefehl "Ende-Transportserver"
description: Windows-Befehls Thema für "Ende-Transportserver"
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44d62332307ffda4dcfa6af286c7b95cb12423dc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833703"
---
# <a name="subcommand-stop-transportserver"></a>Unterbefehl: "beendet-Transportserver"

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Transport Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Server angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "Enable [-Transportserver](using-the-disable-transportserver-command.md) "
mithilfe des Befehls [enable-Transportserver](using-the-enable-transportserver-command.md)
[mithilfe des Befehls Get-TransportServer](using-the-get-transportserver-command.md)
[Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
