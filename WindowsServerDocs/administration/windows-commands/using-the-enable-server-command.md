---
title: Enable-Server
description: Referenz Artikel zu enable-Server, mit dem alle Dienste für die Windows-Bereitstellungs Dienste aktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a0c82614049540e658061bd55bf40f0d0b3beb16
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936823"
---
# <a name="enable-server"></a>Enable-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für die Windows-Bereitstellungs Dienste.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-get-server-command.md) 
 Get-Server [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Set-Server](subcommand-set-server.md) 
 [Unterbefehl: Start-Server](subcommand-start-server.md) 
 [Unterbefehl: "Ende-Server](subcommand-stop-server.md) 
 " [Die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
