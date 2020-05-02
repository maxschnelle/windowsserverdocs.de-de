---
title: 'Ksetup: Domäne'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f127eaf33e9ef6d597851c31a4167ceaa3516abb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724687"
---
# <a name="ksetupdomain"></a>Ksetup: Domäne



Legt den Domänen Namen für alle Kerberos-Vorgänge fest.

## <a name="syntax"></a>Syntax

```
ksetup /domain <DomainName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Domain Name>|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Bemerkungen

Keine.

## <a name="examples"></a>Beispiele

Stellen Sie eine Verbindung mit einer gültigen Domäne (z. b. Microsoft) mit dem/mapuser-Unterbefehl her:
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
Wenn die Verbindung erfolgreich ist, wird ein neues TGT angezeigt, oder ein vorhandenes TGT wird aktualisiert.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)