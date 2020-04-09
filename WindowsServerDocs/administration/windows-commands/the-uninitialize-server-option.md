---
title: nicht initialisieren-Server
description: Windows-Befehls Thema für "Uninitialize-Server", mit dem die Änderungen auf dem Server während der anfänglichen Server Konfiguration wieder hergestellt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ed912af1ec3bc505e1e7465650a119af979b407
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833113"
---
# <a name="uninitialize-server"></a>nicht initialisieren-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kehrt die Änderungen zurück, die während der anfänglichen Serverkonfiguration auf dem Server vorgenommen wurden. Dies schließt Änderungen ein, die entweder von der **/Initialize-Server** -Option oder dem MMC-Snap-in Windows-Bereitstellungs Dienste vorgenommen werden. Beachten Sie, dass mit diesem Befehl der Server in einen nicht konfigurierten Zustand zurückgesetzt wird. Mit diesem Befehl wird der Inhalt des freigegebenen Ordners RemoteInstall nicht geändert. Stattdessen wird der Zustand des Servers zurückgesetzt, sodass Sie den Server erneut initialisieren können.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um den Server erneut zu initialisieren:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "Enable [-Server](using-the-disable-server-command.md) "
mithilfe des Befehls " [enable-](using-the-enable-server-command.md) Server"
[mithilfe des Befehls "Get-Server](using-the-get-server-command.md) "
mit dem Befehl [Initialize-Server](using-the-initialize-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: beenden-Server](subcommand-stop-server.md)
