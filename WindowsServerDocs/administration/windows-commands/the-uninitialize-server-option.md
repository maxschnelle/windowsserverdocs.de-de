---
title: Die Option "nicht initialisieren-Server"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c63e09738871c5b74c1b564a83c35ad28f4fa80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385593"
---
# <a name="the-uninitialize-server-option"></a>Die Option "nicht initialisieren-Server"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

kehrt die Änderungen zurück, die während der anfänglichen Serverkonfiguration auf dem Server vorgenommen wurden. Dies schließt Änderungen ein, die entweder von der **/Initialize-Server** -Option oder dem MMC-Snap-in Windows-Bereitstellungs Dienste vorgenommen werden. Beachten Sie, dass mit diesem Befehl der Server in einen nicht konfigurierten Zustand zurückgesetzt wird. Mit diesem Befehl wird der Inhalt des freigegebenen Ordners RemoteInstall nicht geändert. Stattdessen wird der Zustand des Servers zurückgesetzt, sodass Sie den Server erneut initialisieren können.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um den Server erneut zu initialisieren:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md)Befehls "Enable-Server" 
 mit dem Befehl "[enable-](using-the-enable-server-command.md)Server" 
 mithilfe des Befehls "[Get-](using-the-get-server-command.md)Server" 
 mit[dem Befehl "Initialize-Server](using-the-initialize-server-command.md)" 
[ Unterbefehl: Set-Server](subcommand-set-server.md)1[Unterbefehl: Start-Server](subcommand-start-server.md)3[Unterbefehl:-Server](subcommand-stop-server.md)
