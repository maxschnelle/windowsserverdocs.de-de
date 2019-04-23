---
title: 'AD-Gesamtstruktur-Wiederherstellung: Überprüfen Sie die Replikation'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: fb05586f281460dc2c7a1afea4c0423493e3fc46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878311"
---
# <a name="resources-to-verify-replication-is-working"></a>Ressourcen, um sicherzustellen, dass die Replikation funktioniert 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Wenn Sie wiederhergestellt oder erneut installiert alle Domänencontroller, können Sie überprüfen, dass AD DS und SYSVOL wiederhergestellt und repliziert richtig mit werden **Repadmin/replsum**, das auf eine beliebige Version von Windows Server ausführt.  
  
> [!TIP]
> Sie können auch herunterladen und Ausführen der [Status-Tool von Active Directory-Replikation](https://www.microsoft.com/download/details.aspx?id=30005) (ADReplStatus), ein kostenloses Tool, das Replikationsstatus der DCs und meldet Fehler überwacht. ADReplStatus erfordert .NET Framework 4 installiert werden, wenn es nicht bereits vorhanden ist.  

Überprüfen Sie die DFS-Replikation-Protokoll in der Ereignisanzeige für Ereignis-ID 4602 (oder File Replication Service 13516 Ereignis-ID) gibt an, dass die SYSVOL initialisiert wurde.  

Wenn die erste wiederhergestellt protokolliert DC-Ereignis-ID 4614 ("der Domänencontroller ist warten auf erste Replikation ausgeführt. Der replizierte Ordner bleibt in einem ersten Synchronisierungsstatus befindet, bis er mit seinem Partner repliziert wurde") in das Protokoll für die DFS-Replikation, 4602 der Ereignis-ID wird nicht angezeigt und müssen Sie zum Ausführen der folgenden manuellen Schritte zur Wiederherstellung von SYSVOL, wenn es vom repliziert wird DFSR:  

1. Wenn 4612 der DFSR-Ereignis auf dem ersten wiederhergestellten DC angezeigt wird, führen eine manuelle autorisierende Wiederherstellung wie in beschrieben [2218556: Gewusst wie: Erzwingen einer autorativen und nicht autorativen Synchronisierung für DFSR-repliziertes SYSVOL (wie "D4/D2" für FRS)](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556).  
2. Legen Sie **SysvolReady Flag** auf 1, wie in beschrieben, manuell [947022 der NETLOGON-Freigabe ist nicht vorhanden ist, nach der Installation von Active Directory Domain Services auf einem neuen vollständigen oder nur-Lese Windows Server 2008-basierten Domänencontroller ](https://support.microsoft.com/kb/947022).  

Sie können auch einen DFS-Replikation-Diagnosebericht erstellen. Weitere Informationen finden Sie unter [Erstellen eines Diagnoseberichts für die DFS-Replikation](https://technet.microsoft.com/library/cc754227.aspx) und [DFS-schrittweise Anleitung für Windows Server 2008](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx). Wenn der Server Windows Server 2008 R2 ausgeführt wird, können Sie [dfsrdiag.exe ReplicationState Befehlszeilenschalter](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx).  

Sie können auch den Replikationen-Test mit dcdiag.exe um zu prüfen, Replikationsfehler ausführen. Weitere Informationen finden Sie im Knowledge Base [Artikel 249256](https://support.microsoft.com/kb/249256).

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)
