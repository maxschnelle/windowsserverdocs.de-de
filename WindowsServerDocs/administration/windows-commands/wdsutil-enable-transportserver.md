---
title: WDSUTIL Enable-Transportserver
description: Referenz Artikel für den Befehl "WDSUTIL Enable-Transportserver", mit dem alle Dienste für den Transport Server aktiviert werden.
ms.topic: reference
ms.assetid: 9d79dba1-4b57-4a00-8cba-877e6b8618e6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b698a9fae2d730a78497fffe52dc91a68175f0f3
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070302"
---
# <a name="wdsutil-enable-transportserver"></a>WDSUTIL Enable-Transportserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für den Transport-Server.

## <a name="syntax"></a>Syntax

```
wdsutil [options] /Enable-TransportServer [/Server:<Servername>]
```

### <a name="parameters"></a>Parameter

| Parameter | Description |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |

## <a name="examples"></a>Beispiele

Um die Dienste auf dem Server zu aktivieren, geben Sie Folgendes ein:

```
wdsutil /Enable-TransportServer
```

```
wdsutil /verbose /Enable-TransportServer /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "WDSUTIL deaktivieren-Transportserver"](wdsutil-disable-transportserver.md)

- [Befehl "WDSUTIL Get-TransportServer"](wdsutil-get-transportserver.md)

- [WDSUTIL Set-TransportServer-Befehl](wdsutil-set-transportserver.md)

- [WDSUTIL Start-TransportServer-Befehl](wdsutil-start-transportserver.md)

- [WDSUTIL-Befehl zum Abbrechen von Transportserver](wdsutil-stop-transportserver.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
