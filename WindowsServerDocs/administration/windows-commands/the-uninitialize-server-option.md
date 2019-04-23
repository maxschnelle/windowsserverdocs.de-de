---
title: Die Uninitialize-Server-Option
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 73f1ff67331ae41fa0d88cb3a16df5095e0b6d66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873981"
---
# <a name="the-uninitialize-server-option"></a>Die Uninitialize-Server-Option

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

setzt Änderungen an den Server während der ersten Server-Konfiguration zurück. Dies schließt Änderungen vorgenommen werden, indem Sie entweder die **/initialize-server** Option oder der Windows-Bereitstellungsdienste-Mmc-Snap-in. Beachten Sie, dass mit diesem Befehl den Server auf einem nicht konfigurierten Zustand zurückgesetzt. Dieser Befehl ändert nicht den Inhalt der freigegebenen Ordner "RemoteInstall". Stattdessen setzt es, damit Sie den Server neu initialisieren, können der Zustand des Servers zurück.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie einen der folgenden Schritte aus, um den Server erneut zu initialisieren:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Get-Server-Befehl](using-the-get-server-command.md)
[mithilfe des Befehls Initialize-Server](using-the-initialize-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md) 
 [ Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: Stop-Server](subcommand-stop-server.md)
