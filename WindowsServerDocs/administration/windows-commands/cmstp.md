---
title: cmstp
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd2e8dbb08b41875335b35dd802007a0bd1fbd41
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379270"
---
# <a name="cmstp"></a>cmstp

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Installiert oder entfernt ein Verbindungs-Manager-Dienst Profil. Wenn Sie ohne optionale Parameter verwendet wird, installiert **Cmstp** ein Dienst Profil mit den Standardeinstellungen, die für das Betriebssystem und die Berechtigungen des Benutzers geeignet sind. 
## <a name="syntax"></a>Syntax
Syntax 1:
```
ServiceProfileFileName .exe /q:a /c:"cmstp.exe ServiceProfileFileName .inf [/nf] [/ni] [/ns] [/s] [/su] [/u]"
```
Syntax 2:
```
cmstp.exe [/nf] [/ni] [/ns] [/s] [/su] [/u]  [Drive:][path]ServiceProfileFileName.inf"
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|< Serviceprofilefilename >. exe|Gibt anhand des Namens das Installationspaket an, das das zu installierende Profil enthält.<br /><br />Erforderlich für Syntax 1, aber nicht gültig für Syntax 2.|
|/q:a|Gibt an, dass das Profil installiert werden soll, ohne den Benutzer aufzufordern. Die Überprüfungs Meldung, dass die Installation erfolgreich war, wird weiterhin angezeigt.<br /><br />Erforderlich für Syntax 1, aber nicht gültig für Syntax 2.|
|[Laufwerk:] [Pfad] @no__t -0. inf|Erforderlich. Gibt den Namen der Konfigurationsdatei an, die bestimmt, wie das Profil installiert werden soll.<br /><br />Der [Laufwerk:] [Pfad]-Parameter ist für Syntax 1 ungültig.|
|/nf|Gibt an, dass die Unterstützungs Dateien nicht installiert werden sollen.|
|/ni|Gibt an, dass kein Desktop Symbol erstellt werden soll. Dieser Parameter ist nur gültig für Computer, auf denen Windows 95, Windows 98, Windows NT 4,0 oder Windows Millennium Edition ausgeführt wird.|
|/ns|Gibt an, dass keine Desktop Verknüpfung erstellt werden soll. Dieser Parameter ist nur gültig für Computer, auf denen ein Mitglied der Windows Server 2003-Produktfamilie, Windows 2000 oder Windows XP ausgeführt wird.|
|/s|Gibt an, dass das Dienst Profil im Hintergrund installiert oder deinstalliert werden soll (ohne Aufforderung zur Eingabe eines Benutzers oder zum Anzeigen der Überprüfungs Meldung).|
|/su|Gibt an, dass das Dienst Profil für einen einzelnen Benutzer und nicht für alle Benutzer installiert werden soll. Dieser Parameter ist nur gültig für Computer, auf denen Windows Server 2003, Windows 2000 oder Windows XP ausgeführt wird.|
|/au|Gibt an, dass das Dienst Profil für alle Benutzer installiert werden soll. Dieser Parameter ist nur gültig für Computer, auf denen Windows Server 2003, Windows 2000 oder Windows XP ausgeführt wird.|
|/u|Gibt an, dass das Dienst Profil deinstalliert werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
**/s** ist der einzige Parameter, den Sie in Kombination mit **/u**verwenden können.
Syntax 1 ist die typische Syntax, die in einer benutzerdefinierten Installationsanwendung verwendet wird. Um diese Syntax zu verwenden, müssen Sie **Cmstp** aus dem Verzeichnis ausführen, das die Datei @no__t -1. exe enthält.
## <a name="BKMK_Examples"></a>Beispiele
Geben Sie Folgendes ein, um das unfiktive Dienst Profil ohne Unterstützungs Dateien zu installieren:
```
fiction.exe /c:"cmstp.exe fiction.inf /nf"
```
Geben Sie Folgendes ein, um das Benutzerprofil für einen einzelnen Benutzer automatisch zu installieren:
```
fiction.exe /c:"cmstp.exe fiction.inf /s /su"
```
Geben Sie Folgendes ein, um das Dienst Profil für den-Typ im Hintergrund
```
fiction.exe /c:"cmstp.exe fiction.inf /s /u"
```
## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
