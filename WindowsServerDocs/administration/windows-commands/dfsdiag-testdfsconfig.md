---
title: Dfsdiag testdfsconfig
description: Windows-Befehls Thema für Dfsdiag testdfsconfig, das die Konfiguration eines verteiltes Dateisystem-Namespace (DFS) überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffb75ba26b4ed90dbf5c8bfda80f4a81f986e46a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846333"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag testdfsconfig

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

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
  
|       Parameter       |               Beschreibung               |
|-----------------------|-----------------------------------------|
| /DFSRoot:`<namespace>` | Der zu diagnostizieren Namespace (DFS-Stamm). |
  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

