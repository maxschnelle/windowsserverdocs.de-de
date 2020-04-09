---
title: Remove-Namespace
description: Windows-Befehls Thema für Remove-Namespace, wodurch ein benutzerdefinierter Namespace entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f8b830a5d99d13ed00a3a19f2cf246ad71d1c5f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830233"
---
# <a name="using-the-remove-namespace-command"></a>Verwenden des Remove-Namespace-Befehls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt einen benutzerdefinierten Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces an. Dies ist nicht der Anzeige Name, und er muss eindeutig sein.<p>**Rollen Dienst "-   Bereitstellungs Server**": die Syntax für den Namespace Namen lautet/Namespace: WDS:<ImageGroup>/<ImageName>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server-Rollen Dienst**: dieser Wert muss dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Force|entfernt den Namespace sofort und beendet alle Clients. Beachten Sie, dass vorhandene Clients die Übertragung durchführen können, es sei denn, Sie geben **/Force**an. neue Clients können jedoch nicht beitreten.|
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace zu beenden (aktuelle Clients können die Übertragung beenden, aber keine neuen Clients beitreten). Geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Namespace:Custom Auto 1
```
Wenn Sie die Beendigung aller Clients erzwingen möchten, geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /force
```
## <a name="additional-references"></a>Weitere Verweise
- Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls get-allnamespaces](using-the-get-allnamespaces-command.md)
[mit dem Befehl New-Namespace](using-the-new-namespace-command.md)
[Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
