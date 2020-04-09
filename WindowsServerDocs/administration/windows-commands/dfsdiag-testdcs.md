---
title: Dfsdiag-testdcs
description: Windows-Befehls Thema für Dfsdiag testdcs, das die Konfiguration von Domänen Controllern in der angegebenen Domäne überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 092ce3710eb6d209f596683bd4ad054dadd11aa3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846316"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag-testdcs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration von Domänen Controllern, indem die folgenden Tests auf den einzelnen Domänen Controllern in der angegebenen Domäne durchgeführt werden:  
  
-   Überprüft, ob der verteiltes Dateisystem (DFS)-Namespace-Dienst ausgeführt wird und der Starttyp auf "automatisch" festgelegt ist.  
  
-   Hiermit wird die Unterstützung von für die Website costeten verweisen für "Netlogon" und "SYSVOL" überprüft.  
  
-   Überprüft die Konsistenz der Site Zuordnung nach Hostname und IP-Adresse.

## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|/Domain:`<domain_name>`|Die Domäne, die Sie überprüfen möchten.|  
  
## <a name="remarks"></a>Hinweise  

/Domain ist ein optionaler Parameter. Der Standardwert ist die lokale Domäne, mit der der lokale Host verknüpft ist.  
  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
Zum Überprüfen der Konfiguration von Domänen Controllern in der Domäne contoso.com geben Sie Folgendes ein:  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

