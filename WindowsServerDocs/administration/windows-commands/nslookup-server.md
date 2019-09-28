---
title: nslookup server
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ce609f62f2d87024e1d75b43869b3b867e946e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373057"
---
# <a name="nslookup-server"></a>nslookup server

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
server <DNSDomain>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                          Beschreibung                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | Erforderlich. Gibt die neue DNS-Domäne für den Standard Server an. |
| {Help &#124; ?} |     Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.      |

## <a name="remarks"></a>Hinweise
- Der **Server** Befehl verwendet den aktuellen Standard Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **lserver** -Befehl, der den ursprünglichen Server verwendet.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
