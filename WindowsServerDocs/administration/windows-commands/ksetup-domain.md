---
title: 'Ksetup: Domäne'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfaa8a37ae4ee5c9669b09f27a73b3d016324dea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841583"
---
# <a name="ksetupdomain"></a>Ksetup: Domäne



Legt den Domänen Namen für alle Kerberos-Vorgänge fest. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /domain <DomainName>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Domainname >|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. contoso.com oder Configuration Manager.|

## <a name="remarks"></a>Hinweise

None.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Stellen Sie eine Verbindung mit einer gültigen Domäne (z. b. Microsoft) mit dem/mapuser-Unterbefehl her:
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
Wenn die Verbindung erfolgreich ist, wird ein neues TGT angezeigt, oder ein vorhandenes TGT wird aktualisiert.

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)