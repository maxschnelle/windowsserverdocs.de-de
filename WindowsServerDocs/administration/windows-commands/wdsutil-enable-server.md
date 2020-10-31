---
title: WDSUTIL Enable-Server
description: Referenz Artikel für den Befehl "WDSUTIL Enable-Server", mit dem alle Dienste für die Windows-Bereitstellungs Dienste aktiviert werden.
ms.topic: reference
ms.assetid: 939ffbfb-cf3c-4310-9627-6e7e0c0644d6
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2e2f62198ce4c012245174bc00e536e15ecd1c27
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070322"
---
# <a name="wdsutil-enable-server"></a>WDSUTIL Enable-Server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert alle Dienste für die Windows-Bereitstellungs Dienste.

## <a name="syntax"></a>Syntax

```
wdsutil [options] /Enable-Server [/Server:<Servername>]
```

### <a name="parameters"></a>Parameter

| Parameter | Description |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |

## <a name="examples"></a>Beispiele

Um die Dienste auf dem Server zu aktivieren, geben Sie Folgendes ein:

```
wdsutil /Enable-Server
```

```
wdsutil /verbose /Enable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [WDSUTIL-Befehl zum Deaktivieren des Servers](wdsutil-disable-server.md)

- [WDSUTIL-Befehl "Get-Server"](wdsutil-get-server.md)

- [Befehl "WDSUTIL Initialize-Server"](wdsutil-initialize-server.md)

- [WDSUTIL Set-Server-Befehl](wdsutil-set-server.md)

- [WDSUTIL Start-Server-Befehl](wdsutil-start-server.md)

- [WDSUTIL-Befehl zum Abbrechen von Servern](wdsutil-stop-server.md)

- [WDSUTIL-Befehl "Uninitialize-Server"](wdsutil-uninitialize-server.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
