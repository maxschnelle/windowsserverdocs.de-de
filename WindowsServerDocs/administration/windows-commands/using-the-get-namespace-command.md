---
title: Verwenden des Befehls Get-Namespace
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 607fb758db64cfc938a08b070b520fe2950aa482
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363081"
---
# <a name="using-the-get-namespace-command"></a>Verwenden des Befehls Get-Namespace

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
## <a name="parameters"></a>Parameter

|               Parameter               |                                                                                                                                                                                         Beschreibung                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      /Namespace:<Namespace name>      | Gibt den Namen des Namespaces an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<br /><br />-Bereitstellungs Server: die Syntax für den Namespace Namen lautet/Namspace: WDS:<ImageGroup>/<ImageName>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-Transport Server: dieser Wert sollte dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde. |
|        [/Server:<Server name>]        |                                                                                                             Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                              |
| [/Show: Clients] oder [/Details: Clients] |                                                                                                                                                  Hiermit werden Informationen zu Client Computern angezeigt, die mit dem angegebenen Namespace verbunden sind.                                                                                                                                                  |

## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einem Namespace anzuzeigen:
```
wdsutil /Get-Namespace /Namespace:"Custom Auto 1"
```
Zum Anzeigen von Informationen zu einem Namespace und den Clients, die verbunden sind, geben Sie eine der folgenden Informationen ein:
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /details:Clients`
  #### <a name="additional-references"></a>Weitere Verweise
  Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md) "
  [mithilfe des Befehls "New-Namespace](using-the-new-namespace-command.md) "
  [mithilfe des Remove-Namespace](using-the-remove-namespace-command.md) -Befehls
  [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
