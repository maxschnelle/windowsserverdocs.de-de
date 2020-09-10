---
title: Unterbefehl Start-Namespace
description: Referenz Artikel für den Unterbefehl Start-Namespace, der einen scheduled-Cast-Namespace startet.
ms.topic: reference
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9d37921024c1f92f97687c7b0a4a0714192fe564
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633924"
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
| /Namespace: <Namespace Name| Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-   **Bereitstellungs Server**: die Syntax für den Namespace Namen lautet/Namspace: WDS: <Image group> / <Image name> / <Index> . Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server**: dieser Name muss dem Namen entsprechen, der für den Namespace angegeben wurde, als er auf dem Server erstellt wurde. |
|   [/Server:<Server name>]   |                                                                                                           Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                           |

## <a name="examples"></a>Beispiele
Um einen Namespace zu starten, geben Sie einen der folgenden Informationen ein:
```
wdsutil /start-Namespace /Namespace:Custom Auto 1
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1
```
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-get-allnamespaces-command.md) 
 get-allnamespaces [Verwenden des New-Namespace-Befehls](using-the-new-namespace-command.md) 
 [Verwenden des Remove-Namespace-Befehls](using-the-remove-namespace-command.md)
