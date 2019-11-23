---
title: Dfsdiag testdfsintegrity
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 173ee832-26e1-4ec8-a23a-38a7d6229ac3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f344e2d1fecc542efc39688f20165fd3e39a04a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378427"
---
# <a name="dfsdiag-testdfsintegrity"></a>Dfsdiag testdfsintegrity

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Integrität der verteiltes Dateisystem \(DFS-\) Namespace, indem die folgenden Tests durchgeführt werden:  
  
-   Sucht nach DFS-metadatenbeschädigungen  
  
-   Überprüft die Konfiguration der Access\-basierten Enumeration, um sicherzustellen, dass Sie zwischen den DFS-Metadaten und der Namespace-Server Freigabe konsistent ist.  
  
-   Erkennt überlappende DFS-Ordner \(Verknüpfungen\), doppelte Ordner und Ordner mit überlappenden Ordner Zielen.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/dfsroot:<DFS root path>|Der zu diagnostizieren DFS-Namespace.|  
|\/recurse|Führt die Tests einschließlich der Namespace-Interlinks aus.|  
|\/voll|überprüft die Konsistenz von Freigabe-und NTFS-ACLs und Client seitiger Konfiguration für alle Ordner Ziele. Außerdem wird überprüft, ob die Online-Eigenschaft festgelegt ist.|  
  
## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

