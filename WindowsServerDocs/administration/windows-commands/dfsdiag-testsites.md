---
title: Dfsdiag TestSites
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6486c79cfa58bb262fd3161ad0801e84185b6629
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873971"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag TestSites

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft die Konfiguration der active Directory Domain Services \(AD DS\) Websites, indem Sie überprüfen, die als Namespaceserver oder den Ordner fungieren Servers \(Link\) Ziele haben die gleichen standortzuordnungen für alle in der Domäne Controller.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/Computer:<server name>|Der Name des Servers, auf dem die sitezuordnung zu überprüfen.|  
|\/DFSpath:<namespace root or DFS folder>|Den Namespacestamm oder DFS- \(DFS\) Ordner \(Link\) mit Zielen, die für das die sitezuordnung überprüft.|  
|\/Recurse|Listet auf und überprüft die Website-Zuordnungen für alle Ordnerziele, unter dem angegebenen Namespace-Stammverzeichnis.|  
|\/Vollständige|Stellt sicher, dass AD DS und der Registrierung des Servers die gleiche Zuordnungsinformationen enthalten.|  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

