---
title: nslookup set domain
description: Referenz Artikel für den Befehl nslookup Set Domain, der den Domain Name System Standard-DNS-Domänen Namen (DNS) in den angegebenen Namen ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eaa12029beab301f955a4c9bed4595831f6ebf12
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934410"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard-DNS-Domänen Namen (Domain Name System) in den angegebenen Namen.

## <a name="syntax"></a>Syntax

```
set domain=<domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<domainname>` | Gibt einen neuen Namen für den Standard-DNS-Domänen Namen an. Der Standardwert ist der Name des Hosts. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der Standard-DNS-Domänen Name wird an eine Such Anforderung angehängt, abhängig vom Status der Optionen " **defname** " und " **Search** ".

- Die DNS-Domänen Suchliste enthält die übergeordneten Elemente der DNS-Standard Domäne, wenn Ihr Name aus mindestens zwei Komponenten besteht. Wenn die DNS-Standard Domäne z. b. MFG.widgets.com lautet, heißt die Suchliste sowohl MFG.widgets.com als auch Widgets.com.

- Verwenden Sie den Befehl [nslookup set srchlist](nslookup-set-srchlist.md) , um eine andere Liste anzugeben, und den Befehl [nslookup alle festlegen](nslookup-set-all.md) , um die Liste anzuzeigen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
