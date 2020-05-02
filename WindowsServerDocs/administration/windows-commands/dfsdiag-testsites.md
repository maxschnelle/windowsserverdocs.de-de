---
title: Dfsdiag Testsites
description: Referenz Thema für Dfsdiag Testsites, das die Konfiguration der Active Directory-Domänen Dienste-Standorte (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über die gleichen Standort Zuordnungen verfügen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68048699a812beac94fa121d6801da5f42e5393b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719555"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag Testsites

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit wird die Konfiguration der Active Directory-Domänen Dienste (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über dieselben Standort Zuordnungen verfügen.

## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|BESCHREIBUNG|  
|-------|--------|  
|\/Computer<server name>|Der Name des Servers, auf dem die Standort Zuordnung überprüft werden soll.|  
|\/Dfspath:<namespace root or DFS folder>|Der Namespace Stamm oder verteiltes Dateisystem Ordner (DFS) (Link) mit Zielen, für die die Standort Zuordnung überprüft werden soll.|  
|\/Recurse|Listet die Site Zuordnungen für alle Ordner Ziele unter dem angegebenen Namespace Stamm auf und überprüft sie.|  
|\/Vollständig|überprüft, ob AD DS und die Registrierung des-Servers dieselben Standort Zuordnungs Informationen enthalten.|  
  
## <a name="examples"></a>Beispiele  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
 
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

