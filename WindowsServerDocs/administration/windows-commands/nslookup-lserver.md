---
title: nslookup lserver
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d0d8619101d2e7b1f7fb6d6ed99d801c7c264f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838633"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
lserver <DNSDomain> 
```
### <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | Gibt die neue DNS-Domäne für den Standard Server an.  |
| {Help &#124; ?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Hinweise
- Der **lserver** -Befehl verwendet den anfänglichen Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **Server** -Befehl, der den aktuellen Standard Server verwendet.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Server](nslookup-server.md)
