---
title: Verwenden des Befehls Get-allservers
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8dd7f9917a54a80b3c570b07fe1a87bd3bcbe4d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363256"
---
# <a name="using-the-get-allservers-command"></a>Verwenden des Befehls Get-allservers



Ruft Informationen zu allen Windows-Bereitstellungsdiensteserver ab.

> [!NOTE]
> Dieser Befehl kann eine längere Zeit in Anspruch nehmen, wenn in Ihrer Umgebung viele Windows-Bereitstellungsdiensteserver vorhanden sind oder wenn die Netzwerkverbindung, die die Server verknüpft, langsam ist.

## <a name="syntax"></a>Syntax

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

## <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                 Beschreibung                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show: {config |                                                                                                                    Abbilder                                                                                                                    |
|  /Detailed  | Wenn Sie in Verbindung mit **/Show: Images** oder **/Show: all**verwendet wird, gibt alle Bild Metadaten aus jedem Bild zurück. Wenn die **/detailed** -Option nicht angegeben ist, besteht das Standardverhalten darin, den Image Namen, die Beschreibung und den Dateinamen zurückzugeben. |
| [/Forest: {Ja |                                                                                                                     Nein}]                                                                                                                     |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um Informationen zu allen Servern anzuzeigen:
```
WDSUTIL /Get-AllServers /Show:Config
```
Wenn Sie ausführliche Informationen zu allen Servern anzeigen möchten, geben Sie Folgendes ein:
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)