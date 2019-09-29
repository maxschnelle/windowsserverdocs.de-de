---
title: 'Ksetup: Domäne'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4d9f09def32c7518046c25887f4154020c5d7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375117"
---
# <a name="ksetupdomain"></a>Ksetup: Domäne



Legt den Domänen Namen für alle Kerberos-Vorgänge fest. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /domain <DomainName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<domainname >|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Hinweise

Keine

## <a name="BKMK_Examples"></a>Beispiele

Stellen Sie eine Verbindung mit einer gültigen Domäne (z. b. Microsoft) mit dem/mapuser-Unterbefehl her:
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
Wenn die Verbindung erfolgreich ist, wird ein neues TGT angezeigt, oder ein vorhandenes TGT wird aktualisiert.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)