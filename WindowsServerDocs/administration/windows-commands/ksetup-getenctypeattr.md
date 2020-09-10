---
title: ksetup getenctypeattr
description: Referenz Artikel für den Befehl "Ksetup getenctypeattr", der das Verschlüsselungstyp Attribut für die Domäne abruft.
ms.topic: reference
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f8dc2a1c7c4a2d17ca1fb0e5099fdb25a818d2aa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640039"
---
# <a name="ksetup-getenctypeattr"></a>ksetup getenctypeattr

Ruft das Verschlüsselungstyp Attribut für die Domäne ab. Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

Sie können den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzeigen, indem Sie den Befehl **klist** ausführen und die Ausgabe anzeigen. Sie können die Domäne so festlegen, dass eine Verbindung mit hergestellt und verwendet wird, indem Sie den `ksetup /domain <domainname>` Befehl ausführen.

## <a name="syntax"></a>Syntax

```
ksetup /getenctypeattr <domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<domainname>` | Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Verwenden Sie den voll qualifizierten Domänen Namen oder eine einfache Form des Namens, z. b. Corp.contoso.com oder Configuration Manager. |

### <a name="examples"></a>Beispiele

Um das Verschlüsselungstyp Attribut für die Domäne zu überprüfen, geben Sie Folgendes ein:

```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [klist-Befehl](klist.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Domänen Befehl](ksetup-domain.md)

- [Ksetup-Befehl "addenctypeattr"](ksetup-addenctypeattr.md)

- [Ksetup setenctypeattr-Befehl](ksetup-setenctypeattr.md)

- [Ksetup-Befehl "Delta TYPEATTR"](ksetup-delenctypeattr.md)
