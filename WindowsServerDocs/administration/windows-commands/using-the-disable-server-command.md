---
title: Deaktivieren Sie-Server.
description: Referenz Artikel zu "deaktivieren-Server", mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver deaktiviert werden.
ms.topic: reference
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ed8fafb9c35f54656ab4551876dc0461ea1a2c55
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89622038"
---
# <a name="disable-server"></a>Deaktivieren Sie-Server.

Deaktiviert alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|[/Server:\<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Führen Sie einen der folgenden Schritte aus, um den Server zu deaktivieren:
```
WDSUTIL /Disable-Server
WDSUTIL /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

