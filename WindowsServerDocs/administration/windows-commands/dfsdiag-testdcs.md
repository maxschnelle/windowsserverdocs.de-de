---
title: Dfsdiag-testdcs
description: Referenz Thema für Dfsdiag testdcs, das die Konfiguration von Domänen Controllern in der angegebenen Domäne überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ac7fe1a7bae6a7b3dab9004b6212b7d93774ade
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719596"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag-testdcs

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration von Domänen Controllern, indem die folgenden Tests auf den einzelnen Domänen Controllern in der angegebenen Domäne durchgeführt werden:  
  
-   Überprüft, ob der verteiltes Dateisystem (DFS)-Namespace-Dienst ausgeführt wird und der Starttyp auf "automatisch" festgelegt ist.  
  
-   Hiermit wird die Unterstützung von für die Website costeten verweisen für "Netlogon" und "SYSVOL" überprüft.  
  
-   Überprüft die Konsistenz der Site Zuordnung nach Hostname und IP-Adresse.

## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|-`<domain_name>`|Die Domäne, die Sie überprüfen möchten.|  
  
## <a name="remarks"></a>Bemerkungen  

/Domain ist ein optionaler Parameter. Der Standardwert ist die lokale Domäne, mit der der lokale Host verknüpft ist.  
  
## <a name="examples"></a>Beispiele  
Zum Überprüfen der Konfiguration von Domänen Controllern in der Domäne contoso.com geben Sie Folgendes ein:  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

