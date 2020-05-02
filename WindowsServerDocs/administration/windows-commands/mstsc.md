---
title: mstsc
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3355aa310bb9919b5218052878d94416f577381
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723833"
---
# <a name="mstsc"></a>mstsc

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

von werden Verbindungen mit Remotedesktop-Sitzungshost-Servern (RD-Sitzungs Host) oder anderen Remote Computern hergestellt, eine vorhandene Remotedesktopverbindung (RDP-Konfigurationsdatei) bearbeitet und ältere Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien migriert.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

### <a name="parameters"></a>Parameter

|        Parameter        |                                                         BESCHREIBUNG                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   Gibt den Namen einer RDP-Datei für die Verbindung an.                                    |
|  /v: <Server\>[: <Port\>] |                Gibt den Remote Computer und optional die Portnummer an, mit der Sie eine Verbindung herstellen möchten.                 |
|         /admin          |                                   Stellt eine Verbindung mit einer-Sitzung zur Verwaltung des-Servers her.                                   |
|           /f            |                                    startet Remotedesktopverbindung im Vollbildmodus.                                    |
|       /w<Width>        |                                      Gibt die Breite des Remotedesktop Fensters an.                                      |
|       /h<Height>       |                                     Gibt die Höhe des Remotedesktop Fensters an.                                      |
|         /Public         |                  Führt Remotedesktop im öffentlichen Modus aus. Im öffentlichen Modus werden Kenn Wörter und Bitmaps nicht zwischengespeichert.                  |
|          /Span          | Entspricht der Remotedesktop Breite und-Höhe mit dem lokalen virtuellen Desktop, bei Bedarf über mehrere Monitore hinweg. |
| /Edit<Connection File> |                                         Öffnet die angegebene RDP-Datei zum Bearbeiten.                                          |
|        /migrate         |       Migriert Legacy-Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien.       |
|           /?            |                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                             |

## <a name="remarks"></a>Bemerkungen
-   "Default. RDP" wird für jeden Benutzer als versteckte Datei im Ordner "Dokumente" des Benutzers gespeichert. Vom Benutzer erstellte RDP-Dateien werden standardmäßig im Ordner "Dokumente" des Benutzers gespeichert, können aber an einem beliebigen Speicherort gespeichert werden.
-   Für Monitore muss die gleiche Auflösung verwendet werden, und Sie müssen horizontal ausgerichtet werden (d. h. nebeneinander). Es ist derzeit nicht unterstützt, mehrere Monitore vertikal auf dem Client System zu überspannen.

## <a name="examples"></a>Beispiele
-   Zum Herstellen einer Verbindung mit einer Sitzung im Vollbildmodus geben Sie Folgendes ein:
    ```
    mstsc /f
    ```
-   Um eine Datei namens filename. RDP zum Bearbeiten zu öffnen, geben Sie Folgendes ein:
    ```
    mstsc /edit filename.rdp
    ```

## <a name="additional-references"></a>Zusätzliche Referenzen
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
