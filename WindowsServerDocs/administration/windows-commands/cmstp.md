---
title: cmstp
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0ee5c5189b4eab21994def221dd757b0061ef22d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836381"
---
# <a name="cmstp"></a>cmstp

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Installiert oder entfernt ein Dienstprofil der Verbindungs-Manager. Ohne optionale Parameter **Cmstp** ein Service-Profil mit den Standardeinstellungen entsprechende, um das Betriebssystem und die Berechtigungen des Benutzers installiert. 
## <a name="syntax"></a>Syntax
1-Syntax:
```
ServiceProfileFileName .exe /q:a /c:"cmstp.exe ServiceProfileFileName .inf [/nf] [/ni] [/ns] [/s] [/su] [/u]"
```
2-Syntax:
```
cmstp.exe [/nf] [/ni] [/ns] [/s] [/su] [/u]  [Drive:][path]ServiceProfileFileName.inf"
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|< ServiceProfileFileName >.exe|Gibt den Namen, das Installationspaket, das das Profil enthält, das Sie installieren möchten.<br /><br />Bei Syntax 1 jedoch nicht gültig erforderlich für die Syntax 2.|
|/q:a|Gibt an, dass das Profil installiert werden soll, ohne den Benutzer aufzufordern. Die Bestätigungsnachricht, die die Installation erfolgreich war, wird weiterhin angezeigt.<br /><br />Bei Syntax 1 jedoch nicht gültig erforderlich für die Syntax 2.|
|[Laufwerk:] [Pfad] <ServiceProfileFileName>INF|Erforderlich. Gibt den Namen die Konfigurationsdatei, die bestimmt, wie das Profil installiert werden soll.<br /><br />Die [Laufwerk:] [Pfad]-Parameter ist ungültig bei Syntax 1.|
|/nf|Gibt an, dass die Unterstützungsdateien nicht installiert werden sollen.|
|/ni|Gibt an, dass ein Desktopsymbol nicht erstellt werden soll. Dieser Parameter gilt nur für Computer unter Windows 95, Windows 98, Windows NT 4.0 oder Windows Millennium Edition.|
|/ns|Gibt an, dass eine desktopverknüpfung nicht erstellt werden soll. Dieser Parameter gilt nur für ein Mitglied der Windows Server 2003-Produktfamilie, Windows 2000 oder Windows XP-Computern.|
|/s|Gibt an, die das Dienstprofil sollte installiert oder deinstalliert wird, im Hintergrund (ohne Benutzerantwort anzufordern oder Bestätigungsnachricht angezeigt).|
|/su|Gibt an, dass das Service-Profil für einen einzelnen Benutzer und nicht für alle Benutzer installiert werden soll. Dieser Parameter gilt nur für Computer unter einem Windows Server 2003, Windows 2000 oder Windows XP.|
|/au|Gibt an, dass das Service-Profil für alle Benutzer installiert werden soll. Dieser Parameter gilt nur für Computer unter Windows Server 2003, Windows 2000 oder Windows XP.|
|/u|Gibt an, dass es sich bei das Dienstprofil deinstalliert werden soll.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
**/ s** ist der einzige Parameter, mit denen Sie in Kombination mit **/u**.
Syntax 1 ist die typische Syntax, die in einer Anwendung für die benutzerdefinierte Installation verwendet. Um diese Syntax verwenden, müssen Sie ausführen **Cmstp** aus dem Verzeichnis, enthält die <ServiceProfileFileName>.exe-Datei.
## <a name="BKMK_Examples"></a>Beispiele für
Um dem Dienstprofil Fiktion, ohne alle erforderlichen unterstützenden Dateien zu installieren, geben Sie Folgendes ein:
```
fiction.exe /c:"cmstp.exe fiction.inf /nf"
```
Geben Sie Folgendes ein, für die unbeaufsichtigte Installation Science-Fiction-Service-Profil für einen einzelnen Benutzer:
```
fiction.exe /c:"cmstp.exe fiction.inf /s /su"
```
Um dem Dienstprofil Fiktion im Hintergrund zu deinstallieren, geben Sie Folgendes ein:
```
fiction.exe /c:"cmstp.exe fiction.inf /s /u"
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)
