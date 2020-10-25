---
title: WDSUTIL Initialize-Server
description: Referenz Artikel zu "WDSUTIL Initialize-Server", mit dem ein Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung nach der Installation der Server Rolle konfiguriert wird.
ms.topic: reference
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c61da4f608e825a7cb19c8fb80f8f4b3a5c26fed
ms.sourcegitcommit: 554d274fea48a4d47c19845d969a9ec93dec82de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524275"
---
# <a name="wdsutil-initialize-server"></a>WDSUTIL Initialize-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert einen Windows-Bereitstellungsdiensteserver für die erstmalige Verwendung, nachdem die Server Rolle installiert wurde. Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie den [Befehl WDSUTIL Add-Image](wdsutil-add-image.md) verwenden, um dem Server Images hinzuzufügen.
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
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)
- [Befehl "WDSUTIL Enable-Server"](wdsutil-enable-server.md)
- [WDSUTIL-Befehl "Get-Server"](wdsutil-get-server.md)
- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)
- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)
- [WDSUTIL-Befehl zum Abbrechen von Servern](wdsutil-stop-server.md)
- [WDSUTIL-Befehl "Uninitialize-Server"](wdsutil-uninitialize-server.md)
