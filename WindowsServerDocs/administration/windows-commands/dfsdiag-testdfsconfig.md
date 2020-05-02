---
title: Dfsdiag testdfsconfig
description: Referenz Thema für Dfsdiag testdfsconfig, das die Konfiguration eines verteiltes Dateisystem-Namespace (DFS) prüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 057b0662fddb7148837be16380d190cdb37382c5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719589"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag testdfsconfig

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration eines verteiltes Dateisystem-Namespace (DFS), indem die folgenden Aktionen durchgeführt werden:  
  
-   Überprüft, ob der DFS-Namespace-Dienst ausgeführt wird und ob der Starttyp auf allen Namespace Servern auf "automatisch" festgelegt ist.  
  
-   Mit dieser Option wird überprüft, ob die Konfiguration der DFS-Registrierung zwischen den Namespace Servern konsistent ist.  
  
-   Überprüft die folgenden Abhängigkeiten auf gruppierten Namespace Servern, auf denen Windows Server 2008 oder höher ausgeführt wird:  
  
    -   Namespace-Stamm Ressourcenabhängigkeit von Netzwerknamen Ressource.  
  
    -   Netzwerknamen Ressourcenabhängigkeit von IP-Adress Ressource.  
  
    -   Namespace-Stamm Ressourcenabhängigkeit von physischer Datenträger Ressource.

## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
#### <a name="parameters"></a>Parameter  
  
|       Parameter       |               BESCHREIBUNG               |
|-----------------------|-----------------------------------------|
| /DFSRoot:`<namespace>` | Der zu diagnostizieren Namespace (DFS-Stamm). |
  
## <a name="examples"></a>Beispiele  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

