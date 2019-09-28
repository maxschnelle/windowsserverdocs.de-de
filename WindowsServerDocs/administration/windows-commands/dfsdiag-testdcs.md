---
title: Dfsdiag-testdcs
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a193e68b6f015b1535a98e20b52deb2a4a14034c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378438"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag-testdcs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration von Domänen Controllern, indem die folgenden Tests auf den einzelnen Domänen Controllern in der angegebenen Domäne durchgeführt werden:  
  
-   überprüft, ob die verteiltes Dateisystem \(dfs @ no__t-1-Namespace Dienst ausgeführt wird und ob der Starttyp auf "automatisch" festgelegt ist.  
  
-   Hiermit wird die Unterstützung von "Site @ no__t-0costed Verweise" für "Netlogon" und "SYSVOL" überprüft.  
  
-   überprüft die Konsistenz der Site Zuordnung nach Hostname und IP-Adresse.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/domäne: <Domain name>|Die Domäne, die Sie überprüfen möchten.|  
  
## <a name="remarks"></a>Hinweise  
\/domäne ist ein optionaler Parameter. Der Standardwert ist die lokale Domäne, mit der der lokale Host verknüpft ist.  
  
## <a name="BKMK_Examples"></a>Beispiele  
Zum Überprüfen der Konfiguration von Domänen Controllern in der Domäne contoso.com geben Sie Folgendes ein:  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

