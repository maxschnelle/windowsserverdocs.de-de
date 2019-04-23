---
title: ksetup:delenctypeattr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c2cc96e8156cafd3846422596abe62513e275b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838131"
---
# <a name="ksetupdelenctypeattr"></a>ksetup:delenctypeattr



Entfernt das Typattribut der Verschlüsselung für die Domäne an. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delenctypeattr <DomainName> 
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DomainName>|Der Name der Domäne, die zum Herstellen einer Verbindung werden soll. Verwenden Sie den vollqualifizierten Domänennamen oder ein einfaches Formular mit dem Namen, z. B. "corp.contoso.com" "oder" Contoso.|

## <a name="remarks"></a>Hinweise

Führen Sie zum Anzeigen des Verschlüsselungstyp für das Kerberos-Ticket-granting-Ticket (TGT) und der Sitzungsschlüssel der **Klist** Befehl und die Ausgabe anzuzeigen.

Eine Statusmeldung wird nach Abschluss von erfolgreichen oder fehlgeschlagenen angezeigt.

Um der Domäne festzulegen, die Sie zum Herstellen einer Verbindung mit und verwenden möchten, führen Sie die **Ksetup/Domain \<DomainName >** Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Bestimmen Sie die aktuellen Verschlüsselungstypen, die auf diesem Computer festgelegt sind:
```
klist
```
Legen Sie die Domäne mit.contoso.com:
```
ksetup /domain mit.contoso.com
```
Überprüfen Sie, was das Typattribut der Verschlüsselung für die Domäne ist:
```
ksetup /getenctypeattr mit.contoso.com
```
Entfernen Sie Set Encryption Type-Attributs für die Domäne mit.contoso.com:
```
ksetup /delenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)