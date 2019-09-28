---
title: 'Ksetup: setrealm'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bbe5c000b7e84066c19511639fe3d92d7e4b558
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374899"
---
# <a name="ksetupsetrealm"></a>Ksetup: setrealm



Legt den Namen eines Kerberos-Bereichs fest. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setrealm <DNSDomainName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<dnsdomainname >|Der DNS-Domänen Name kann in Form eines voll qualifizierten Domänen Namens oder eines einfachen Domänen namens vorliegen.|

## <a name="remarks"></a>Hinweise

Der DNS-Domänen Namen Parameter sollte in Großbuchstaben eingegeben werden. Andernfalls fordert der **Ksetup** -Befehl eine Überprüfung an, um den Vorgang fortzusetzen.

Das Festlegen des Kerberos-Bereichs auf einem Domänen Controller wird nicht unterstützt. Wenn Sie versuchen, dies zu tun, wird eine Warnung und ein Befehls Fehler verursacht.

## <a name="BKMK_Examples"></a>Beispiele

Legen Sie den Bereich für diesen Computer auf einen bestimmten Domänen Namen fest, um den Zugriff durch einen nicht-Domänen Controller direkt auf den Bereich "Domäne" von "Configuration Manager" zu beschränken:
```
ksetup /setrealm CONTOSO
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)