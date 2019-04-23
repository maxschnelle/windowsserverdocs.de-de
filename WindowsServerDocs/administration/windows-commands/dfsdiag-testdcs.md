---
title: Dfsdiag TestDCs
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 62956ae65d2311939ac0db6a4b86950f21dba407
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836601"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag TestDCs

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft die Konfiguration der Domänencontroller anhand der folgenden Tests auf jedem Domänencontroller in der angegebenen Domäne:  
  
-   überprüft, ob das Distributed File System \(DFS\) Namespace-Dienst ausgeführt wird und, die der Starttyp auf automatisch gesetzt ist.  
  
-   Überprüft, ob die Unterstützung des Standorts\-mit Kosten Verweise für Netlogon- und SYSvol.  
  
-   überprüft die Konsistenz der sitezuordnung von Hostnamen und IP-Adresse an.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/Domäne:<Domain name>|Domäne, die Sie überprüfen möchten.|  
  
## <a name="remarks"></a>Hinweise  
\/Domäne ist ein optionaler Parameter. Der Standardwert ist die lokale Domäne, der mit der lokale Host verknüpft ist.  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie Folgendes ein, um die Konfiguration von Domänencontrollern in der Domäne "contoso.com" zu überprüfen:  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

