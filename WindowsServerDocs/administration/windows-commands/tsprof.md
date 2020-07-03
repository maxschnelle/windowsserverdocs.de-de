---
title: tsprof
description: Referenz Artikel für TSPROF, der die Remotedesktopdienste Benutzer Konfigurationsinformationen von einem Benutzer auf einen anderen kopiert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0b030f6f1353a6570883cf44c17e383b929cb3a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937329"
---
# <a name="tsprof"></a>tsprof

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Kopiert die Remotedesktopdienste Benutzer Konfigurationsinformationen von einem Benutzer in einen anderen.
Die Remotedesktopdienste Benutzer Konfigurationsinformationen werden in den Remotedesktopdienste-Erweiterungen für lokale Benutzer und Gruppen sowie für Active Directory-Benutzer und-Computer angezeigt.

**TSPROF** kann auch den Profilpfad für einen Benutzer festlegen.



> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsprof /update {/domain:<DomainName> | /local} /profile:<path> <UserName>
tsprof /copy {/domain:<DomainName> | /local} [/profile:<path>] <Src_usr> <Dest_usr>
tsprof /q {/domain:<DomainName> | /local} <UserName>
```

### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/update|Aktualisiert Profilpfad Informationen für <*Benutzernamen*> in *Domänen* <Domain Name> auf <*ProfilePath* ->.|
|/Domain\<DomainName>|Gibt den Namen der Domäne an, in der der Vorgang angewendet wird.|
|/local ein|Wendet den Vorgang nur auf lokale Benutzerkonten an.|
|/profile\<path>|Gibt den Profilpfad an, der in den Remotedesktopdienste Erweiterungen in lokale Benutzer und Gruppen und Active Directory-Benutzer und-Computer angezeigt wird.|
|\<UserName>|Gibt den Namen des Benutzers an, für den Sie den Serverprofil Pfad aktualisieren oder Abfragen möchten.|
|/Copy|Kopiert Benutzer Konfigurationsinformationen aus \<*SourceUser*> in \<*DestinationUser*> und aktualisiert die Profilpfad Informationen für \<*DestinationUser*> in \<*Profilepath*> . Sowohl \<*SourceUser*> als auch \<*DestinationUser*> müssen entweder lokal oder in der Domäne sein \<*DomainName*> .|
|\<Src_usr>|Gibt den Namen des Benutzers an, von dem Sie die Benutzer Konfigurationsinformationen kopieren möchten.|
|\<Dest_usr>|Gibt den Namen des Benutzers an, in den die Benutzer Konfigurationsinformationen kopiert werden sollen.|
|/q|Zeigt den aktuellen Profilpfad des Benutzers an, für den Sie den Serverprofil Pfad Abfragen möchten.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der Befehl " **TSPROF** " ist nur verfügbar, wenn Sie den Terminal Server-Rollen Dienst auf einem Computer mit Windows Server 2008 oder RD-Sitzungshost Rollen Dienst auf einem Computer mit Windows Server 2008 R2 installiert haben.

## <a name="examples"></a>Beispiele
-   Um Benutzer Konfigurationsinformationen von LocalUser1 nach LocalUser2 zu kopieren, geben Sie Folgendes ein:
    ```
    tsprof /copy /local LocalUser1 LocalUser2
    ```
-   Um den Remotedesktopdienste Profilpfad für LocalUser1 auf ein Verzeichnis namens c:\Profiles festzulegen, geben Sie Folgendes ein:
    ```
    tsprof /update /local /profile:c:\profiles LocalUser1
    ```

## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
