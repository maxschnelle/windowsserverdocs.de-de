---
title: Verwenden des Remove-Namespace-Befehls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b4c087442c43fd885fe4554cb29f9b2788420e05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362789"
---
# <a name="using-the-remove-namespace-command"></a>Verwenden des Remove-Namespace-Befehls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

entfernt einen benutzerdefinierten Namespace.
## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces an. Dies ist nicht der Anzeige Name, und er muss eindeutig sein.<br /><br />**Rollen Dienst "-   Bereitstellungs Server**": die Syntax für den Namespace Namen lautet/Namespace: WDS:<ImageGroup>/<ImageName>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server-Rollen Dienst**: dieser Wert muss dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Force|entfernt den Namespace sofort und beendet alle Clients. Beachten Sie, dass vorhandene Clients die Übertragung durchführen können, es sei denn, Sie geben **/Force**an. neue Clients können jedoch nicht beitreten.|
## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace zu beenden (aktuelle Clients können die Übertragung beenden, aber keine neuen Clients beitreten). Geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Namespace:"Custom Auto 1"
```
Wenn Sie die Beendigung aller Clients erzwingen möchten, geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /force
```
#### <a name="additional-references"></a>Weitere Verweise
Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls get-allnamespaces](using-the-get-allnamespaces-command.md)
[mit dem Befehl New-Namespace](using-the-new-namespace-command.md)
[Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
