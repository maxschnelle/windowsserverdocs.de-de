---
title: Initialize-Server
description: Windows-Befehls Thema für "Initialize-Server", mit dem ein Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung nach der Installation der Server Rolle konfiguriert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c80af07827c889a3dd1c5d3050cd2ca3b4c8f1e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830793"
---
# <a name="initialize-server"></a>Initialize-Server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert einen Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung, nachdem die Server Rolle installiert wurde. Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie [mithilfe des Befehls Befehls Add-Image](using-the-add-image-command.md) dem Server Images hinzufügen.
## <a name="syntax"></a>Syntax
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/remInst:<Full path>|Gibt den vollständigen Pfad und den Namen des Ordners "RemoteInstall" an. Wenn der angegebene Ordner nicht bereits vorhanden ist, wird er durch diese Option erstellt, wenn der Befehl ausgeführt wird. Sie sollten immer einen lokalen Pfad eingeben, auch wenn es sich um einen Remote Computer handelt. Beispiel: **d:\RemoteInstall**.|
|/Authorize-Endpunkt|Autorisiert den Server im Dynamic Host Control Protocol (DHCP). Diese Option ist nur erforderlich, wenn die DHCP-nicht autorisierte Erkennung aktiviert ist. Dies bedeutet, dass der PXE-Server der Windows-Bereitstellungs Dienste in DHCP autorisiert werden muss, damit Client Computer gewartet werden können. Beachten Sie, dass die DHCP-nicht autorisierte Erkennung standardmäßig deaktiviert ist.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk F: festzulegen, geben Sie ein.
```
wdsutil /Initialize-Server /remInst:F:\remoteInstall
```
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk C: festzulegen, geben Sie ein.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:C:\remoteInstall
```
## <a name="additional-references"></a>Weitere Verweise
- [Der Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
mithilfe des Befehls "Enable [-Server](using-the-disable-server-command.md) "
mithilfe des Befehls " [enable-](using-the-enable-server-command.md) Server"
[mithilfe des Befehls "Get-Server](using-the-get-server-command.md) "
[Unterbefehl: Set-Server](subcommand-set-server.md)
[Unterbefehl: Start-Server](subcommand-start-server.md)
[Unterbefehl: beenden-Server](subcommand-stop-server.md)
[die Option "Uninitialize-Server](the-uninitialize-server-option.md) "
