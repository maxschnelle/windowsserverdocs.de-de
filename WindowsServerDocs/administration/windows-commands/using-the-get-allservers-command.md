---
title: "\"Get-allservers\""
description: Referenz Thema zu Get-allservers, das Informationen zu allen Windows-Bereitstellungsdiensteserver abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b623b5e95e2a57147b7d9d191d42556191dd8e4d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719984"
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