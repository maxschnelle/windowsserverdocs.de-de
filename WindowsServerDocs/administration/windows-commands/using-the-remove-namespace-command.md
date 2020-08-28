---
title: Remove-Namespace
description: Referenz Artikel für Remove-Namespace, mit dem ein benutzerdefinierter Namespace entfernt wird.
ms.topic: reference
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3bef563a91ed4eb445cdf3c555025873078d2716
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89023084"
---
# <a name="using-the-remove-namespace-command"></a>Verwenden des Remove-Namespace-Befehls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt einen benutzerdefinierten Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Namespace<Namespace name>|Gibt den Namen des Namespace an. Dies ist nicht der Anzeige Name, und er muss eindeutig sein.<p>-   **Rollen Dienst "Bereitstellungs Server**": die Syntax für den Namespace Namen lautet/Namespace: WDS: <ImageGroup> / <ImageName> / <Index> . Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server-Rollen Dienst**: dieser Wert muss dem Namen entsprechen, der für den Namespace angegeben wurde, als er auf dem Server erstellt wurde.|
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
## <a name="additional-references"></a>Weitere Verweise
- [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
 [Verwenden des Befehls](using-the-get-allnamespaces-command.md) 
 get-allnamespaces [Verwenden des New-Namespace-Befehls](using-the-new-namespace-command.md) 
 [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
