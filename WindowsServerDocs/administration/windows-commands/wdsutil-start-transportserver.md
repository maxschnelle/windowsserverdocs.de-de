---
title: WDSUTIL Start-TransportServer
description: Referenz Artikel für den Unterbefehl Start-TransportServer, mit dem alle Dienste für einen Transport Server gestartet werden.
ms.topic: reference
ms.assetid: 0e93bc84-5b9e-4f9d-8cf0-1634417da0f6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 3aa948fb86b1b69448ac131c6894ff0c41f548e8
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730598"
---
# <a name="wdsutil-start-transportserver"></a>WDSUTIL Start-TransportServer

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-TransportServer
wdsutil /verbose /start-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL deaktivieren-Transportserver"](wdsutil-disable-transportserver.md)
- [Befehl "WDSUTIL Enable-Transportserver"](wdsutil-enable-transportserver.md)
- [Befehl "WDSUTIL Get-TransportServer"](wdsutil-get-transportserver.md)
- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)
- [WDSUTIL-Befehl zum Abbrechen von Transportserver](wdsutil-stop-transportserver.md)
