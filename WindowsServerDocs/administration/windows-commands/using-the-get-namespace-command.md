---
title: Mithilfe des Befehls Get-Namespace
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: bd11880b6e733850b522c3a06152ac7ce7a28841
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889661"
---
# <a name="using-the-get-namespace-command"></a>Mithilfe des Befehls Get-Namespace

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu benutzerdefinierten Namespace.
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
|Parameter|Beschreibung|
|-------|--------|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces. Beachten Sie, dass dies nicht der Anzeigename, und muss eindeutig sein.<br /><br />-Bereitstellungsserver: Die Syntax für Namespacename ist /Namspace:WDS:<ImageGroup>/<ImageName>/<Index>. Zum Beispiel: **WDS:ImageGroup1/install.wim/1**<br />-Transport-Server: Dieser Wert sollte der Name für den Namespace bei der Erstellung auf dem Server übereinstimmen.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dies kann den NetBIOS-Namen oder den vollständig qualifizierten Domänennamen (FQDN) sein. Wenn kein Servername angegeben wird, wird der lokale Server verwendet.|
|[/ Anzeigen: Clients] oder [/ Details: Clients]|Zeigt Informationen zu Clientcomputern, die auf den angegebenen Namespace verbunden sind.|
## <a name="BKMK_examples"></a>Beispiele für
Um Informationen zum Namespace anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-Namespace /Namespace:"Custom Auto 1"
```
Zum Anzeigen von Informationen zu einem Namespace und den Clients, die verbunden sind, geben Sie eine der folgenden:
-   Windows Server 2008: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /Show:Clients`
-   Windows Server 2008 R2: `wdsutil /Get-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /details:Clients`
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllNamespaces](using-the-get-allnamespaces-command.md)
[mit dem neuen Namespace-Befehl](using-the-new-namespace-command.md)
[verwenden den Befehl Remove-Namespace](using-the-remove-namespace-command.md)
[Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
