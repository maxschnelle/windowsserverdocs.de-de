---
title: Mithilfe des Befehls Get-AllNamespaces
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b77bb80238ee63cc0d71d88592d75850720e33b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440522"
---
# <a name="using-the-get-allnamespaces-command"></a>Mithilfe des Befehls Get-AllNamespaces

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen über alle Namespaces auf einem Server an.
## <a name="syntax"></a>Syntax
Windows Server 2008:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
## <a name="parameters"></a>Parameter

|         Parameter         |                                                                               WindowsServer 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/Server:<Server name>]  | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben wird, wird der lokale Server verwendet werden. |                        |
| [/ContentProvider:<name>] |                                                        Enthält die Namespaces für den angegebenen Inhaltsanbieter.                                                         |                        |
|      [/Show:Clients]      |                            Nur unterstützt für Windows Server 2008. Zeigt Informationen zu Clientcomputern, die auf den Namespace verbunden sind.                             |                        |
|    [/details:Clients]     |                           Nur unterstützt für Windows Server 2008 R2. Zeigt Informationen zu Clientcomputern, die auf den Namespace verbunden sind.                           |                        |
|  [/ExcludedeletePending]  |                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                              |                        |

## <a name="BKMK_examples"></a>Beispiele für
Um alle Namespaces anzuzeigen, geben Sie Folgendes ein:
```
wdsutil /Get-AllNamespaces
```
Um alle Namespaces außer diejenigen anzuzeigen, die deaktiviert sind, geben Sie Folgendes ein:
- WindowsServer 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:"MyContentProv" /details:Clients /ExcludedeletePending
  ```
  #### <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [mit dem neuen Namespace-Befehl](using-the-new-namespace-command.md)
  [mit dem Befehl Remove-Namespace](using-the-remove-namespace-command.md) 
   [ Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
