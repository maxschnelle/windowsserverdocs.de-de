---
title: Verwenden des Befehls "Initialize-Server"
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b9e95972838fc70ee1e617d1e299c9e35db5b979
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392094"
---
# <a name="using-the-initialize-server-command"></a>Verwenden des Befehls "Initialize-Server"

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert einen Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung, nachdem die Server Rolle installiert wurde. Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie [mithilfe des Befehls Befehls Add-Image](using-the-add-image-command.md) dem Server Images hinzufügen.
## <a name="syntax"></a>Syntax
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/remInst: "<Full path>"|Gibt den vollständigen Pfad und den Namen des Ordners "RemoteInstall" an. Wenn der angegebene Ordner nicht bereits vorhanden ist, wird er durch diese Option erstellt, wenn der Befehl ausgeführt wird. Sie sollten immer einen lokalen Pfad eingeben, auch wenn es sich um einen Remote Computer handelt. Zum Beispiel: **D:\RemoteInstall**.|
|/Authorize-Endpunkt|Autorisiert den Server im Dynamic Host Control Protocol (DHCP). Diese Option ist nur erforderlich, wenn die DHCP-nicht autorisierte Erkennung aktiviert ist. Dies bedeutet, dass der PXE-Server der Windows-Bereitstellungs Dienste in DHCP autorisiert werden muss, damit Client Computer gewartet werden können. Beachten Sie, dass die DHCP-nicht autorisierte Erkennung standardmäßig deaktiviert ist.|
## <a name="BKMK_examples"></a>Beispiele
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk F: festzulegen, geben Sie ein.
```
wdsutil /Initialize-Server /remInst:"F:\remoteInstall"
```
Um den Server zu initialisieren und den freigegebenen RemoteInstall-Ordner auf Laufwerk C: festzulegen, geben Sie ein.
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:"C:\remoteInstall"
```
#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mit dem Befehl "deaktivierte Server](using-the-disable-server-command.md)" 
 mit dem Befehl "[enable-](using-the-enable-server-command.md)Server" 
 mithilfe des Befehls "[Get-Server](using-the-get-server-command.md)" 
 Unterbefehl: "[Set-Server](subcommand-set-server.md)
"[Unterbefehl: Start-Server](subcommand-start-server.md)1[Unterbefehl: beenden-Server](subcommand-stop-server.md)3[die Option "nicht initialisieren-Server](the-uninitialize-server-option.md) "
