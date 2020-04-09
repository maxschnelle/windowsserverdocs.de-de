---
title: Deaktivieren Sie-Server.
description: Windows-Befehls Thema für "deaktivieren-Server", mit dem alle Dienste für einen Windows-Bereitstellungsdiensteserver deaktiviert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba8c42f8b951baa4679adc44c69bf28cb2af2629
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831633"
---
# <a name="disable-server"></a>Deaktivieren Sie-Server.

Deaktiviert alle Dienste für einen Windows-Bereitstellungsdiensteserver.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/Server:\<Server Name >]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Führen Sie einen der folgenden Schritte aus, um den Server zu deaktivieren:
```
WDSUTIL /Disable-Server
WDSUTIL /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

