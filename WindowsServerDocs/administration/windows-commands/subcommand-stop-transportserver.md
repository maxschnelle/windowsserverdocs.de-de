---
title: Unterbefehl "Ende-Transportserver"
description: Referenz Artikel für "Ende-Transportserver"
ms.topic: article
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49e7c0c61a110fc7a7aa687ff30d60eb8f51a543
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881964"
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-transportserver-command.md) 
 "deaktivierte Transport Server" [Verwenden des Befehls](using-the-enable-transportserver-command.md) 
 enable-Transportserver [Verwenden des Befehls](using-the-get-transportserver-command.md) 
 Get-TransportServer [Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md) 
 [Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
