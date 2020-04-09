---
title: Unterbefehl Start-TransportServer
description: Windows-Befehls Thema für den Unterbefehl Start-TransportServer, mit dem alle Dienste für einen Transport Server gestartet werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1356d415006324d75783d4e12ad6882d0fcc779
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833753"
---
# <a name="subcommand-start-transportserver"></a>Unterbefehl: Start-TransportServer

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "Enable [-Transportserver](using-the-disable-transportserver-command.md) "
mithilfe des Befehls [enable-Transportserver](using-the-enable-transportserver-command.md)
[mithilfe des Befehls Get-TransportServer](using-the-get-transportserver-command.md)
[Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl:](subcommand-stop-transportserver.md) "Set-TransportServer".
