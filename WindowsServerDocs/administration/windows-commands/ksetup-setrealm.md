---
title: 'Ksetup: setrealm'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 453977ac39dd3a52b4f5a3104995f944e4a48392
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724556"
---
# <a name="ksetupsetrealm"></a>Ksetup: setrealm



Legt den Namen eines Kerberos-Bereichs fest.

## <a name="syntax"></a>Syntax

```
ksetup /setrealm <DNSDomainName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<DNSDomainName->|Der DNS-Domänen Name kann in Form eines voll qualifizierten Domänen Namens oder eines einfachen Domänen namens vorliegen.|

## <a name="remarks"></a>Bemerkungen

Der DNS-Domänen Namen Parameter sollte in Großbuchstaben eingegeben werden. Andernfalls fordert der **Ksetup** -Befehl eine Überprüfung an, um den Vorgang fortzusetzen.

Das Festlegen des Kerberos-Bereichs auf einem Domänen Controller wird nicht unterstützt. Wenn Sie versuchen, dies zu tun, wird eine Warnung und ein Befehls Fehler verursacht.

## <a name="examples"></a>Beispiele

Legen Sie den Bereich für diesen Computer auf einen bestimmten Domänen Namen fest, um den Zugriff durch einen nicht-Domänen Controller direkt auf den Bereich "Domäne" von "Configuration Manager" zu beschränken:
```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)