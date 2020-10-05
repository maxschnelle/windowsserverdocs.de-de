---
title: WDSUTIL Start-Server
description: Referenz Artikel für den Unterbefehl Start-Server, mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver gestartet werden.
ms.topic: reference
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 03791bd3a313f1ab2a5a2e076036d0aaddb18a8e
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730589"
---
# <a name="wdsutil-start-server"></a>WDSUTIL Start-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an, der gestartet werden soll. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Um den Server zu starten, geben Sie eine der folgenden Informationen ein:
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)
- [Befehl "WDSUTIL Enable-Server"](wdsutil-enable-server.md)
- [WDSUTIL-Befehl "Get-Server"](wdsutil-get-server.md)
- [Befehl "WDSUTIL Initialize-Server"](wdsutil-initialize-server.md)
- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)
- [WDSUTIL-Befehl zum Abbrechen von Servern](wdsutil-stop-server.md)
- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)
- [WDSUTIL-Befehl "Uninitialize-Server"](wdsutil-uninitialize-server.md)
