---
title: WDSUTIL deaktivieren-Transportserver
description: Referenz Artikel zu "WDSUTIL deaktivieren-Transportserver", mit dem alle Dienste für einen Transport Server deaktiviert werden.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9d404c8f16e876a15e4b683dd3cceef60804fbdb
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730377"
---
# <a name="wdsutil-disable-transportserver"></a>WDSUTIL deaktivieren-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Disable-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des zu deaktivierenden Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu deaktivieren, geben Sie Folgendes ein:
```
wdsutil /Disable-TransportServer
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL Enable-Transportserver"](wdsutil-enable-transportserver.md)
- [Befehl "WDSUTIL Get-TransportServer"](wdsutil-get-transportserver.md)
- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)
- [WDSUTIL Start-TransportServer-Befehl](wdsutil-start-transportserver.md)
- [WDSUTIL-Befehl zum Abbrechen von Transportserver](wdsutil-stop-transportserver.md)
