---
title: nicht initialisieren-Server
description: Referenz Artikel für "Uninitialize-Server", mit dem die Änderungen auf dem Server während der anfänglichen Server Konfiguration wieder hergestellt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdbe391a7335c347f05f9f9c06bbade3474fa30e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935872"
---
# <a name="uninitialize-server"></a>nicht initialisieren-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kehrt die Änderungen zurück, die während der anfänglichen Serverkonfiguration auf dem Server vorgenommen wurden. Dies schließt Änderungen ein, die entweder von der **/Initialize-Server** -Option oder dem MMC-Snap-in Windows-Bereitstellungs Dienste vorgenommen werden. Beachten Sie, dass mit diesem Befehl der Server in einen nicht konfigurierten Zustand zurückgesetzt wird. Mit diesem Befehl wird der Inhalt des freigegebenen Ordners RemoteInstall nicht geändert. Stattdessen wird der Zustand des Servers zurückgesetzt, sodass Sie den Server erneut initialisieren können.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um den Server erneut zu initialisieren:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-enable-server-command.md) 
 "Enable-Server" [Verwenden des Befehls](using-the-get-server-command.md) 
 Get-Server [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Set-Server](subcommand-set-server.md) 
 [Unterbefehl: Start-Server](subcommand-start-server.md) 
 [Unterbefehl: "Ende-Server](subcommand-stop-server.md) "
