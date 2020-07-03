---
title: ksetup domain
description: Referenz Artikel für den Ksetup-Domänen Befehl, mit dem der Domänen Name für alle Kerberos-Vorgänge festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70454205f73375b11dc63e3496a2d7fc1bb3e50e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926105"
---
# <a name="ksetup-domain"></a>ksetup domain

Legt den Domänen Namen für alle Kerberos-Vorgänge fest.

## <a name="syntax"></a>Syntax

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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