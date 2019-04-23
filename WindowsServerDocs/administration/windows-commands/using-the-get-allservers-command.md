---
title: Mithilfe des Befehls Get-AllServers
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 080836e406b329cf8c15f95ef6afc99973bb3e4d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853091"
---
# <a name="using-the-get-allservers-command"></a>Mithilfe des Befehls Get-AllServers



Ruft Informationen über alle Windows-Bereitstellungsdienste-Server ab.

> [!NOTE]
> Mit diesem Befehl dauert einen erweiterten Zeitraum abgeschlossen wird, wenn viele Windows-Bereitstellungsdienste-Server in Ihrer Umgebung vorhanden sind oder wenn der Verbindungsserver die Netzwerkverbindung langsam ist.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/Show:{Config | Abbilder | Alle}|Gibt an, welche Art von Informationen zurückgegeben.</br>-   **Config** Konfigurationsinformationen für Server zurückgegeben.</br>-   **Images** Informationen Abbildgruppen, Startabbildern und Installationsabbildern auf dem Server zurückgegeben.</br>-   **Alle** sieht in Server-Konfiguration und das angegebene Bild.|
|[/Detailed]|Bei Verwendung in Verbindung mit der **/Show:Images** oder **/Show:All**, gibt alle Metadaten aus jedem Bild image. Wenn die **/detaillierte** Option nicht angegeben wird, ist das Standardverhalten der Image-Name, Beschreibung und Dateinamen zurück.|
|[/ Gesamtstruktur: {Yes | No}]|Gibt an, ob Informationen für die Gesamtstruktur oder in der lokalen Domäne zurückgegeben. Wenn ein Wert für diese Option nicht angegeben wird, ist das Standardverhalten, um die Server in der lokalen Domäne zurückzugeben.|

## <a name="BKMK_examples"></a>Beispiele für

Um Informationen zu allen Servern anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Get-AllServers /Show:Config
```
Um ausführliche Informationen zu allen Servern anzuzeigen, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)