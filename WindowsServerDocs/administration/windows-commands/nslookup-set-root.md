---
title: nslookup set root
description: 'Windows-Befehls Thema für * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a1737275bf6321525bbba56cd4d6a77ef973423
ms.sourcegitcommit: 9a6a692a7b2a93f52bb9e2de549753e81d758d28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591028"
---
# <a name="nslookup-set-root"></a>nslookup set root

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird.
## <a name="syntax"></a>Syntax
```
set root=<RootServer>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                   Beschreibung                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Gibt den neuen Namen für den Stamm Server an. Der Standardwert ist NS.nic.DDN.mil. |
| {Help &#124; ?} |              Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.               |

## <a name="remarks"></a>Hinweise
- Der untergeordnete Stamm Befehl **festlegen** wirkt sich auf den **root** -Unterbefehl aus.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
  [nslookup](nslookup-root.md) -Stamm
