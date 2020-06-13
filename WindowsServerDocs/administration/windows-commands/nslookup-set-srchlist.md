---
title: nslookup set srchlist
description: Referenz Thema für den Befehl "nslookup set srchlist", mit dem der DNS-Domain Name System Standard Domänen Name und die Suchliste geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed9bbce1910324c4cae5da4228a6d3d1f269d050
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721400"
---
# <a name="nslookup-set-srchlist"></a>nslookup set srchlist

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Domain Name System Standard-DNS-Domänen Namen und die Suchliste. Dieser Befehl überschreibt den Standard-DNS-Domänen Namen und die Suchliste des Befehls [nslookup Set Domain](nslookup-set-domain.md) .

## <a name="syntax"></a>Syntax

```
set srchlist=<domainname>[/...]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<domainname>` | Gibt neue Namen für die DNS-Standard Domäne und-Suchliste an. Der Standardwert für den Domänen Namen basiert auf dem Hostnamen. Sie können maximal sechs Namen angeben, die durch Schrägstriche (/) getrennt sind. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Verwenden Sie den Befehl [nslookup alle festlegen](nslookup-set-all.md) , um die Liste anzuzeigen.

### <a name="examples"></a>Beispiele

So legen Sie die DNS-Domäne auf *MFG.widgets.com* und die Suchliste auf die drei Namen fest:

```
set srchlist=mfg.widgets.com/mrp2.widgets.com/widgets.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set domain](nslookup-set-domain.md)

- [nslookup set all](nslookup-set-all.md)
