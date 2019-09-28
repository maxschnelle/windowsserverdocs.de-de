---
title: nslookup set root
description: 'Windows-Befehle Thema ****- '
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
ms.openlocfilehash: 08cf41ec9b6ac30699013112216a538dcf625fd5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372838"
---
# <a name="nslookup-set-root"></a>nslookup set root

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
