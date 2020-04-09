---
title: Enable-Server
description: Windows-Befehls Thema für Enable-Server, mit dem alle Dienste für Windows-Bereitstellungs Dienste aktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b10ff920667cfdbaae5baaf096bf56e11ce880e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831543"
---
# <a name="enable-server"></a>Enable-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für die Windows-Bereitstellungs Dienste.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md) Befehls "debugserver"
mithilfe des Befehls " [Get-Server](using-the-get-server-command.md) "
[mit dem Befehl "Initialize-Server](using-the-initialize-server-command.md) "
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: beenden-Server](subcommand-stop-server.md)
[die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
