---
title: nslookup set root
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea2c34bbf7c9323c948d57ac2a838c22aea1008e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838313"
---
# <a name="nslookup-set-root"></a>nslookup set root

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Namen des Stamm Servers, der für Abfragen verwendet wird.
## <a name="syntax"></a>Syntax
```
set root=<RootServer>
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                   Beschreibung                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Gibt den neuen Namen für den Stamm Server an. Der Standardwert ist NS.nic.DDN.mil. |
| {Help &#124; ?} |              Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.               |

## <a name="remarks"></a>Hinweise
- Der untergeordnete Stamm Befehl **festlegen** wirkt sich auf den **root** -Unterbefehl aus.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup](nslookup-root.md) -Stamm
