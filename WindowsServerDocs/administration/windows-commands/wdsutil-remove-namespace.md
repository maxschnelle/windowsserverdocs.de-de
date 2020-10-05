---
title: WDSUTIL Remove-Namespace
description: Referenz Artikel für "Remove-Namespace" von WDSUTIL, mit dem ein benutzerdefinierter Namespace entfernt wird.
ms.topic: reference
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bc5d44b727bf93bf6630f7289833640397e69dae
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730535"
---
# <a name="wdsutil-remove-namespace"></a>WDSUTIL Remove-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt einen benutzerdefinierten Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>Parameter
|Parameter|BESCHREIBUNG|
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
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "get-allnamespaces"](wdsutil-get-allnamespaces.md)
- [WDSUTIL New-Namespace-Befehl](wdsutil-new-namespace.md)
- [WDSUTIL-Befehl "Start-Namespace"](wdsutil-start-namespace.md)
