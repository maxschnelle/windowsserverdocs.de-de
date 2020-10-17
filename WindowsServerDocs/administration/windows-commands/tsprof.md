---
title: tsprof
description: Referenz Artikel für den Befehl "TSPROF", mit dem die Remotedesktopdienste Benutzer Konfigurationsinformationen von einem Benutzer auf einen anderen kopiert werden.
ms.topic: reference
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e18f736a31af3cc649d4921197710f713e7df6af
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156346"
---
# <a name="tsprof"></a>tsprof

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert die Remotedesktopdienste Benutzer Konfigurationsinformationen von einem Benutzer in einen anderen. Die Remotedesktopdienste Benutzer Konfigurationsinformationen werden in den Remotedesktopdienste-Erweiterungen für lokale Benutzer und Gruppen sowie für Active Directory-Benutzer und-Computer angezeigt.

> [!NOTE]
> Sie können auch den [TSPROF-Befehl](tsprof.md) verwenden, um den Profilpfad für einen Benutzer festzulegen.
>
> Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
tsprof /update {/domain:<Domainname> | /local} /profile:<path> <username>
tsprof /copy {/domain:<Domainname> | /local} [/profile:<path>] <src_user> <dest_user>
tsprof /q {/domain:<Domainname> | /local} <username>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /update | Aktualisiert Profilpfad Informationen für `<username>` in der Domäne in `<domainname>` `<profilepath>` . |
| /Domain`<Domainname>` | Gibt den Namen der Domäne an, in der der Vorgang angewendet wird. |
| /local ein | Wendet den Vorgang nur auf lokale Benutzerkonten an. |
| /profile`<path>` | Gibt den Profilpfad an, der in den Remotedesktopdienste Erweiterungen in lokale Benutzer und Gruppen und Active Directory-Benutzer und-Computer angezeigt wird. |
| `<username>` | Gibt den Namen des Benutzers an, für den Sie den Serverprofil Pfad aktualisieren oder Abfragen möchten. |
| /Copy | Kopiert Benutzer Konfigurationsinformationen aus `<src_user>` in `<dest_user>` und aktualisiert die Profilpfad Informationen für `<dest_user>` in `<profilepath>` . Sowohl `<src_user>` als auch `<dest_user>` müssen entweder lokal oder in der Domäne sein `<domainname>` . |
| `<src_user>` | Gibt den Namen des Benutzers an, von dem Sie die Benutzer Konfigurationsinformationen kopieren möchten. Wird auch als Quell Benutzer bezeichnet. |
| `<dest_user>` | Gibt den Namen des Benutzers an, in den die Benutzer Konfigurationsinformationen kopiert werden sollen. Wird auch als Ziel Benutzer bezeichnet. |
| /q | Zeigt den aktuellen Profilpfad des Benutzers an, für den Sie den Serverprofil Pfad Abfragen möchten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um Benutzer Konfigurationsinformationen von *LocalUser1* nach *LocalUser2*zu kopieren, geben Sie Folgendes ein:

```
tsprof /copy /local LocalUser1 LocalUser2
```

Um den Remotedesktopdienste Profilpfad für *LocalUser1* auf ein Verzeichnis namens *c:\Profiles*festzulegen, geben Sie Folgendes ein:

```
tsprof /update /local /profile:c:\profiles LocalUser1
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
