---
title: Unterbefehl Start-Server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a89e3f17aeed7eb3156e28997206517342be109
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852041"
---
# <a name="subcommand-start-server"></a>Unterbefehl: Start-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

startet alle Dienste für einen Windows-Bereitstellungsdienste-Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers, der gestartet werden. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Um den Server zu starten, geben Sie eine der folgenden:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Get-Server-Befehl](using-the-get-server-command.md)
[mithilfe des Befehls Initialize-Server](using-the-initialize-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md) 
 [ Unterbefehl: Stop-Server](subcommand-stop-server.md)
[die Uninitialize-Server-Option](the-uninitialize-server-option.md)
