---
title: Verwenden des Befehls Get-TransportServer
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 282b69162cf3550c5bcba3282b60f15072c96ed6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363070"
---
# <a name="using-the-get-transportserver-command"></a>Verwenden des Befehls Get-TransportServer

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem angegebenen Transport Server an.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config}|Gibt Konfigurationsinformationen zum angegebenen Transport Server zurück.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-TransportServer /Show:Config
```
Geben Sie Folgendes ein, um die Konfigurationsinformationen anzuzeigen:
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "Enable-Transportserver](using-the-disable-transportserver-command.md)" 
[mit dem Befehl enable-Transportserver](using-the-enable-transportserver-command.md)
[unter Command: Set-TransportServer](subcommand-set-transportserver.md)
[Unterbefehl: Start-TransportServer](subcommand-start-transportserver.md)
-[Unterbefehl: "stoppt-Transportserver](subcommand-stop-transportserver.md) "
