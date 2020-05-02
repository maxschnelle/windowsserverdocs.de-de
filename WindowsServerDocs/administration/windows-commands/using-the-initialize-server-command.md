---
title: Initialize-Server
description: Referenz Thema für Initialize-Server, mit dem ein Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung nach der Installation der Server Rolle konfiguriert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54180923a077c0b423e73588bcbd1c03b0154d08
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719720"
---
# <a name="initialize-server"></a>Initialize-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert einen Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung, nachdem die Server Rolle installiert wurde. Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie [mithilfe des Befehls Befehls Add-Image](using-the-add-image-command.md) dem Server Images hinzufügen.
## <a name="syntax"></a>Syntax
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|remInst<Full path>|Gibt den vollständigen Pfad und den Namen des Ordners "RemoteInstall" an. Wenn der angegebene Ordner nicht bereits vorhanden ist, wird er durch diese Option erstellt, wenn der Befehl ausgeführt wird. Sie sollten immer einen lokalen Pfad eingeben, auch wenn es sich um einen Remote Computer handelt. Beispiel: **d:\RemoteInstall**.|
|/Authorize-Endpunkt|Autorisiert den Server im Dynamic Host Control Protocol (DHCP). Diese Option ist nur erforderlich, wenn die DHCP-nicht autorisierte Erkennung aktiviert ist. Dies bedeutet, dass der PXE-Server der Windows-Bereitstellungs Dienste in DHCP autorisiert werden muss, damit Client Computer gewartet werden können. Beachten Sie, dass die DHCP-nicht autorisierte Erkennung standardmäßig deaktiviert ist.|
## <a name="examples"></a>Beispiele
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk F: festzulegen, geben Sie ein.
```
wdsutil /Initialize-Server /remInst:F:\remoteInstall
```
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk C: festzulegen, geben Sie ein.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:C:\remoteInstall
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des](using-the-disable-server-command.md)
Befehls "Enable-Server" mit dem Befehl "[Enable-Server](using-the-enable-server-command.md)
" mit dem Befehl "[Get-Server Command](using-the-get-server-command.md)
[unter Command: Set-Server](subcommand-set-server.md)
[subcommand: Start-Server](subcommand-start-server.md)
[unter Command: beenden-Server](subcommand-stop-server.md)
[The Uninitialize-Server](the-uninitialize-server-option.md) "
