---
title: WDSUTIL Uninitialize-Server
description: Referenz Artikel für "Uninitialize-Server", mit dem die Änderungen auf dem Server während der anfänglichen Server Konfiguration wieder hergestellt werden.
ms.topic: reference
ms.assetid: 015efb04-fe84-469f-bd81-49d0046296b2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4f8f7623c31f355ece5df389af474001d996e755
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730107"
---
# <a name="wdsutil-uninitialize-server"></a>WDSUTIL Uninitialize-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kehrt die Änderungen zurück, die während der anfänglichen Serverkonfiguration auf dem Server vorgenommen wurden. Dies schließt Änderungen ein, die entweder von der **/Initialize-Server** -Option oder dem MMC-Snap-in Windows-Bereitstellungs Dienste vorgenommen werden. Beachten Sie, dass mit diesem Befehl der Server in einen nicht konfigurierten Zustand zurückgesetzt wird. Mit diesem Befehl wird der Inhalt des freigegebenen Ordners RemoteInstall nicht geändert. Stattdessen wird der Zustand des Servers zurückgesetzt, sodass Sie den Server erneut initialisieren können.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Uninitialize-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um den Server erneut zu initialisieren:
```
wdsutil /Uninitialize-Server
wdsutil /verbose /Uninitialize-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)
- [Befehl "WDSUTIL Enable-Server"](wdsutil-enable-server.md)
- [WDSUTIL-Befehl "Get-Server"](wdsutil-get-server.md)
- [Befehl "WDSUTIL Initialize-Server"](wdsutil-initialize-server.md)
- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)
- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)
- [WDSUTIL-Befehl zum Abbrechen von Servern](wdsutil-stop-server.md)
