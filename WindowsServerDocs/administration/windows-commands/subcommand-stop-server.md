---
title: Unterbefehl "Ende-Server"
description: Referenz Artikel für den Unterbefehl "Stopp-Server", der alle Dienste auf einem Windows-Bereitstellungsdiensteserver stoppt.
ms.topic: reference
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c84b95607b4cf0fb69765dbc941d7e984e43d7cf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626842"
---
# <a name="subcommand-stop-server"></a>Unterbefehl: "Ende-Server"

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-disable-server-command.md) 
 "deaktivierte Server" [Verwenden des Befehls](using-the-enable-server-command.md) 
 "Enable-Server" [Verwenden des Befehls](using-the-get-server-command.md) 
 Get-Server [Verwenden des Befehls](using-the-initialize-server-command.md) 
 "Initialize-Server" [Unterbefehl: Set-Server](subcommand-set-server.md) 
 [Unterbefehl: Start-Server](subcommand-start-server.md) 
 [Die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
