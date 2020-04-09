---
title: Get-Namespace
description: Windows-Befehls Thema für Get-Namespace, in dem Informationen zu einem benutzerdefinierten Namespace angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 58e84ec5c82ea3c2663b38bd2e53f65f2cf47519
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830883"
---
# <a name="get-namespace"></a>Get-Namespace

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem benutzerdefinierten Namespace an.

## <a name="syntax"></a>Syntax
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/Show:Clients]
```
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/details:Clients]
```
### <a name="parameters"></a>Parameter

|               Parameter               |                                                                                                                                                                                         Beschreibung                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Namespace:<Namespace name>      | Gibt den Namen des Namespaces an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-Bereitstellungs Server: die Syntax für den Namespace Namen lautet/Namspace: WDS:<ImageGroup>/<ImageName>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-Transport Server: dieser Wert sollte dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde. |
|        [/Server:<Server name>]        |                                                                                                             Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                              |
| [/Show: Clients] oder [/Details: Clients] |                                                                                                                                                  Hiermit werden Informationen zu Client Computern angezeigt, die mit dem angegebenen Namespace verbunden sind.                                                                                                                                                  |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einem Namespace anzuzeigen:
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
Zum Anzeigen von Informationen zu einem Namespace und den Clients, die verbunden sind, geben Sie eine der folgenden Informationen ein:
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`
  ## <a name="additional-references"></a>Weitere Verweise
  - Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md) "
  [mithilfe des Befehls "New-Namespace](using-the-new-namespace-command.md) "
  [mithilfe des Remove-Namespace](using-the-remove-namespace-command.md) -Befehls
  [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
