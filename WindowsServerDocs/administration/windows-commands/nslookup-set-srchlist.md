---
title: nslookup set srchlist
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8936daa3505b02295ae2f09c2910dead8d4c0ff8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723551"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Domain Name System Standard-DNS-Domänen Namen und die Suchliste.

## <a name="syntax"></a>Syntax
```
Set srchlist=<DomainName>[/...]
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                        BESCHREIBUNG                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | Gibt neue Namen für die DNS-Standard Domäne und-Suchliste an. Der Standardwert für den Domänen Namen basiert auf dem Hostnamen. Sie können maximal sechs Namen angeben, die durch Schrägstriche (/) getrennt sind. |
| {Help &#124;?} |                                                                   Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                   |

## <a name="remarks"></a>Bemerkungen
- Der Befehl **set srchlist**überschreibt den Standard-DNS-Domänen Namen und die Suchliste des Befehls **Set Domain** . Verwenden Sie den Befehl **alle festlegen** , um die Liste anzuzeigen.
  ## <a name="examples"></a>Beispiele
  So legen Sie die DNS-Domäne auf MFG.widgets.com und die Suchliste auf die drei Namen fest:
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup legen Sie Domäne](nslookup-set-domain.md)
  [nslookup alle festlegen fest](nslookup-set-all.md) .
