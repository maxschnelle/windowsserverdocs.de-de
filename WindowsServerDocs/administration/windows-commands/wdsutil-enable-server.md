---
title: WDSUTIL Enable-Server
description: Referenz Artikel für WDSUTIL Enable-Server, mit dem alle Dienste für die Windows-Bereitstellungs Dienste aktiviert werden.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3ec32f2bd0d269795e1f88b967804c2bb82ac9f4
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730353"
---
# <a name="wdsutil-enable-server"></a>WDSUTIL Enable-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für die Windows-Bereitstellungs Dienste.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Enable-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Führen Sie einen der folgenden Schritte aus, um die Dienste auf dem Server zu aktivieren:
```
wdsutil /Enable-Server
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [WDSUTIL-Befehl](wdsutil-disable-server.md) 
 zum Deaktivieren des Servers [WDSUTIL-Befehl](wdsutil-get-server.md) 
 "Get-Server" Befehl "WDSUTIL [Initialize-Server](wdsutil-initialize-server.md) 
 " [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md) 
 [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md) 
 [WDSUTIL-Befehl](wdsutil-stop-server.md) 
 zum Abbrechen von Servern [WDSUTIL-Befehl "Uninitialize-Server](wdsutil-uninitialize-server.md) "
