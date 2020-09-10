---
title: Get-Namespace
description: Referenz Artikel zu Get-Namespace, in dem Informationen zu einem benutzerdefinierten Namespace angezeigt werden.
ms.topic: reference
ms.assetid: ea641bab-e97b-4909-918e-447730027dc1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2ebbabfea1dee0b3d7265bf4977ad93dd5ff47c0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640590"
---
# <a name="get-namespace"></a>Get-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu einem benutzerdefinierten Namespace an.

## <a name="syntax"></a>Syntax
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/Show:Clients]
```
Windows Server 2008 R2
```
wdsutil /Get-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/details:Clients]
```
### <a name="parameters"></a>Parameter

|               Parameter               |                                                                                                                                                                                         BESCHREIBUNG                                                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Namespace<Namespace name>      | Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-Bereitstellungs Server: die Syntax für den Namespace Namen lautet/Namspace: WDS: <ImageGroup> / <ImageName> / <Index> . Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-Transport Server: dieser Wert sollte dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde. |
|        [/Server:<Server name>]        |                                                                                                             Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                              |
| [/Show: Clients] oder [/Details: Clients] |                                                                                                                                                  Hiermit werden Informationen zu Client Computern angezeigt, die mit dem angegebenen Namespace verbunden sind.                                                                                                                                                  |

## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um Informationen zu einem Namespace anzuzeigen:
```
wdsutil /Get-Namespace /Namespace:Custom Auto 1
```
Zum Anzeigen von Informationen zu einem Namespace und den Clients, die verbunden sind, geben Sie eine der folgenden Informationen ein:
- Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /Show:Clients`
- Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /details:Clients`
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Verwenden des Befehls](using-the-get-allnamespaces-command.md) 
   get-allnamespaces [Verwenden des New-Namespace-Befehls](using-the-new-namespace-command.md) 
   [Verwenden des Remove-Namespace-Befehls](using-the-remove-namespace-command.md) 
   [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
