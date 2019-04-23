---
title: ksetup:getenctypeattr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 302f94616f98eb350332b08ad37a58305a0a0be1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841991"
---
# <a name="ksetupgetenctypeattr"></a>ksetup:getenctypeattr



Ruft das Typattribut der Verschlüsselung für die Domäne ab. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /getenctypeattr <DomainName> 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DomainName>|Der Name der Domäne, die zum Herstellen einer Verbindung werden soll. Verwenden Sie den vollqualifizierten Domänennamen oder ein einfaches Formular mit dem Namen, z. B. "corp.contoso.com" "oder" Contoso.|

## <a name="remarks"></a>Hinweise

Führen Sie zum Anzeigen des Verschlüsselungstyp für das Kerberos-Ticket-granting-Ticket (TGT) und der Sitzungsschlüssel der **Klist** Befehl und die Ausgabe anzuzeigen.

Wenn der Befehl erfolgreich ausgeführt wird oder fehlschlägt, wird eine Statusmeldung mit der Fertigstellung erfolgreiche oder fehlgeschlagene angezeigt.

Um der Domäne festzulegen, die Sie zum Herstellen einer Verbindung mit und verwenden möchten, führen Sie die **Ksetup/Domain \<DomainName >** Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Überprüfen Sie das Typattribut der Verschlüsselung für die Domäne aus:
```
ksetup /getenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)