---
title: Remove-Namespace
description: Referenz Thema für Remove-Namespace, mit dem ein benutzerdefinierter Namespace entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ef329a53a7f212c1810af2e4ced11a2abf76840
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720326"
---
# <a name="using-the-remove-namespace-command"></a>Verwenden des Remove-Namespace-Befehls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt einen benutzerdefinierten Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
|-------|--------|
|Namespace<Namespace name>|Gibt den Namen des Namespace an. Dies ist nicht der Anzeige Name, und er muss eindeutig sein.<p>-   **Rollen Dienst "Bereitstellungs Server**": die Syntax für den Namespace Namen lautet/Namespace<ImageGroup>/<ImageName>/<Index>: WDS:. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server-Rollen Dienst**: dieser Wert muss dem Namen entsprechen, der für den Namespace angegeben wurde, als er auf dem Server erstellt wurde.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Dabei kann es sich um den NetBIOS-Namen oder den voll qualifizierten Domänen Namen (FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.|
|/Force|entfernt den Namespace sofort und beendet alle Clients. Beachten Sie, dass vorhandene Clients die Übertragung durchführen können, es sei denn, Sie geben **/Force**an. neue Clients können jedoch nicht beitreten.|
## <a name="examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Namespace zu beenden (aktuelle Clients können die Übertragung beenden, aber keine neuen Clients beitreten). Geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Namespace:Custom Auto 1
```
Wenn Sie die Beendigung aller Clients erzwingen möchten, geben Sie Folgendes ein:
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /force
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md)
"[mit dem Befehl "New-Namespace Command](using-the-new-namespace-command.md)
"[: Start-Namespace](subcommand-start-namespace.md)
