---
title: Unterbefehl Start-TransportServer
description: Referenz Artikel für den Unterbefehl Start-TransportServer, mit dem alle Dienste für einen Transport Server gestartet werden.
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8236079d895a5ec94cab03009c2f31ddd7ef66d5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882029"
---
# <a name="subcommand-start-transportserver"></a>Unterbefehl: Start-TransportServer

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-transportserver-command.md) 
 "deaktivierte Transport Server" [Verwenden des Befehls](using-the-enable-transportserver-command.md) 
 enable-Transportserver [Verwenden des Befehls](using-the-get-transportserver-command.md) 
 Get-TransportServer [Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md) 
 [Unterbefehl: "beendet-Transportserver](subcommand-stop-transportserver.md) "
