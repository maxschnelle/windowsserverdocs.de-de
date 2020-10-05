---
title: WDSUTIL get-allnamespaces
description: Referenz Artikel zu WDSUTIL get-allnamespaces, in dem Informationen zu allen Namespaces auf einem Server angezeigt werden.
ms.topic: reference
ms.assetid: e8fe896d-a69a-4180-923b-9f18185f5941
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ddad534e46c4ca30311ad497a9fa66d60a4cda60
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730290"
---
# <a name="wdsutil-get-allnamespaces"></a>WDSUTIL get-allnamespaces

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

|         Parameter         |                                                                               Windows Server 2008                                                                               | Windows Server 2008 R2 |
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
- Windows Server 2008
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /Show:Clients /ExcludedeletePending
  ```
- Windows Server 2008 R2
  ```
  wdsutil /Get-AllNamespaces /Server:MyWDSServer /ContentProvider:MyContentProv /details:Clients /ExcludedeletePending
  ```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [WDSUTIL New-Namespace-Befehl](wdsutil-new-namespace.md)
- [WDSUTIL Remove-Namespace-Befehl](wdsutil-remove-namespace.md)
- [Befehl "WDSUTIL Start-nmespace"](wdsutil-start-namespace.md)
