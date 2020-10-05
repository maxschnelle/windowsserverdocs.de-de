---
title: WDSUTIL Get-TransportServer
description: Referenz Artikel zu WDSUTIL Get-TransportServer, der Informationen zu einem angegebenen Transport Server anzeigt.
ms.topic: reference
ms.assetid: de634123-0179-41b2-9c6f-726508130ff5
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a0d807035fa60ca757b1b27cc63c4bfce6e92070
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730221"
---
# <a name="wdsutil-get-transportserver"></a>WDSUTIL Get-TransportServer

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem angegebenen Transport Server an.

## <a name="syntax"></a>Syntax
```
wdsutil [Options] /Get-TransportServer [/Server:<Server name>] /Show:{Config}
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Show: {config}|Gibt Konfigurationsinformationen zum angegebenen Transport Server zurück.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zum Server anzuzeigen:
```
wdsutil /Get-TransportServer /Show:Config
```
Geben Sie Folgendes ein, um die Konfigurationsinformationen anzuzeigen:
```
wdsutil /Get-TransportServer /Server:MyWDSServer /Show:Config
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Befehl "WDSUTIL deaktivieren-Transportserver"](wdsutil-disable-transportserver.md)
- [Befehl "WDSUTIL Enable-Transportserver"](wdsutil-enable-transportserver.md)
- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)
- [WDSUTIL Start-TransportServer-Befehl](wdsutil-start-transportserver.md)
- [WDSUTIL-Befehl zum Abbrechen von Transportserver](wdsutil-stop-transportserver.md)
