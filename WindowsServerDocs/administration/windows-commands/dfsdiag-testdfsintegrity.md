---
title: Dfsdiag TestDFSIntegrity
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9a79e034f7c60be89266eb29dcd69e8f73b2aafe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837091"
---
# <a name="dfsdiag-testdfsintegrity"></a>Dfsdiag TestDFSIntegrity

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft die Integrität des verteilten Dateisystems \(DFS\) Namespace fest, indem Sie die folgenden Tests ausführen:  
  
-   Prüft auf DFS-mit den Tabellenmetadaten beschädigt oder Inkonsistenzen zwischen Domänencontrollern.  
  
-   Überprüft die Konfiguration der Zugriff\-basierend-Enumeration, um sicherzustellen, dass es DFS-Metadaten und die Namespace-Serverfreigabe konsistent ist.  
  
-   Überlappende DFS-Ordnern erkennt \(Links\), doppelte sowie Ordner mit sich überschneidenden Ordnerziele.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:<DFS root path> [/Recurse] [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/DFSRoot:<DFS root path>|Der DFS-Namespace zu diagnostizieren.|  
|\/Recurse|Führt die Tests, einschließlich, die der Namespace-interlinks.|  
|\/Vollständige|überprüft die Konsistenz der Freigabe- und NTFS-Acls und Client-Seite-Konfiguration auf alle Ordnerziele an. Es wird geprüft, die online-Eigenschaft festgelegt ist.|  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestDFSIntegrity /DFSRoot:\\Contoso.com\MyNamespace /Recurse /Full  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

