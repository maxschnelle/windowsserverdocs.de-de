---
title: Deaktivieren Sie-Server.
description: Referenz Thema zu "deaktivieren-Server", mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver deaktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5df5c7e2f18cdda2aeeea22c209881077c681f03
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720973"
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
|[/Server:\<Server Name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a>Beispiele

Führen Sie einen der folgenden Schritte aus, um den Server zu deaktivieren:
```
WDSUTIL /Disable-Server
WDSUTIL /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

