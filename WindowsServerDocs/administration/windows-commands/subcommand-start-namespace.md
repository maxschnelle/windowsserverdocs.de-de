---
title: Unterbefehl Start-Namespace
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5dc484a3b159cd510d7a61484f4f46b1f1db7a4e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877131"
---
# <a name="subcommand-start-namespace"></a>Unterbefehl: Start-Namespace

>Gilt für: Windows Server (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 startet einen geplanten Cast-Namespace.
## <a name="syntax"></a>Syntax
```
wdsutil /start-Namespace /Namespace:<Namespace name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/Namespace:<Namespace name>|Gibt den Namen des Namespaces. Beachten Sie, dass dies nicht der Anzeigename, und muss eindeutig sein.<br /><br />-   **Bereitstellungsserver**: Die Syntax für Namespacename ist /Namspace:WDS:<Image group>/<Image name>/<Index>. Zum Beispiel: **WDS:ImageGroup1/install.wim/1**<br />-   **Transport-Server**: Dieser Name muss der Name für den Namespace bei der Erstellung auf dem Server übereinstimmen.|
|[/Server:<Server name>]|Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden.|
## <a name="BKMK_examples"></a>Beispiele für
Geben Sie eine der folgenden Schritte aus, um einen Namespace zu starten:
```
wdsutil /start-Namespace /Namespace:"Custom Auto 1"
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1"
```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[mit dem Befehl Get-AllNamespaces](using-the-get-allnamespaces-command.md)
[mit dem neuen Namespace-Befehl](using-the-new-namespace-command.md)
[verwenden den Befehl Remove-Namespace](using-the-remove-namespace-command.md)
