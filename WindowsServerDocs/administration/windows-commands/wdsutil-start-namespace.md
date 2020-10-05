---
title: WDSUTIL Start-Namespace
description: Referenz Artikel für den Unterbefehl Start-Namespace, der einen scheduled-Cast-Namespace startet.
ms.topic: reference
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7463b062bf3322d6cf4f9c481effde825cb2979a
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730541"
---
# <a name="wdsutil-start-namespace"></a>WDSUTIL Start-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Startet einen geplanten Cast-Namespace.

## <a name="syntax"></a>Syntax
```
wdsutil /start-Namespace /Namespace:<Namespace name[/Server:<Server name>]
```
### <a name="parameters"></a>Parameter

|          Parameter          |                                                                                                                                                                                             BESCHREIBUNG                                                                                                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Namespace: <Namespace Name| Gibt den Namen des Namespace an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<p>-   **Bereitstellungs Server**: die Syntax für den Namespace Namen lautet/Namspace: WDS: <Image group> / <Image name> / <Index> . Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server**: dieser Name muss dem Namen entsprechen, der für den Namespace angegeben wurde, als er auf dem Server erstellt wurde. |
|   [/Server:<Server name>]   |                                                                                                           Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                           |

## <a name="examples"></a>Beispiele
Um einen Namespace zu starten, geben Sie einen der folgenden Informationen ein:
```
wdsutil /start-Namespace /Namespace:Custom Auto 1
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL-Befehl "get-allnamespaces"](wdsutil-get-allnamespaces.md)
- [WDSUTIL New-Namespace-Befehl](wdsutil-new-namespace.md)
- [WDSUTIL Remove-Namespace-Befehl](wdsutil-remove-namespace.md)
