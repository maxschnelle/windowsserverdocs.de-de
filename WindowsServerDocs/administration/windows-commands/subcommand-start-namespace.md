---
title: Unterbefehl Start-Namespace
description: Referenz Thema für den Unterbefehl "Start-Namespace", der einen scheduled-Cast-Namespace startet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1562fcb6c61533fcc9994e9011bf7d61154c06f7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721660"
---
# <a name="subcommand-start-namespace"></a>Unterbefehl: Start-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet einen geplanten Cast-Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /start-Namespace /Namespace:<Namespace name[/Server:<Server name>]
```
### <a name="parameters"></a>Parameter

|          Parameter          |                                                                                                                                                                                             BESCHREIBUNG                                                                                                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Namespace: <Namespace Name| Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-   **Bereitstellungs Server**: die Syntax für den Namespace Namen lautet/Namspace: WDS:<Image group>/<Image name>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server**: dieser Name muss dem Namen entsprechen, der für den Namespace angegeben wurde, als er auf dem Server erstellt wurde. |
|   [/Server:<Server name>]   |                                                                                                           Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                           |

## <a name="examples"></a>Beispiele
Um einen Namespace zu starten, geben Sie einen der folgenden Informationen ein:
```
wdsutil /start-Namespace /Namespace:Custom Auto 1
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md)
" mit dem Befehl "[New-Namespace](using-the-new-namespace-command.md)
" mit dem Befehl "[Remove-Namespace](using-the-remove-namespace-command.md) "
