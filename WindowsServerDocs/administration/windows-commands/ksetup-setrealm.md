---
title: ksetup setrealm
description: Referenz Artikel für den Ksetup setrealm-Befehl, mit dem der Name eines Kerberos-Bereichs festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c6fa5573322237dfee5909d9afc2e99696ac82b3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933137"
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

| Parameter | Beschreibung |
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
