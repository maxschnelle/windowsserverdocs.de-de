---
title: tsprof
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e17d60126125fcd4b10373133dd61ca0db030290
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836071"
---
# <a name="tsprof"></a>tsprof

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Kopiert die Konfigurationsinformationen für die Remote Desktop Services-Benutzer von einem Benutzer.
Die Konfigurationsinformationen für die Remote Desktop Services-Benutzer wird in der Remote Desktop Services-Erweiterungen für lokale Benutzer und Gruppen und active Directory-Benutzer und Computer angezeigt.

**Tsprof** können auch den Profilpfad für einen Benutzer festlegen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsprof /update {/domain:<DomainName> | /local} /profile:<path> <UserName>
tsprof /copy {/domain:<DomainName> | /local} [/profile:<path>] <Src_usr> <Dest_usr>
tsprof /q {/domain:<DomainName> | /local} <UserName>
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/update|Updates Profilinformationen Pfad für <*Benutzername*> in Domäne <*DomainName*>, <*Profilpfad*>.|
|/ Domain:\<DomainName >|Gibt den Namen der Domäne, in der der Vorgang angewendet wird.|
|/local|Gilt den Vorgang nur auf lokale Benutzerkonten.|
|/profile:\<path>|Gibt den Profilpfad eingeben, wie in der Remote Desktop Services-Erweiterungen in lokale Benutzer und Gruppen und active Directory-Benutzer und Computer angezeigt.|
|\<Benutzername >|Gibt den Namen des Benutzers für die Sie aktualisieren oder den Terminalserver-Profilpfad abfragen möchten.|
|Copy|Kopiert die Informationen der Konfiguration von \< *SourceUser*> um \< *-destinationuser*> und aktualisiert die Pfad-Profilinformationen für \<  *Zielbenutzer*> um \< *Profilpfad*>. Beide \< *SourceUser*> und \< *-destinationuser*> müssen lokal sein oder muss in der Domäne \< *DomainName*> .|
|\<Src_usr>|Gibt den Namen des Benutzers, von denen Sie die Informationen der Benutzerkonfiguration kopieren möchten.|
|\<Dest_usr>|Gibt den Namen des Benutzers, der Sie die Konfigurationsinformationen für den Benutzer kopieren möchten.|
|/q|Zeigt den aktuellen Profilpfad des Benutzers für die die Terminalserver-Profilpfad abgefragt werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Tsprof** Befehl ist nur verfügbar, wenn Sie die Terminalserver-Rollendienst auf einem Computer unter Windows Server 2008 oder RD-Sitzungshost-Rollendiensts auf einem Computer unter Windows Server 2008 R2 installiert haben.

## <a name="BKMK_examples"></a>Beispiele für
-   Um die Konfigurationsinformationen für Benutzer von Lokalerbenutzer1 in LocalUser2 zu kopieren, geben Sie Folgendes ein:
    ```
    tsprof /copy /local LocalUser1 LocalUser2
    ```
-   Um den Remote Desktop Services-Profilpfad für Lokalerbenutzer1 in ein Verzeichnis namens "c:\profiles" festzulegen, geben Sie Folgendes ein:
    ```
    tsprof /update /local /profile:c:\profiles LocalUser1
    ```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
