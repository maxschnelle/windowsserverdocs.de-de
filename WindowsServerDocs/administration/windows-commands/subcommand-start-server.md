---
title: Unterbefehl Start-Server
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 78407f3474c48b928535abb652d2c023dd1c1c14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383818"
---
# <a name="subcommand-start-server"></a>Unterbefehl: Start-Server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

startet alle Dienste für einen Windows-Bereitstellungsdiensteserver.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an, der gestartet werden soll. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md)Befehls "Enable-Server" 
 mit dem Befehl "[enable-](using-the-enable-server-command.md)Server" 
 mithilfe des Befehls "[Get-](using-the-get-server-command.md)Server" 
 mit[dem Befehl "Initialize-Server](using-the-initialize-server-command.md)" 
[ Unterbefehl: Set-Server](subcommand-set-server.md)1[Unterbefehl: beenden-Server](subcommand-stop-server.md)3[die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
