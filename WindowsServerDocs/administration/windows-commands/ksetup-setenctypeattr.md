---
title: ksetup setenctypeattr
description: Referenz Artikel für den Ksetup-Befehl setenctypeattr, der das Attribut für den Verschlüsselungstyp für die Domäne festlegt.
ms.topic: reference
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9027197817b2fa738726fd0d0feeeeadc5aac0b2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634126"
---
# <a name="ksetup-setenctypeattr"></a>ksetup setenctypeattr

Legt das Verschlüsselungstyp Attribut für die Domäne fest. Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

Sie können den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzeigen, indem Sie den Befehl **klist** ausführen und die Ausgabe anzeigen. Sie können die Domäne so festlegen, dass eine Verbindung mit hergestellt und verwendet wird, indem Sie den `ksetup /domain <domainname>` Befehl ausführen.

## <a name="syntax"></a>Syntax

```
ksetup /setenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
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

Geben Sie Folgendes ein, um das Verschlüsselungstyp Attribut für die Domäne corp.contoso.com auf AES-256-CTS-HMAC-SHA1-96 festzulegen:

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

Geben Sie Folgendes ein, um zu überprüfen, ob das Verschlüsselungstyp Attribut für die Domäne festgelegt wurde:

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [klist-Befehl](klist.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Domänen Befehl](ksetup-domain.md)

- [Ksetup-Befehl "addenctypeattr"](ksetup-addenctypeattr.md)

- [Ksetup getenctypeattr-Befehl](ksetup-getenctypeattr.md)

- [Ksetup-Befehl "Delta TYPEATTR"](ksetup-delenctypeattr.md)
