---
title: 'Ksetup: addenctypeattr'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26441f739979cde31715e5fb06b5f3ab59845d97
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724747"
---
# <a name="ksetupaddenctypeattr"></a>Ksetup: addenctypeattr



Fügt der Liste der möglichen Typen für die Domäne das Attribut Verschlüsselungstyp hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addenctypeattr <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Domain Name>|Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager.|
|Verschlüsselungstyp|Muss einer der folgenden unterstützten Verschlüsselungstypen sein:</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128-CTS-HMAC-SHA1-96</br>-AES256-CTS-HMAC-SHA1-96|

## <a name="remarks"></a>Bemerkungen

Um den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzuzeigen, führen Sie den Befehl **klist** aus, und zeigen Sie die Ausgabe an.

Sie können mehrere Verschlüsselungstypen festlegen oder hinzufügen, indem Sie die Verschlüsselungstypen im Befehl durch ein Leerzeichen trennen. Dies ist jedoch nur für eine Domäne gleichzeitig möglich.

Wenn der Befehl erfolgreich ausgeführt wird oder fehlschlägt, wird eine Statusmeldung angezeigt.

Um die Domäne festzulegen, mit der Sie eine Verbindung herstellen und verwenden möchten, führen Sie den Befehl **Ksetup/Domain \<Domainname>** aus.

## <a name="examples"></a>Beispiele

Bestimmen Sie die aktuellen Verschlüsselungstypen, die auf diesem Computer festgelegt sind:
```
klist
```
Legen Sie die Domäne auf Corp.contoso.com fest:
```
ksetup /domain corp.contoso.com
```
Fügen Sie den Verschlüsselungstyp AES-256-CTS-HMAC-SHA1-96 der Liste der möglichen Typen für die Domäne hinzu Corp.contoso.com:
```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Legen Sie für die Domäne corp.contoso.com das Attribut Verschlüsselungstyp auf AES-256-CTS-HMAC-SHA1-96 fest:
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Vergewissern Sie sich, dass das Verschlüsselungstyp Attribut für die Domäne festgelegt wurde:
```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)