---
title: ksetup domain
description: Referenz Artikel für den Ksetup-Domänen Befehl, mit dem der Domänen Name für alle Kerberos-Vorgänge festgelegt wird.
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81135ed668da901c55e891cec4c8749687359818
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887930"
---
# <a name="ksetup-domain"></a>ksetup domain

Legt den Domänen Namen für alle Kerberos-Vorgänge fest.

## <a name="syntax"></a>Syntax

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<domainname>` | Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. contoso.com oder Configuration Manager.|

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Verbindung mit einer gültigen Domäne (z. b. Microsoft) mit dem `ksetup /mapuser` Unterbefehl herzustellen:

```
ksetup /mapuser principal@realm domain-user /domain domain-name
```

Nach einer erfolgreichen Verbindung erhalten Sie ein neues TGT, oder ein vorhandenes TGT wird aktualisiert.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup mapuser-Befehl](ksetup-mapuser.md)