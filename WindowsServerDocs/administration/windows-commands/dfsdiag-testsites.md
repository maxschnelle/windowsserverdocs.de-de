---
title: Dfsdiag Testsites
description: Windows-Befehls Thema für Dfsdiag Testsites, das die Konfiguration von Active Directory-Domänen Diensten (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über die gleichen Standort Zuordnungen verfügen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80cc9095748dafb030b204130bfa2ccb61ec69ea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846223"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag Testsites

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Hiermit wird die Konfiguration der Active Directory-Domänen Dienste (AD DS) überprüft, indem überprüft wird, ob Server, die als Namespace Server oder Ordner (Verknüpfungs Ziele) fungieren, auf allen Domänen Controllern über dieselben Standort Zuordnungen verfügen.

## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/Computer:<server name>|Der Name des Servers, auf dem die Standort Zuordnung überprüft werden soll.|  
|\/dfspath:<namespace root or DFS folder>|Der Namespace Stamm oder verteiltes Dateisystem Ordner (DFS) (Link) mit Zielen, für die die Standort Zuordnung überprüft werden soll.|  
|\/recurse|Listet die Site Zuordnungen für alle Ordner Ziele unter dem angegebenen Namespace Stamm auf und überprüft sie.|  
|\/voll|überprüft, ob AD DS und die Registrierung des-Servers dieselben Standort Zuordnungs Informationen enthalten.|  
  
## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
 
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
-   [Dfsdiag](dfsdiag.md)  
  

