---
title: Unterbefehl Start-Namespace
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55fe4a6136fe4f8e886dc62fff746a1e5ff1898f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370749"
---
# <a name="subcommand-start-namespace"></a>Unterbefehl: Start-Namespace

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 startet einen geplanten Cast-Namespace.
> ## <a name="syntax"></a>Syntax
> ```
> wdsutil /start-Namespace /Namespace:<Namespace name> [/Server:<Server name>]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |          Parameter          |                                                                                                                                                                                             Beschreibung                                                                                                                                                                                             |
> |-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /Namespace:<Namespace name> | Gibt den Namen des Namespaces an. Beachten Sie, dass dies nicht der Anzeige Name ist und eindeutig sein muss.<br /><br />-   **Bereitstellungs Server**: die Syntax für den Namespace Namen lautet/Namspace: WDS:<Image group>/<Image name>/<Index>. Beispiel: **WDS: ImageGroup1/install. wim/1**<br />-   **Transport Server**: dieser Name muss dem Namen entsprechen, der dem Namespace bei der Erstellung auf dem Server zugewiesen wurde. |
> |   [/Server:<Server name>]   |                                                                                                           Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet.                                                                                                           |
> 
> ## <a name="BKMK_examples"></a>Beispiele
> Um einen Namespace zu starten, geben Sie einen der folgenden Informationen ein:
> ```
> wdsutil /start-Namespace /Namespace:"Custom Auto 1"
> wdsutil /start-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1"
> ```
> #### <a name="additional-references"></a>Weitere Verweise
> Der [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
> [mithilfe des Befehls "get-allnamespaces](using-the-get-allnamespaces-command.md) "
> [mithilfe des Befehls "New-Namespace](using-the-new-namespace-command.md) "
> [mit dem Befehl "Remove-Namespace](using-the-remove-namespace-command.md) " verwendet.
