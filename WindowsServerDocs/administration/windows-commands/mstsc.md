---
title: mstsc
description: Referenz Artikel für den mstsc-Befehl, der Verbindungen mit Remotedesktop-Sitzungshost Servern oder anderen Remote Computern erstellt, eine vorhandene Remotedesktopverbindung (RDP-Konfigurationsdatei) bearbeitet und ältere Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien migriert.
ms.topic: reference
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: f47a8ad0db569c82d64e74b10c30bec9aca958ab
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640541"
---
# <a name="mstsc"></a>mstsc

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Erstellt Verbindungen mit Remotedesktop-Sitzungshost Servern oder anderen Remote Computern, bearbeitet eine vorhandene Remotedesktopverbindung (. RDP)-Konfigurationsdatei und migriert ältere Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien.

## <a name="syntax"></a>Syntax

```
mstsc.exe [<connectionfile>] [/v:<server>[:<port>]] [/admin] [/f] [/w:<width> /h:<height>] [/public] [/span]
mstsc.exe /edit <connectionfile>
mstsc.exe /migrate
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ------------|
| `<connectionfile>` | Gibt den Namen einer RDP-Datei für die Verbindung an. |
| /v:`<server>[:<port>]` | Gibt den Remote Computer und optional die Portnummer an, mit der Sie eine Verbindung herstellen möchten. |
| /admin | Stellt eine Verbindung mit einer-Sitzung zur Verwaltung des-Servers her. |
| /f | Startet Remotedesktopverbindung im Vollbildmodus. |
| /w`<width>` | Gibt die Breite des Remotedesktop Fensters an. |
| /h`<height>` | Gibt die Höhe des Remotedesktop Fensters an. |
| /Public | Führt Remotedesktop im öffentlichen Modus aus. Im öffentlichen Modus werden Kenn Wörter und Bitmaps nicht zwischengespeichert. |
| /Span | Entspricht der Remotedesktop Breite und-Höhe mit dem lokalen virtuellen Desktop, bei Bedarf über mehrere Monitore hinweg. |
| /Edit `<connectionfile>` | Öffnet die angegebene RDP-Datei zum Bearbeiten. |
| /migrate | Migriert Legacy-Verbindungs Dateien, die mit dem Clientverbindungs-Manager erstellt wurden, in neue RDP-Verbindungs Dateien. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- "Default. RDP" wird für jeden Benutzer als versteckte Datei im Ordner " **Dokumente** " des Benutzers gespeichert.

- Vom Benutzer erstellte RDP-Dateien werden standardmäßig im Ordner " **Dokumente** " des Benutzers gespeichert, können aber an einem beliebigen Speicherort gespeichert werden.

- Für Monitore muss die gleiche Auflösung verwendet werden, und Sie müssen horizontal ausgerichtet werden (d. h. nebeneinander). Es ist derzeit nicht unterstützt, mehrere Monitore vertikal auf dem Client System zu überspannen.

### <a name="examples"></a>Beispiele

Zum Herstellen einer Verbindung mit einer Sitzung im Vollbildmodus geben Sie Folgendes ein:

```
mstsc /f
```
oder
```
mstsc /v:computer1 /f
```
Um Breite/Höhe zuzuweisen, geben Sie Folgendes ein:

```
mstsc /v:computer1 /w:1920 /h:1080
```
Um eine Datei namens *filename. RDP* zum Bearbeiten zu öffnen, geben Sie Folgendes ein:

```
mstsc /edit filename.rdp
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
