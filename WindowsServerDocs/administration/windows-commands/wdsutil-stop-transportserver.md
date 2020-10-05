---
title: WDSUTIL-Beendigung-Transportserver
description: Referenz Artikel für "Ende-Transportserver"
ms.topic: reference
ms.assetid: dc1b1eec-6893-445e-81dc-16b3fae287fa
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 800c99cba18ed2158749b1638627b31f8fdbaf5f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730520"
---
# <a name="wdsutil-stop-transportserver"></a>WDSUTIL-Beendigung-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Beendet alle Dienste auf einem Transport Server.
## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Stop-TransportServer [/Server:<Server name>]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Server angegeben ist, wird der lokale Server verwendet.|
## <a name="examples"></a>Beispiele
Geben Sie eine der folgenden Informationen ein, um die Dienste zu unterbinden:
```
wdsutil /Stop-TransportServer
wdsutil /verbose /Stop-TransportServer /Server:MyWDSServer
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL deaktivieren-Transportserver"](wdsutil-disable-transportserver.md)
- [Befehl "WDSUTIL Enable-Transportserver"](wdsutil-enable-transportserver.md)
- [Befehl "WDSUTIL Get-TransportServer"](wdsutil-get-transportserver.md)
- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)
- [WDSUTIL Start-TransportServer-Befehl](wdsutil-start-transportserver.md)
