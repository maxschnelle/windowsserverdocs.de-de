---
title: get-allnamespaces
description: Referenz Artikel zu get-allnamespaces, in dem Informationen zu allen Namespaces auf einem Server angezeigt werden.
ms.topic: article
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 470aab904f9404b8dbe99409445b0533fa83fedd
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896392"
---
# <a name="get-allnamespaces"></a>get-allnamespaces

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu allen Namespaces auf einem Server an.

## <a name="syntax"></a>Syntax
Windows Server 2008:
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 R2
```
wdsutil /Get-AllNamespaces [/Server:<Server name>] [/ContentProvider:<name>] [/details:Clients] [/ExcludedeletePending]
```
### <a name="parameters"></a>Parameter

|         Parameter         |                                                                               WindowsServer 2008                                                                               | Windows Server 2008 R2 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|  [/Server:<Server name>]  | Gibt den Namen des Servers an. Hierbei kann es sich um den NetBIOS-Namen oder den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) handeln. Wenn kein Servername angegeben ist, wird der lokale Server verwendet. |                        |
| [/Contentprovider: <name> ] |                                                        Zeigt nur die Namespaces für den angegebenen Inhaltsanbieter an.                                                         |                        |
|      [/Show: Clients]      |                            Wird nur für Windows Server 2008 unterstützt. Hiermit werden Informationen zu Client Computern angezeigt, die mit dem-Namespace verbunden sind.                             |                        |
|    [/Details: Clients]     |                           Wird nur für Windows Server 2008 R2 unterstützt. Hiermit werden Informationen zu Client Computern angezeigt, die mit dem-Namespace verbunden sind.                           |                        |
|  [/ExcludedeletePending]  |                                                              Schließt alle deaktivierten Übertragungen aus der Liste aus.                                                              |                        |

## <a name="examples"></a>Beispiele
Wenn Sie alle Namespaces anzeigen möchten, geben Sie Folgendes ein:
```
wdsutil /Get-AllNamespaces
```
Wenn Sie alle Namespaces außer den deaktivierten anzeigen möchten, geben Sie Folgendes ein:
- WindowsServer 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
   [Verwenden des New-Namespace-Befehls](using-the-new-namespace-command.md) 
   [Verwenden des Remove-Namespace-Befehls](using-the-remove-namespace-command.md) 
   [Unterbefehl: Start-Namespace](subcommand-start-namespace.md)
