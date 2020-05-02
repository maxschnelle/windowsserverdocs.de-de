---
title: nslookup set root
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d913669fd4fede06c9983756df1bbf626ca430ac
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723571"
---
# <a name="nslookup-set-root"></a>nslookup set root

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird.
## <a name="syntax"></a>Syntax
```
set root=<RootServer>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                   BESCHREIBUNG                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Gibt den neuen Namen für den Stamm Server an. Der Standardwert ist NS.nic.DDN.mil. |
| {Help &#124;?} |              Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.               |

## <a name="remarks"></a>Bemerkungen
- Der untergeordnete Stamm Befehl **festlegen** wirkt sich auf den **root** -Unterbefehl aus.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup](nslookup-root.md) -Stamm
