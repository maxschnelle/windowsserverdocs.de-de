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

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Überprüft verteiltes Dateisystem \(DFS-\) Verweise durch Ausführen der folgenden Tests:  
  
-   Wenn Sie den dfspath-Parameter ohne Argumente verwenden, überprüft dieser Befehl, ob die Verweis Liste alle vertrauenswürdigen Domänen enthält.  
  
-   Wenn Sie eine Domäne angeben, führt der Befehl eine Integritäts Überprüfung von Domänen Controllern \(Dfsdiag \/testdcs\) durch und testet die Standort Zuordnungen und den Domänen Cache des lokalen Hosts.  
  
-   Wenn Sie eine Domäne und \\SYSVOL oder \\Netlogon angeben und die gleichen Integritätsprüfungen wie bei der Angabe einer Domäne durchführen, prüft der Befehl, ob die Gültigkeitsdauer \(TTL\) der SYSVOL-oder Netlogon-Verweise mit dem Standardwert von 900 Sekunden übereinstimmt.  
  
-   Wenn Sie einen Namespace Stamm angeben und die gleichen Integritätsprüfungen wie bei der Angabe einer Domäne durchführen, führt der Befehl eine DFS-Konfigurations Überprüfung \(Dfsdiag \/testdfsconfig\) und eine Namespace Integritäts Überprüfung \(Dfsdiag \/testdfsintegrity-\)aus.  
  
-   Wenn Sie einen DFS-Ordner \(Link\)angeben und die gleichen Integritätsprüfungen wie bei der Angabe eines Namespace Stamms ausführen, wird durch den Befehl die Standort Konfiguration für die Ordner Ziele \(Dfsdiag \/Testsites\) überprüft und die Standort Zuordnung des lokalen Hosts überprüft.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|\/dfspath:<path for getting referrals>|Dieser DFS-Pfad kann eine der folgenden sein:<br /><br />-   \(leeres\): testet vertrauenswürdige Domänen.<br />-   \\\\Domäne: Domänen Controller Verweise.<br />-   \\\\Domänen\\SYSVOL: SYSVOL-Verweise.<br />-   \\\\Domäne\\Netlogon: Netlogon verweirals.<br />-   \\\\<Domain or server>\\<Namespace Root>: Namespace-Stamm Verweise.<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS-Ordner \(Verknüpfungen\) verweisen.|  
|\/voll|Wird nur auf Domänen-und Stamm Verweise angewendet. überprüft die Konsistenz der Standort Zuordnungs Informationen zwischen der Registrierung und den Active Directory-Domänen Diensten \(AD DS\).|  
  
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
  

