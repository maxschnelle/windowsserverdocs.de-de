---
title: Dfsdiag TestDFSConfig
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: affb3c879275228fa0ec17f77ad77db6fc44d6ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814771"
---
# <a name="dfsdiag-testdfsconfig"></a>Dfsdiag TestDFSConfig

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft die Konfiguration eines verteilten Dateisystems \(DFS\) Namespace fest, indem Sie die folgenden Aktionen ausführen:  
  
-   überprüft, ob der DFS-Namespace-Dienst ausgeführt wird und der Starttyp auf automatisch auf allen Namespaceservern festgelegt ist.  
  
-   überprüft, ob die Konfiguration der DFS-Registrierung von Namespaceserver ist.  
  
-   Überprüft die folgenden Abhängigkeiten auf gruppierten Namespaceserver, die WindowsServer 2008 oder höher ausgeführt werden:  
  
    -   Namespace der Stamm-adressabhängigkeit auf Netzwerk-Namensressource.  
  
    -   Network Name Ressource Abhängigkeit von IP-Adressressource.  
  
    -   Namespace der Stamm-adressabhängigkeit auf physikalischen Datenträgerressource.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:<namespace>  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/DFSRoot:<namespace>|Der Namespace \(DFS-Stamms\) zu diagnostizieren.|  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestDFSConfig /DFSRoot:\\Contoso.com\MyNamespace  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

