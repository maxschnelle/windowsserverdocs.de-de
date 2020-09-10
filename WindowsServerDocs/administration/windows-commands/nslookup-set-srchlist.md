---
title: nslookup set srchlist
description: Referenz Artikel für den Befehl nslookup set srchlist, der den Domain Name System Standard-DNS-Domänen Namen und die Suchliste ändert.
ms.topic: reference
ms.assetid: 8486266d-22ac-4ce5-aad6-1cd0c08110a2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0d2798cd97b561ec5da7e515587978a4b19403c0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640531"
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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set domain](nslookup-set-domain.md)

- [nslookup set all](nslookup-set-all.md)
