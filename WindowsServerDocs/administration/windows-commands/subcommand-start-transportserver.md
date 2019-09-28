---
title: Unterbefehl Start-TransportServer
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1bdf80aa9c255e12e1e4821467d556eb67f8691
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370730"
---
# <a name="subcommand-start-transportserver"></a>Unterbefehl: Start-TransportServer

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

startet alle Dienste für einen Transport Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "deaktivierte Transportserver](using-the-disable-transportserver-command.md)" 
 mit dem Befehl "[enable-Transportserver](using-the-enable-transportserver-command.md)" 
 mit dem Befehl "[Get-](using-the-get-transportserver-command.md)Transportserver" 
[Unterbefehl: Set-TransportServer](subcommand-set-transportserver.md)
-[Unterbefehl: "Ende-Transportserver](subcommand-stop-transportserver.md) "
