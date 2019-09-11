---
title: nslookup lserver
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30c5ba8b7fef9b09d854aca998948f7891d99a02
ms.sourcegitcommit: ee8e0b217be6f6b2532ee7265fb4be00c106e124
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70878128"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | Gibt die neue DNS-Domäne für den Standard Server an.  |
| {Help &#124; ?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Hinweise
- Der **lserver** -Befehl verwendet den anfänglichen Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **Server** -Befehl, der den aktuellen Standard Server verwendet.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Server](nslookup-server.md)
