---
title: ksetup domain
description: Referenz Artikel für den Ksetup-Domänen Befehl, mit dem der Domänen Name für alle Kerberos-Vorgänge festgelegt wird.
ms.topic: reference
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dcb7624f7b9fa81c66fed4533a0ba377095fa902
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640047"
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