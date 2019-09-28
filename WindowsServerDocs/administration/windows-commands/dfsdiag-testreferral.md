---
title: Dfsdiag testreferral
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: af22520d2c89f9d9f9d91ea6f43a33f3ff9c57f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378360"
---
# <a name="dfsdiag-testreferral"></a>Dfsdiag testreferral

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Prüft verteiltes Dateisystem \(dfs @ no__t-1-Verweise durch Ausführen der folgenden Tests:  
  
-   Wenn Sie den dfspath-Parameter ohne Argumente verwenden, überprüft dieser Befehl, ob die Verweis Liste alle vertrauenswürdigen Domänen enthält.  
  
-   Wenn Sie eine Domäne angeben, führt der Befehl eine Integritäts Überprüfung der Domänen Controller \(dfsdiag \/testdcs @ no__t-2 aus und testet die Site Zuordnungen und den Domänen Cache des lokalen Hosts.  
  
-   Wenn Sie eine Domäne und \\sysvol oder \\netlogon angeben und die gleichen Integritätsprüfungen wie bei der Angabe einer Domäne durchführen, prüft der Befehl, dass die Gültigkeitsdauer \(ttl @ no__t-3 von SYSVOL-oder Netlogon-Referenzen mit dem Standardwert von übereinstimmt. 900 Sekunden.  
  
-   Wenn Sie einen Namespace Stamm angeben und die gleichen Integritätsprüfungen wie bei der Angabe einer Domäne durchführen, führt der Befehl eine DFS-Konfigurations Überprüfung \(dfsdiag \/testdfsconfig @ no__t-2 und eine Namespace Integritäts Überprüfung \(dfsdiag aus @no__ t-4testdfsintegrity @ no__t-5.  
  
-   Wenn Sie einen DFS-Ordner \(link @ no__t-1 angeben und die gleichen Integritätsprüfungen wie bei der Angabe eines Namespace Stamms ausführen, überprüft der Befehl die Standort Konfiguration für die Ordner Ziele \(dfsdiag \/testsites @ no__t-4 und überprüft. die Site Zuordnung des lokalen Hosts.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/dfspath: <path for getting referrals>|Dieser DFS-Pfad kann eine der folgenden sein:<br /><br />-    @ no__t-1blank @ no__t-2: Testet vertrauenswürdige Domänen.<br />-    @ no__t-1 @ no__t-2domain: Verweise auf Domänen Controller.<br />-    @ no__t-1 @ no__t-2domain @ no__t-3sysvol: SYSVOL-Verweise.<br />-    @ no__t-1 @ no__t-2domain @ no__t-3netlogon: Anmelde Verweise.<br />-    @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5: Namespace-Stamm Verweise.<br />-    @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7: DFS-Ordner \(link @ no__t-1 referenrals.|  
|\/full|Wird nur auf Domänen-und Stamm Verweise angewendet. überprüft die Konsistenz der Standort Zuordnungs Informationen zwischen der Registrierung und den Active Directory-Domänen Diensten \(ad DS @ no__t-1.|  
  
## <a name="BKMK_Examples"></a>Beispiele  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace  
```  
  
Geben Sie in TBD Folgendes ein:  
  
```  
dfsdiag /TestReferral /DFSpath:  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

