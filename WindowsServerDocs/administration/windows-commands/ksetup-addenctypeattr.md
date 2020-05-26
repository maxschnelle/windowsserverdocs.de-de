---
title: Ksetup addenctypeattr
description: Referenz Thema für den Befehl "Ksetup addenctypeattr", mit dem das Attribut "Verschlüsselungstyp" der Liste der möglichen Typen für die Domäne hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7162e35c88cea0cfa2828e12cc4af59eaed66c9
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818150"
---
# <a name="ksetup-addenctypeattr"></a>Ksetup addenctypeattr

Fügt der Liste der möglichen Typen für die Domäne das Attribut Verschlüsselungstyp hinzu. Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

## <a name="syntax"></a>Syntax

```
ksetup /addenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<domainname>` | Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager. |
| Verschlüsselungstyp | Muss einer der folgenden unterstützten Verschlüsselungstypen sein:<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128-CTS-HMAC-SHA1-96</li><li>AES256-CTS-HMAC-SHA1-96</li></ul> |

#### <a name="remarks"></a>Hinweise

- Sie können mehrere Verschlüsselungstypen festlegen oder hinzufügen, indem Sie die Verschlüsselungstypen im Befehl durch ein Leerzeichen trennen. Dies ist jedoch nur für eine Domäne gleichzeitig möglich.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzuzeigen:

```
klist
```

Um die Domäne auf Corp.contoso.com festzulegen, geben Sie Folgendes ein:

```
ksetup /domain corp.contoso.com
```

Geben Sie Folgendes ein, um den Verschlüsselungstyp *AES-256-CTS-HMAC-SHA1-96* der Liste der möglichen Typen für die Domäne *Corp.contoso.com*hinzuzufügen:

```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Geben Sie Folgendes ein, um das Verschlüsselungstyp Attribut für die Domäne *Corp.contoso.com*auf *AES-256-CTS-HMAC-SHA1-96* festzulegen:

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Geben Sie Folgendes ein, um zu überprüfen, ob das Verschlüsselungstyp Attribut für die Domäne festgelegt wurde:

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [klist-Befehl](klist.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Domänen Befehl](ksetup-domain.md)

- [Ksetup setenctypeattr-Befehl](ksetup-setenctypeattr.md)

- [Ksetup getenctypeattr-Befehl](ksetup-getenctypeattr.md)

- [Ksetup-Befehl "Delta TYPEATTR"](ksetup-delenctypeattr.md)
