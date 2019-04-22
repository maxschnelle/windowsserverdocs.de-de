---
title: Mithilfe des Befehls Initialize-Server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a1f3a1c02eb21f630aaff7219610864cd1db2a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825191"
---
# <a name="using-the-initialize-server-command"></a>Mithilfe des Befehls Initialize-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Einen Windows-Bereitstellungsdienste-Server für die Erstverwendung konfiguriert, nach der Installation der Serverrolle. Nachdem Sie diesen Befehl ausführen, sollten Sie verwenden die [mit dem Befehl-Add-Image](using-the-add-image-command.md) Befehl zum Hinzufügen von Bildern mit dem Server.
## <a name="syntax"></a>Syntax
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
|/remInst:"<Full path>"|Gibt den vollständigen Pfad und Namen der Ordner "RemoteInstall". Wenn der angegebene Ordner nicht bereits vorhanden ist, wird diese Option erstellt, wenn der Befehl ausgeführt wird. Sie sollten immer einen lokalen Pfad, sogar im Fall von einem Remotecomputer eingeben. Zum Beispiel: **D:\remoteInstall**.|
|[/ Authorize]|Autorisiert den Server in das Dynamic Host Control Protocol (DHCP). Diese Option muss nur dann, wenn DHCP-Rogue-Erkennung aktiviert ist, was bedeutet, dass der Windows Deployment Services PXE Server in DHCP zugelassen werden, bevor Clientcomputer bearbeitet werden können. Beachten Sie, dass DHCP-Rogue-Erkennung ist standardmäßig deaktiviert.|
## <a name="BKMK_examples"></a>Beispiele für
Initialisieren Sie den Server aus, und legen Sie die freigegebenen Ordner "RemoteInstall" auf das Laufwerk F:, geben Sie ein.
```
wdsutil /Initialize-Server /remInst:"F:\remoteInstall"
```
Initialisieren Sie den Server aus, und legen Sie freigegebene Ordner "RemoteInstall" auf dem Laufwerk "c:", geben Sie ein.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:"C:\remoteInstall"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Disable-Server-Befehl](using-the-disable-server-command.md)
[mit dem Enable-Server-Befehl](using-the-enable-server-command.md)
[mithilfe der Get-Server-Befehl](using-the-get-server-command.md)
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: Stop-Server](subcommand-stop-server.md)
[die Uninitialize-Server-Option](the-uninitialize-server-option.md)
