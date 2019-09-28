---
title: Dfsdiag Testsites
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af72da64dd20d4b37824355a494cb8f97f597b28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378388"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag Testsites

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft die Konfiguration der Active Directory-Domänen Dienste \(ad DS @ no__t-1-Standorte, indem überprüft wird, ob Server, die als Namespace Server oder Ordner \(link @ no__t-3 fungieren, die gleichen Standort Zuordnungen auf allen Domänen Controllern aufweisen.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/machine: <server name>|Der Name des Servers, auf dem die Standort Zuordnung überprüft werden soll.|  
|\/dfspath: <namespace root or DFS folder>|Der Namespace Stamm oder verteiltes Dateisystem \(dfs @ no__t-1 Ordner \(link @ no__t-3 mit Zielen, für die die Standort Zuordnung überprüft werden soll.|  
|\/recurse|Listet die Site Zuordnungen für alle Ordner Ziele unter dem angegebenen Namespace Stamm auf und überprüft sie.|  
|\/full|überprüft, ob AD DS und die Registrierung des-Servers dieselben Standort Zuordnungs Informationen enthalten.|  
  
## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

