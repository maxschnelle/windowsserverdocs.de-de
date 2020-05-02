---
title: nslookup lserver
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2054c0fd427b41e7d6076258b29ab78d0fb7892
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723678"
---
# <a name="nslookup-lserver"></a>nslookup lserver

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
lserver <DNSDomain> 
```
### <a name="parameters"></a>Parameter

|    Parameter    |                      BESCHREIBUNG                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | Gibt die neue DNS-Domäne für den Standard Server an.  |
| {Help &#124;?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Bemerkungen
- Der **lserver** -Befehl verwendet den anfänglichen Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **Server** -Befehl, der den aktuellen Standard Server verwendet.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Server](nslookup-server.md)
