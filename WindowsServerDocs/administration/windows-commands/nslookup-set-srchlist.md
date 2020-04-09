---
title: nslookup set srchlist
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbeb09501474ade670147a6021abd2bb25291d71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838283"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Domain Name System Standard-DNS-Domänen Namen und die Suchliste.

## <a name="syntax"></a>Syntax
```
Set srchlist=<DomainName>[/...]
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                        Beschreibung                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | Gibt neue Namen für die DNS-Standard Domäne und-Suchliste an. Der Standardwert für den Domänen Namen basiert auf dem Hostnamen. Sie können maximal sechs Namen angeben, die durch Schrägstriche (/) getrennt sind. |
| {Help &#124; ?} |                                                                   Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                   |

## <a name="remarks"></a>Hinweise
- Der Befehl **set srchlist**überschreibt den Standard-DNS-Domänen Namen und die Suchliste des Befehls **Set Domain** . Verwenden Sie den Befehl **alle festlegen** , um die Liste anzuzeigen.
  ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
  Im folgenden Beispiel wird die DNS-Domäne auf MFG.widgets.com und die Suchliste auf die drei Namen festgelegt:
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Domäne festlegen](nslookup-set-domain.md)
  [nslookup alle festlegen](nslookup-set-all.md)
