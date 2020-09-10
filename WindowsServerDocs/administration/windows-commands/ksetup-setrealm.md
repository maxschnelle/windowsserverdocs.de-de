---
title: ksetup setrealm
description: Referenz Artikel für den Ksetup setrealm-Befehl, mit dem der Name eines Kerberos-Bereichs festgelegt wird.
ms.topic: reference
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a06c5fef1127236319b580fbd6810269c58d1377
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627137"
---
# <a name="ksetup-setrealm"></a>ksetup setrealm

Legt den Namen eines Kerberos-Bereichs fest.

> [!IMPORTANT]
> Das Festlegen des Kerberos-Bereichs auf einem Domänen Controller wird nicht unterstützt. Der Versuch, dies zu tun, verursacht eine Warnung und einen Befehls Fehler.

## <a name="syntax"></a>Syntax

```
ksetup /setrealm <DNSdomainname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<DNSdomainname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. Sie können den voll qualifizierten Domänen Namen oder eine einfache Form des Namens verwenden. Wenn Sie den DNS-Namen nicht in Großbuchstaben verwenden, werden Sie zur Überprüfung aufgefordert, um den Vorgang fortzusetzen. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Bereich dieses Computers auf einen bestimmten Domänen Namen festzulegen und den Zugriff durch einen nicht-Domänen Controller direkt auf den Bereich von "Configuration Manager" (Kerberos) zu beschränken:

```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [ksetup removerealm](ksetup-removerealm.md)
