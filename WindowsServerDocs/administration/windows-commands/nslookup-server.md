---
title: nslookup server
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8de2d8a801d57a9197d5e8ec7d3b6adb2d00dd04
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838683"
---
# <a name="nslookup-server"></a>nslookup server

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard Server in die angegebene Domain Name System Domäne (DNS).
## <a name="syntax"></a>Syntax
```
server <DNSDomain>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                          Beschreibung                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | Erforderlich Gibt die neue DNS-Domäne für den Standard Server an. |
| {Help &#124; ?} |     Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.      |

## <a name="remarks"></a>Hinweise
- Der **Server** Befehl verwendet den aktuellen Standard Server, um die Informationen zur angegebenen DNS-Domäne zu suchen. Dies steht im Gegensatz zum **lserver** -Befehl, der den ursprünglichen Server verwendet.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
