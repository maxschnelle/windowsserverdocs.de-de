---
title: Dfsdiag testdfsconfig
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 106aeeb9-ea79-4e6e-829c-eca06309bab2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8008e02d588edaa6fe7700a331c43f9680d89431
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378421"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag testdfsconfig

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration einer verteiltes Dateisystem \(DFS-\) Namespace, indem die folgenden Aktionen durchgeführt werden:  
  
-   überprüft, ob der DFS-Namespace-Dienst ausgeführt wird und ob der Starttyp auf allen Namespace Servern auf "automatisch" festgelegt ist.  
  
-   mit dieser Option wird überprüft, ob die Konfiguration der DFS-Registrierung zwischen den Namespace Servern konsistent ist.  
  
-   Überprüft die folgenden Abhängigkeiten auf gruppierten Namespace Servern, auf denen Windows Server 2008 oder höher ausgeführt wird:  
  
    -   Namespace-Stamm Ressourcenabhängigkeit von Netzwerknamen Ressource.  
  
    -   Netzwerknamen Ressourcenabhängigkeit von IP-Adress Ressource.  
  
    -   Namespace-Stamm Ressourcenabhängigkeit von physischer Datenträger Ressource.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
### <a name="parameters"></a>Parameter  
  
|       Parameter       |               Beschreibung               |
|-----------------------|-----------------------------------------|
| \/dfsroot:<namespace> | Der Namespace \(DFS-Stamm\) zur Diagnose. |
  
## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

