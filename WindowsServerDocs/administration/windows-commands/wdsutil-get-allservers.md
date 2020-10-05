---
title: "\"Get-allservers\""
description: Referenz Artikel zu Get-allservers, der Informationen zu allen Windows-Bereitstellungsdiensteserver abruft.
ms.topic: reference
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b60fb7710699c4fff6656a0e2a34684a538b116d
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730293"
---
# <a name="get-allservers"></a>"Get-allservers"

Ruft Informationen zu allen Windows-Bereitstellungsdiensteserver ab.

> [!NOTE]
> Dieser Befehl kann eine längere Zeit in Anspruch nehmen, wenn in Ihrer Umgebung viele Windows-Bereitstellungsdiensteserver vorhanden sind oder wenn die Netzwerkverbindung, die die Server verknüpft, langsam ist.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                 BESCHREIBUNG                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show: {config |                                                                                                                    Bilder                                                                                                                    |
|  /Detailed  | Wenn Sie in Verbindung mit **/Show: Images** oder **/Show: all**verwendet wird, gibt alle Bild Metadaten aus jedem Bild zurück. Wenn die **/detailed** -Option nicht angegeben ist, besteht das Standardverhalten darin, den Image Namen, die Beschreibung und den Dateinamen zurückzugeben. |
| [/Forest: {Ja |                                                                                                                     Nein}]                                                                                                                     |

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu allen Servern anzuzeigen:
```
WDSUTIL /Get-AllServers /Show:Config
```
Wenn Sie ausführliche Informationen zu allen Servern anzeigen möchten, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)