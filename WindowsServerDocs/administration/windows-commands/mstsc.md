---
title: mstsc
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6f89c1e3b0d36f14dbd55f9e6994c788305b30d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437184"
---
# <a name="mstsc"></a>mstsc

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verbindungen mit Remote Desktop Session Host (rd Session Host)-Server oder anderen Remotecomputern erstellt, bearbeitet eine vorhandene Konfigurationsdatei für die Remotedesktopverbindung (RDP) und migriert ältere Verbindungsdateien, die mit Client-Verbindungs-Manager erstellt wurden in neue Dateien in einer RDP-Verbindung.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

## <a name="parameters"></a>Parameter

|        Parameter        |                                                         Beschreibung                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   Gibt den Namen einer RDP-Datei für die Verbindung.                                    |
|   / v: < Server [:<Port>]   |                Gibt an, die Remotecomputer und optional die Portnummer, die Sie eine Verbindung herstellen möchten.                 |
|         /admin          |                                   Verbindet Sie mit einer Sitzung für das Verwalten des Servers.                                   |
|           /f            |                                    Startet Remotedesktopverbindung im Vollbildmodus an.                                    |
|       /w:<Width>        |                                      Gibt die Breite des Fensters Remotedesktop.                                      |
|       /h:<Height>       |                                     Gibt die Höhe des Fensters Remotedesktop.                                      |
|         /public         |                  Remotedesktop im öffentlichen Modus ausgeführt. Im öffentlichen Modus werden Kennwörter und Bitmaps nicht zwischengespeichert.                  |
|          /span          | Entspricht der Remotedesktop-Breite und Höhe mit dem lokalen virtuellen Desktop, die Aufteilung auf mehrere Monitore bei Bedarf. |
| / Edit <Connection File> |                                         Öffnet die angegebene RDP-Datei zur Bearbeitung.                                          |
|        / Migrieren         |       Ältere Verbindungsdateien, die mit Client-Verbindungs-Manager, in neue RDP-Verbindungsdateien erstellt wurden wird migriert.       |
|           /?            |                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                             |

## <a name="remarks"></a>Hinweise
-   Default.RDP wird für jeden Benutzer als eine ausgeblendete Datei im Ordner "Dokumente" des Benutzers gespeichert. Benutzer, die RDP-Dateien erstellt werden standardmäßig im Ordner "Dokumente" des Benutzers gespeichert, jedoch kann eine beliebige Stelle gespeichert werden.
-   Um über Monitore hinweg erstrecken, werden die Monitore müssen die gleiche Auflösung verwenden und müssen horizontal ausgerichtet sein (d. h., parallel). Es gibt derzeit keine Unterstützung für das Aufstellen mehrerer Monitore vertikal auf dem Clientsystem.

## <a name="BKMK_examples"></a>Beispiele für
-   Um zu einer Sitzung in den Vollbildmodus zu verbinden, geben Sie Folgendes ein:
    ```
    mstsc /f
    ```
-   Um eine Datei namens filename.rdp für die Bearbeitung zu öffnen, geben Sie Folgendes ein:
    ```
    mstsc /edit filename.rdp
    ```

#### <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Remotedesktopdienste &#40;Terminaldienste&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
