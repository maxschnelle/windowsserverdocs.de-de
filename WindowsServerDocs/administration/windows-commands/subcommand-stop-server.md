---
title: Unterbefehl Stop-Server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddb681234cfcbe6d02e56f2e366167faeeb25280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834731"
---
# <a name="subcommand-stop-server"></a>Unterbefehl: Stop-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Beendet alle Dienste auf einem Windows-Bereitstellungsdiensteserver.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, um die Dienste zu beenden:
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Get-Server-Befehl](using-the-get-server-command.md)
[mithilfe des Befehls Initialize-Server](using-the-initialize-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md) 
 [ Unterbefehl: Start-Server](subcommand-start-server.md)
[die Uninitialize-Server-Option](the-uninitialize-server-option.md)
