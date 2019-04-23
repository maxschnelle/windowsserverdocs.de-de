---
title: ksetup:setrealm
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: aa6b2a21904ec4dae1e60def5bd36647291b1af6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877401"
---
# <a name="ksetupsetrealm"></a>ksetup:setrealm



Legt den Namen von einem Kerberos-Bereich. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setrealm <DNSDomainName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DNSDomainName>|Der DNS-Domänenname kann in Form eines vollständig qualifizierten Domänennamen oder den einfachen Domänennamen sein.|

## <a name="remarks"></a>Hinweise

Parameter für den DNS-Domänennamen sollten in Großbuchstaben eingegeben werden. Andernfalls die **Ksetup** Befehl fragt für die Überprüfung, um den Vorgang fortzusetzen.

Festlegen des Kerberos-Bereichs auf einem Domänencontroller wird nicht unterstützt. Dies dennoch versuchen, verursacht eine Warnung und einen Befehl Fehler.

## <a name="BKMK_Examples"></a>Beispiele für

Legen Sie den Bereich für diesen Computer auf einen bestimmten Domänennamen, den Zugriff von einem Domänencontroller nur auf dem CONTOSO-Kerberos-Bereich zu beschränken:
```
ksetup /setrealm CONTOSO
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)