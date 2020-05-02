---
title: Get-TransportServer
description: Referenz Thema zu Get-TransportServer, das Informationen zu einem angegebenen Transport Server anzeigt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82ab5f901240f964bd22e7fb8053ed95b1c6fe51
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719726"
---
# <a name="get-transportserver"></a>Get-TransportServer

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem angegebenen Transport Server an.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config}|Gibt Konfigurationsinformationen zum angegebenen Transport Server zurück.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-TransportServer /Show:Config
```
Geben Sie Folgendes ein, um die Konfigurationsinformationen anzuzeigen:
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "Enable-Transportserver](using-the-disable-transportserver-command.md)
"[mit dem Befehl enable-Transportserver Command](using-the-enable-transportserver-command.md)
[unter Command: Set-TransportServer](subcommand-set-transportserver.md)
[subcommand: Start-TransportServer](subcommand-start-transportserver.md)
[unter Command:-Transportserver](subcommand-stop-transportserver.md)
