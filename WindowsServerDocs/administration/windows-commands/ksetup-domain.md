---
title: ksetup:domain
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1f53e807891b434709b1a8faed7aae8e8d444f6e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857451"
---
# <a name="ksetupdomain"></a>ksetup:domain



Legt fest, den Domänennamen für alle Kerberos-Vorgänge. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /domain <DomainName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DomainName>|Der Name der Domäne, die zum Herstellen einer Verbindung werden soll. Verwenden Sie den vollqualifizierten Domänennamen oder ein einfaches Formular mit dem Namen, z. B. "contoso.com" "oder" Contoso.|

## <a name="remarks"></a>Hinweise

Keine

## <a name="BKMK_Examples"></a>Beispiele für

Herstellen einer Verbindungs mit der eine gültige Domäne an, wie z. B. Microsoft, mit dem Unterbefehl /mapuser:
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
Wenn die Verbindung erfolgreich ist, erhalten Sie eine neue TGT oder eine vorhandene TGT aktualisiert werden.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)