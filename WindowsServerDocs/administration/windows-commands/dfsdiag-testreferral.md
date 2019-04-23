---
title: Dfsdiag TestReferral
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd1b87befa8a9cfda5ea27a4ce5a5105ea1a1009
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848021"
---
# <a name="dfsdiag-testreferral"></a>Dfsdiag TestReferral

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Überprüft, Distributed File System \(DFS\) verweisen, indem Sie die folgenden Tests ausführen:  
  
-   Wenn Sie den Parameter DFSpath ohne Argumente verwenden, mit diesem Befehl wird überprüft, ob die Liste der Verweise auf alle vertrauenswürdige Domänen umfasst.  
  
-   Wenn Sie eine Domäne angeben, führt der Befehl eine Überprüfung der Integrität von Domänencontrollern \(Dfsdiag \/Testdcs\) und testet den standortzuordnungen und Domänencache des lokalen Hosts.  
  
-   Wenn Sie eine Domäne angeben und \\SYSvol oder \\NETLOGON, zusätzlich zum Ausführen der gleichen Integritäts überprüft werden, als wenn Sie eine Domäne angeben, der Befehl, der die Time To Live, Gültigkeitsdauer überprüft \(Gültigkeitsdauer (TTL)\) SYSVOL- und NETLOGON-Weiterleitungen entspricht den Standardwert von 900 Sekunden.  
  
-   Wenn Sie einen Namespacestamm, zusätzlich zum Ausführen der gleichen Integritäts angeben, überprüft der Befehl eine Überprüfung der DFS-Konfiguration ausführt, wenn Sie eine Domäne angeben, \(Dfsdiag \/TestDFSConfig\) und einen Namespace-integritätsprüfung \(Dfsdiag \/TestDFSIntegrity\).  
  
-   Wenn Sie einen DFS-Ordner angeben \(Link\), zusätzlich zum Ausführen der gleichen integritätsprüfungen während der Befehl die Standortkonfiguration für Ordnerziele, wenn Sie einen Namespacestamm angeben überprüft, \(Dfsdiag \/ Testsites\) und überprüft die Zuordnung der Standort des lokalen Hosts.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/DFSpath:<path for getting referrals>|Dieser Pfad für die DFS-kann es sich um eine der folgenden sein:<br /><br />-   \(blank\): Tests vertrauenswürdigen Domänen.<br />-   \\\\Domäne: Domain-Controller-Weiterleitungen.<br />-   \\\\Domain\\SYSvol: SYSvol-Verweise.<br />-   \\\\Domain\\NETLOGON: NETLOGON-Verweise.<br />-   \\\\<Domain or server>\\<Namespace Root>: Namespace-stammweiterleitungen.<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS-Ordner \(Link\) Verweise.|  
|\/Vollständige|Nur auf die Domäne und zu den Root-Verweisen angewendet wird. überprüft die Konsistenz von Standortinformationen über die Zuordnung zwischen der Registrierung und die active Directory-Domänendienste \(AD DS\).|  
  
## <a name="BKMK_Examples"></a>Beispiele für  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace  
```  
  
Geben Sie um noch festzulegen ein:  
  
```  
dfsdiag /TestReferral /DFSpath:  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
  

