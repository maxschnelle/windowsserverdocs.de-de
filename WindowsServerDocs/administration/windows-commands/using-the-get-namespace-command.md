---
title: Get-Namespace
description: Referenz Thema für Get-Namespace, in dem Informationen zu einem benutzerdefinierten Namespace angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76980d2add9ee9b7584812c9d366408f8770b681
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719745"
---
# <a name="get-namespace"></a>Get-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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

|               Parameter               |                                                                                                                                                                                         BESCHREIBUNG                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Namespace<Namespace name>      | Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-Bereitstellungs Server: die Syntax für den Namespace Namen lautet/Namspace: WDS<ImageGroup>/<ImageName>/<Index>:. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-Transport Server: dieser Wert sollte dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde. |
|        [/Server:<Server name>]        |                                                                                                             Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                              |
| [/Show: Clients] oder [/Details: Clients] |                                                                                                                                                  Hiermit werden Informationen zu Client Computern angezeigt, die mit dem angegebenen Namespace verbunden sind.                                                                                                                                                  |

## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einem Namespace anzuzeigen:
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
Zum Anzeigen von Informationen zu einem Namespace und den Clients, die verbunden sind, geben Sie eine der folgenden Informationen ein:
- Windows Server 2008:`wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2:`wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md)
  " mit dem Befehl "[New-Namespace](using-the-new-namespace-command.md)
  " mit dem Befehl "[Remove-Namespace](using-the-remove-namespace-command.md)
  "[Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
