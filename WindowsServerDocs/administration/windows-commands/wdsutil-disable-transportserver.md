---
title: WDSUTIL deaktivieren-Transportserver
description: Referenz Artikel für den Befehl "WDSUTIL deaktivieren-Transportserver", der alle Dienste für einen Transport Server deaktiviert.
ms.topic: reference
ms.assetid: a009706b-8e89-486b-8e3d-512cd9f4de74
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4bbb177897e3a779de275957949b0dcf62e53478
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070352"
---
# <a name="wdsutil-disable-transportserver"></a>WDSUTIL deaktivieren-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Deaktiviert alle Dienste für einen Transport Server.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Disable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Parameter

|Parameter|Description|
|-------|--------|
|[/Server:`<Servername>`]|Gibt den Namen des zu deaktivierenden Transport Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Transport Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Um den Server zu deaktivieren, geben Sie Folgendes ein:

```
wdsutil /Disable-TransportServer
```

```
wdsutil /verbose /Disable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "WDSUTIL Enable-Transportserver"](wdsutil-enable-transportserver.md)

- [Befehl "WDSUTIL Get-TransportServer"](wdsutil-get-transportserver.md)

- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)

- [WDSUTIL Start-TransportServer-Befehl](wdsutil-start-transportserver.md)

- [WDSUTIL-Befehl zum Abbrechen von Transportserver](wdsutil-stop-transportserver.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
