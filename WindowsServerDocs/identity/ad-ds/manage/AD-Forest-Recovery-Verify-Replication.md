---
title: "AD-Gesamtstruktur-Wiederherstellung – überprüfen Sie die Replikation"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adfs
ms.openlocfilehash: d85336a10e808755677a99777af8ecf5c07b05ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="resources-to-verify-replication-is-working"></a>Ressourcen, um sicherzustellen, dass die Replikation funktioniert 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
 Nachdem Sie alle Domänencontroller neu installiert oder wiederhergestellt haben, können Sie sicherstellen, dass AD DS und SYSVOL wiederhergestellt und die Replikation ordnungsgemäß mithilfe sind **Repadmin/replsum**, der unter einer beliebigen Version von Windows Server ausgeführt wird.  
  
> [!TIP]
>  Sie können auch herunterladen und Ausführen der [Status-Tool von Active Directory-Replikation](https://www.microsoft.com/download/details.aspx?id=30005) (ADReplStatus), ein kostenloses Tool, das Replikationsstatus Fehler DCs und Berichte überwacht. ADReplStatus erfordert .NET Framework 4 installiert werden, wenn er nicht bereits vorhanden ist.  
  
 Überprüfen Sie das Ereignisprotokoll der DFS-Replikation in der Ereignisanzeige nach Ereignis-ID 4602 (oder File Replication Service-Ereignis-ID 13516) gibt an, dass die SYSVOL initialisiert wurde.  
  
 Wenn die erste wiederhergestellt protokolliert DC-Ereignis-ID 4614 ("der Domänencontroller wartet auf die erste Replikation auszuführen. Der replizierte Ordner in einem ersten Synchronisierungsstatus bleibt, bis er mit seinem Partner repliziert wurde") in das Protokoll von DFS-Replikation, klicken Sie dann Ereignis-ID 4602 wird nicht angezeigt und müssen Sie die folgenden Schrittemanuell SYSVOL wiederherstellen, wenn er vom DFSR repliziert wird:  
  
1.  Bei DFSR-Ereignis 4612 auf der ersten wiederhergestellten Domänencontrollers angezeigt wird, führen Sie eine manuelle autorisierende Wiederherstellung wie unter [2218556: zum Erzwingen einer autorativen und nicht autoritative Synchronisierungs für DFSR-repliziertes SYSVOL (wie "D4/D2" für FRS)](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556).  
  
2.  Legen Sie **SysvolReady Flag** 1 manuell, wie unter [947022 der NETLOGON-Freigabe ist nicht vorhanden, nach der Installation von Active Directory-Domänendienste auf einem neuen vollständigen oder schreibgeschützt Windows Server2008-basierten Domänencontroller](https://support.microsoft.com/kb/947022).  
  
 Sie können auch einen Diagnosebericht DFS-Replikation erstellen. Weitere Informationen finden Sie unter [Erstellen eines Diagnoseberichts für die DFS-Replikation](https://technet.microsoft.com/library/cc754227.aspx) und [DFS Step-by-Step Anleitung für Windows Server2008](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx). Wenn der Server mit Windows Server2008 R2 ausgeführt wird, können Sie [dfsrdiag.exe ReplicationState Befehlszeilenschalter](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx).  
  
 Sie können auch den Replikationen Test Replikationsfehler Überprüfung mit dcdiag.exe ausführen. Weitere Informationen finden Sie im Knowledge Base [Artikel 249256](https://support.microsoft.com/kb/249256).

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
