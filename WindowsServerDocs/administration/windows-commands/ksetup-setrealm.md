---
title: Ksetup setrealm
description: Referenz Thema für den Ksetup setrealm-Befehl, mit dem der Name eines Kerberos-Bereichs festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03b33977f57e187a8bea69be78c1e9c094b9a73e
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817280"
---
# <a name="ksetup-setrealm"></a>Ksetup setrealm

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup removerealm](ksetup-removerealm.md)
