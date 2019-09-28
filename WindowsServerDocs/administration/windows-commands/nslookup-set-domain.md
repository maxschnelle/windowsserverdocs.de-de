---
title: nslookup set domain
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f140a371a6374baa7921ca823df469156593423c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372929"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Standard-DNS-Domänen Namen (Domain Name System) in den angegebenen Namen.
## <a name="syntax"></a>Syntax
```
set domain=<DomainName>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                           Beschreibung                                           |
|-----------------|-------------------------------------------------------------------------------------------------|
|  <DomainName>   | Gibt einen neuen Namen für den Standard-DNS-Domänen Namen an. Der Standard Domänen Name ist der Hostname. |
| {Help &#124; ?} |                      Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                      |

## <a name="remarks"></a>Hinweise
- Der Standard-DNS-Domänen Name wird an eine Such Anforderung angehängt, abhängig vom Status der Optionen " **defname** " und " **Search** ". Die DNS-Domänen Suchliste enthält die übergeordneten Elemente der DNS-Standard Domäne, wenn Ihr Name aus mindestens zwei Komponenten besteht. Wenn die DNS-Standard Domäne z. b. MFG.widgets.com lautet, heißt die Suchliste sowohl MFG.widgets.com als auch Widgets.com. Verwenden Sie den Befehl **set srchlist** , um eine andere Liste anzugeben, und den Befehl **alle festlegen** , um die Liste anzuzeigen.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup set srchlist](nslookup-set-srchlist.md)
  [nslookup alle festlegen](nslookup-set-all.md)
