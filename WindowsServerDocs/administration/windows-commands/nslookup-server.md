---
title: nslookup server
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9a3f4c7bdbcf8122bb532fafe83b400400d8d6b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723686"
---
# <a name="nslookup-server"></a>nslookup server

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
server <DNSDomain>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                          BESCHREIBUNG                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | Erforderlich. Gibt die neue DNS-Domäne für den Standard Server an. |
| {Help &#124;?} |     Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.      |

## <a name="remarks"></a>Bemerkungen
- Der **Server** Befehl verwendet den aktuellen Standard Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **lserver** -Befehl, der den ursprünglichen Server verwendet.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
