---
title: WDSUTIL-Beendigung-Server
description: Referenz Artikel für den Unterbefehl "Stopp-Server", der alle Dienste auf einem Windows-Bereitstellungsdiensteserver stoppt.
ms.topic: reference
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0c1288900cdc5eaa46c27b6eb05fd64b9a1b16a4
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730119"
---
# <a name="wdsutil-stop-server"></a>WDSUTIL-Beendigung-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)
- [Befehl "WDSUTIL Enable-Server"](wdsutil-enable-server.md)
- [WDSUTIL-Befehl "Get-Server"](wdsutil-get-server.md)
- [Befehl "WDSUTIL Initialize-Server"](wdsutil-initialize-server.md)
- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)
- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)
- [WDSUTIL-Befehl "Uninitialize-Server"](wdsutil-uninitialize-server.md)

