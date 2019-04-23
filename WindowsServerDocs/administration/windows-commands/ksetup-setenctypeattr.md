---
title: ksetup:setenctypeattr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a91539ec7a9e0ce4c75d5165da1b88ae36d3fe6c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879201"
---
# <a name="ksetupsetenctypeattr"></a>ksetup:setenctypeattr



Legt das Typattribut der Verschlüsselung für die Domäne fest. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<DomainName>|Der Name der Domäne, die zum Herstellen einer Verbindung werden soll. Verwenden Sie den vollqualifizierten Domänennamen oder ein einfaches Formular mit dem Namen, z. B. "corp.contoso.com" "oder" Contoso.|
|Verschlüsselungstyp|Dabei muss es sich um eine der folgenden unterstützten Verschlüsselungsarten sein:</br>-   DES-CBC-CRC</br>-   DES-CBC-MD5</br>-   RC4-HMAC-MD5</br>-   AES128-CTS-HMAC-SHA1-96</br>-   AES256-CTS-HMAC-SHA1-96|

## <a name="remarks"></a>Hinweise

Führen Sie zum Anzeigen des Verschlüsselungstyp für das Kerberos-Ticket-granting-Ticket (TGT) und der Sitzungsschlüssel der **Klist** Befehl und die Ausgabe anzuzeigen.

Sie können festlegen, oder fügen Sie mehrere Verschlüsselungstypen hinzu, indem die Verschlüsselungstypen im Befehl durch ein Leerzeichen trennen. Allerdings können Sie nur für eine Domäne zu einem Zeitpunkt dafür.

Wenn der Befehl erfolgreich ausgeführt wird oder fehlschlägt, wird eine Statusmeldung angezeigt.

Um der Domäne festzulegen, die Sie zum Herstellen einer Verbindung mit und verwenden möchten, führen Sie die **Ksetup/Domain \<DomainName >** Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Bestimmen Sie die aktuellen Verschlüsselungstypen, die auf diesem Computer festgelegt sind:
```
klist
```
Legen Sie die Domäne "corp.contoso.com":
```
ksetup /domain corp.contoso.com
```
Das Typattribut der Verschlüsselung auf AES-256-CTS-HMAC-SHA1-96 für die Domäne "corp.contoso.com" festgelegt:
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Stellen Sie sicher, dass die Verschlüsselung-Type-Attribut festgelegt wurde, wie für die Domäne vorgesehen:
```
ksetup /getenctypeattr corp.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)