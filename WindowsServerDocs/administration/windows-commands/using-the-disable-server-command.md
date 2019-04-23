---
title: Mithilfe der deaktivieren-Server-Befehl
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b229146206c1fbe6ce8b6f585b2ff9b50ae6104
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853031"
---
# <a name="using-the-disable-server-command"></a>Mithilfe der deaktivieren-Server-Befehl



Deaktiviert alle Dienste für einen Windows-Bereitstellungsdienste-Server an.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Disable-Server [/Server:<Server name>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[/ Server:\<Servername >]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|

## <a name="BKMK_examples"></a>Beispiele für

Führen Sie einen der folgenden Schritte aus, um den Server zu deaktivieren:
```
WDSUTIL /Disable-Server
WDSUTIL /Verbose /Disable-Server /Server:MyWDSServer
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

