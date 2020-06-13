---
title: nslookup set domain
description: Referenz Thema für den Befehl "nslookup-Domäne", der den Domain Name System Standard-DNS-Domänen Namen (DNS) in den angegebenen Namen ändert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e672bf53e655ef12cadb2a30aaa377b24e49afec
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721633"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert den Standard-DNS-Domänen Namen (Domain Name System) in den angegebenen Namen.

## <a name="syntax"></a>Syntax

```
set domain=<domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<domainname>` | Gibt einen neuen Namen für den Standard-DNS-Domänen Namen an. Der Standardwert ist der Name des Hosts. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Der Standard-DNS-Domänen Name wird an eine Such Anforderung angehängt, abhängig vom Status der Optionen " **defname** " und " **Search** ".

- Die DNS-Domänen Suchliste enthält die übergeordneten Elemente der DNS-Standard Domäne, wenn Ihr Name aus mindestens zwei Komponenten besteht. Wenn die DNS-Standard Domäne z. b. MFG.widgets.com lautet, heißt die Suchliste sowohl MFG.widgets.com als auch Widgets.com.

- Verwenden Sie den Befehl [nslookup set srchlist](nslookup-set-srchlist.md) , um eine andere Liste anzugeben, und den Befehl [nslookup alle festlegen](nslookup-set-all.md) , um die Liste anzuzeigen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
