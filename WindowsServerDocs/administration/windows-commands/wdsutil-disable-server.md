---
title: WDSUTIL deaktivieren-Server
description: Referenz Artikel für den Befehl "WDSUTIL deaktivieren-Server", mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver deaktiviert werden.
ms.topic: reference
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d8af0a0c929e2bff341b2b5bff71d0838b09d418
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070392"
---
# <a name="wdsutil-disable-server"></a>WDSUTIL deaktivieren-Server

Deaktiviert alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax

```
wdsutil [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

| Parameter | Description |
|--|--|
| [/Server:`<Servername>`] | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |

## <a name="examples"></a>Beispiele

Um den Server zu deaktivieren, geben Sie Folgendes ein:

```
wdsutil /Disable-Server
```

```
wdsutil /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Cmdlets für die Windows-Bereitstellungs Dienste](/powershell/module/wds)
