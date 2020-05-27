---
title: Kennwort für Ksetup
description: Referenz Thema für den Befehl "Ksetup ChangePassword", bei dem das Kennwort für den Schlüsselverteilungscenter (KDC)-Kennwort (kpasswd) verwendet wird, um das Kennwort des angemeldeten Benutzers zu ändern.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c1ed9d9b611a7911c4a22c7ca803b480f52f323
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817980"
---
# <a name="ksetup-changepassword"></a>Kennwort für Ksetup

Verwendet das Kennwort für den Schlüsselverteilungscenter (KDC)-Kennwort (kpasswd), um das Kennwort des angemeldeten Benutzers zu ändern. Die Ausgabe des Befehls informiert Sie über den Status Erfolg oder Fehler.

Sie können überprüfen, ob **kpasswd** festgelegt ist, indem Sie den `ksetup /dumpstate` Befehl ausführen und die Ausgabe anzeigen.


## <a name="syntax"></a>Syntax

```
ksetup /changepassword <oldpassword> <newpassword>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<oldpassword>` | Gibt das vorhandene Kennwort des angemeldeten Benutzers an. |
| `<newpassword>` | Gibt das neue Kennwort des angemeldeten Benutzers an. Dieses Kennwort muss alle Kenn Wort Anforderungen erfüllen, die auf diesem Computer festgelegt sind. |

#### <a name="remarks"></a>Hinweise

- Wenn das Benutzerkonto in der aktuellen Domäne nicht gefunden wird, werden Sie vom System aufgefordert, den Domänen Namen anzugeben, in dem sich das Benutzerkonto befindet.

- Wenn Sie bei der nächsten Anmeldung eine Kenn Wort Änderung erzwingen möchten, kann mit diesem Befehl das Sternchen (*) verwendet werden, damit der Benutzer zur Eingabe eines neuen Kennworts aufgefordert wird.

-

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Kennwort eines Benutzers zu ändern, der derzeit in dieser Domäne an diesem Computer angemeldet ist:

```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```

Geben Sie Folgendes ein, um das Kennwort eines Benutzers zu ändern, der zurzeit in der Domäne "Domäne" angemeldet ist:

```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```

Geben Sie Folgendes ein, um zu erzwingen, dass der aktuell angemeldete Benutzer das Kennwort bei der nächsten Anmeldung ändert:

```
ksetup /changepassword Pas$w0rd *
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup (dumpstate-Befehl)](ksetup-dumpstate.md)

- [Ksetup-Befehl "addkpasswd"](ksetup-addkpasswd.md)

- [Ksetup-Befehl "Delta passwd"](ksetup-delkpasswd.md)

- [Ksetup (dumpstate-Befehl)](ksetup-dumpstate.md)
