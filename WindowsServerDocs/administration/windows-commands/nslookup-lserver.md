---
title: nslookup lserver
description: 'Windows-Befehle Thema ***- '
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
ms.openlocfilehash: 2f2f787915f2b941d6c098d44de1bb0e04dbd491
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436914"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Standardserver an der angegebenen Domäne von Domain Name System (DNS).
## <a name="syntax"></a>Syntax
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>Parameter

|    Parameter    |                      Beschreibung                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | Gibt die neue DNS-Domäne für den Standardserver an.  |
| {help &#124; ?} | Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle. |

## <a name="remarks"></a>Hinweise
- Die **Lserver** Befehl verwendet den ersten Server, um die Informationen über die angegebenen DNS-Domäne zu suchen. Dies ist im Gegensatz zu den **Server** -Befehl, der den aktuellen Standardservers verwendet.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Nslookup-Server](nslookup-server.md)
