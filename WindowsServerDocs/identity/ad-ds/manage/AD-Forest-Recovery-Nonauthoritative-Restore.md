---
title: Wiederherstellung der Active Directory-Gesamtstruktur - nicht autorisierende Wiederherstellung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adfs
ms.openlocfilehash: 684672491a0574b12e9b117a8e3c9c1f0936f357
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Eine nicht autoritative Wiederherstellung der Active Directory-Domänendienste ausführen 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
 Gehen Sie folgendermaßen vor, um eine nicht autoritative Wiederherstellung durchzuführen.  
  
 Die folgenden Verfahren werden die Wbadmin.exe nicht autoritative Wiederherstellung von Active Directory oder Active Directory-Domänendienste (AD DS) verwenden. Wenn Sie eine andere Lösung für die Sicherung verwenden oder wenn Sie die autorisierende Wiederherstellung von SYSVOL weiter unten in der Gesamtstruktur Recovery-Vorgang abschließen möchten, können Sie eine autorisierende Wiederherstellung von SYSVOL mit diesen alternativen Methoden ausführen:  
  
-   Wenn Sie zum Replizieren von SYSVOL (File Replication Service, FRS) verwenden, führen Sie die Schrittein [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443) in der Microsoft Knowledge Base mit der **BurFlags** Registrierungsschlüssel erneut initialisieren FRS-Replikatsätzen, oder bei Bedarf Artikel 315457 [315457](https://support.microsoft.com/kb/315457)neu erstellen, die SYSVOL-Struktur. Um festzustellen, ob SYSVOL von FRS repliziert wird, finden Sie unter [bestimmen, ob ein Domänencontroller des Ordners "SYSVOL" wird durch die DFSR- oder FRS repliziert](https://msdn.microsoft.com/en-us/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs).  
  
-   Wenn Sie zum Replizieren von SYSVOL-Replikation (Distributed File System, DFS) verwenden, finden Sie unter [eine autoritative Synchronisierung von SYSVOL mit DFS-Replikation ausgeführt](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).  
  
 
## <a name="performing-a-nonauthoritative-restore"></a>Durchführen einer nicht autoritativen Wiederherstellung  
 Verwenden Sie das folgende Verfahren zum Ausführen einer nicht autoritativen Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL zur gleichen Zeit mit wbadmin.exe auf einem Domänencontroller, der Windows Server2012, Windows Server2008 R2 oder Windows Server2008 ausgeführt wird. Die Sicherung muss explizit Systemstatusdaten enthalten. eine vollständige Sicherung, die für vollständige Wiederherstellung des Servers verwendet wird, funktionieren nicht. Weitere Informationen zum Erstellen einer Sicherung des Systemstatus, finden Sie unter [Sicherung der Systemstatusdaten](AD-Forest-Recovery-Backing-up-System-State.md).  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>Eine nicht autoritative Wiederherstellung von AD DS und autorisierende Wiederherstellung von SYSVOL mit wbadmin.exe ausführen  
  
-   Enthalten die **- Authsysvol** in Ihrem Befehl Wiederherstellung wechseln, wie im folgenden Beispiel dargestellt:  
  
    ```  
    wbadmin start systemstaterecovery <otheroptions> -authsysvol  
    ```  
  
     Zum Beispiel:  
  
    ```  
    wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
    ```  
  
 ![Stellen Sie wieder her](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
