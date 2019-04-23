---
title: Verwenden den Befehl Remove-Namespace
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 115c0a90a60e18ee4b89758200773d1dfec2163f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842041"
---
# <a name="using-the-remove-namespace-command"></a>Verwenden den Befehl Remove-Namespace

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Entfernt einen benutzerdefinierten Namespace an.
## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces. Dies ist nicht den Anzeigenamen, und muss eindeutig sein.<br /><br />-   **Deployment Server-Rollendienst**: Die Syntax für Namespacename ist /Namespace:WDS:<ImageGroup>/<ImageName>/<Index>. Zum Beispiel: **WDS:ImageGroup1/install.wim/1**<br />-   **Transport-Server-Rollendienst**: Dieser Wert muss der Name für den Namespace bei der Erstellung auf dem Server übereinstimmen.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|[/force]|Entfernt den Namespace sofort, und alle Clients beendet. Beachten Sie, dass es sei denn, Sie geben **/force**, vorhandene Clients können die Übertragung abgeschlossen, aber neue Clients sind nicht beitreten.|
## <a name="BKMK_examples"></a>Beispiele für
So beenden Sie einen Namespace (aktuelle Clients können die Übertragung abgeschlossen, aber neue Clients sind nicht beitreten), Typ:
```
wdsutil /remove-Namespace /Namespace:"Custom Auto 1"
```
Um die Beendigung aller Clients zu erzwingen, geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /force
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllNamespaces](using-the-get-allnamespaces-command.md)
[mit dem neuen Namespace-Befehl](using-the-new-namespace-command.md) 
 [ Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
