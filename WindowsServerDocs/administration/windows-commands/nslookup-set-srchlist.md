---
title: nslookup set srchlist
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39b28e7d43df2427caae46d323cd30f03b6b484c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436573"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Standard Domain Name System (DNS) Domäne Name "und" suchen.

## <a name="syntax"></a>Syntax
```
Set srchlist=<DomainName>[/...]
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                                                                        Beschreibung                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <DomainName>   | Gibt neue Namen für die Standard-DNS-Domäne, und suchen. Der Name der domänenstandardwert basiert auf den Namen des Hosts. Sie können maximal sechs Namen, die durch Schrägstriche (/) getrennt angeben. |
| {help &#124; ?} |                                                                   Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.                                                                   |

## <a name="remarks"></a>Hinweise
- Die **Srchlist festgelegt**Befehl überschreibt der standardmäßigen DNS-Namen, und suchen Sie Domänenliste der **Satz Domäne** Befehl. Verwenden der **alle festlegen** Befehl aus, um die Liste anzuzeigen.
  ## <a name="BKMK_examples"></a>Beispiele für
  Im folgenden Beispiel wird die DNS-Domäne mfg.widgets.com und der Liste "Suchen" auf die drei Namen:
  ```
  set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
  ```
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Domäne fest, Nslookup](nslookup-set-domain.md)
  [Nslookup alle festlegen](nslookup-set-all.md)
