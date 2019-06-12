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
ms.openlocfilehash: dbccb834f9058f2c3cca097cdf998455f2a6892e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440495"
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

|   Parameter   |                                                                                                                 Beschreibung                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show:{Config |                                                                                                                    Abbilder                                                                                                                    |
|  [/Detailed]  | Bei Verwendung in Verbindung mit der **/Show:Images** oder **/Show:All**, gibt alle Metadaten aus jedem Bild image. Wenn die **/detaillierte** Option nicht angegeben wird, ist das Standardverhalten der Image-Name, Beschreibung und Dateinamen zurück. |
| [/ Gesamtstruktur: {Yes |                                                                                                                     No}]                                                                                                                     |

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

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)