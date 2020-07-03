---
title: ksetup delenctypeattr
description: Referenz Artikel für das Ksetup-Delta TYPEATTR, das das Verschlüsselungstyp Attribut für die Domäne entfernt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5aabbb99f40d8d22189d6abccc188161b7ee2f5c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925483"
---
# <a name="ksetup-delenctypeattr"></a>ksetup delenctypeattr

Entfernt das Verschlüsselungstyp Attribut für die Domäne. Bei erfolgreicher oder fehlgeschlagener Ausführung wird eine Statusmeldung angezeigt.

Sie können den Verschlüsselungstyp für das Kerberos-Ticket Erteilungs Ticket (TGT) und den Sitzungsschlüssel anzeigen, indem Sie den Befehl **klist** ausführen und die Ausgabe anzeigen. Sie können die Domäne so festlegen, dass eine Verbindung mit hergestellt und verwendet wird, indem Sie den `ksetup /domain <domainname>` Befehl ausführen.

## <a name="syntax"></a>Syntax

```
ksetup /delenctypeattr <domainname>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| ----------| ----------- |
| `<domainname>` | Der Name der Domäne, zu der Sie eine Verbindung herstellen möchten. Sie können entweder den voll qualifizierten Domänen Namen oder eine einfache Form des Namens verwenden, z. b. "Corp.contoso.com" oder "Configuration Manager". |

### <a name="examples"></a>Beispiele

Um die aktuellen Verschlüsselungstypen zu bestimmen, die auf diesem Computer festgelegt sind, geben Sie Folgendes ein:

```
klist
```

Um die Domäne auf mit.contoso.com festzulegen, geben Sie Folgendes ein:

```
ksetup /domain mit.contoso.com
```

Geben Sie Folgendes ein, um zu überprüfen, welches Verschlüsselungstyp Attribut für die Domäne gilt:

```
ksetup /getenctypeattr mit.contoso.com
```

Um das Set encryption type-Attribut für die Domäne mit.contoso.com zu entfernen, geben Sie Folgendes ein:

```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [klist-Befehl](klist.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Domänen Befehl](ksetup-domain.md)

- [Ksetup-Befehl "addenctypeattr"](ksetup-addenctypeattr.md)

- [Ksetup setenctypeattr-Befehl](ksetup-setenctypeattr.md)
