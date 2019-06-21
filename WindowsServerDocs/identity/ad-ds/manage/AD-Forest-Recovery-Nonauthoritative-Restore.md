---
title: Wiederherstellung der Active Directory-Gesamtstruktur - nicht autorisierende Wiederherstellung
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adds
ms.openlocfilehash: 65e33e6507d2affc4d07cc0780a7baf91a170a09
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280591"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Ausführen einer nicht autorisierenden Wiederherstellung von Active Directory Domain Services 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Um eine nicht autoritative Wiederherstellung durchzuführen, führen Sie das folgende Verfahren aus.  
  
Die folgenden Verfahren werden die Wbadmin.exe zum Ausführen einer nicht autoritativen Wiederherstellung von Active Directory oder Active Directory Domain Services (AD DS) verwenden. Wenn Sie eine andere sicherungslösung verwenden, oder wenn Sie beabsichtigen, die die autorisierende Wiederherstellung von SYSVOL weiter unten in der Gesamtstruktur-Wiederherstellungsprozess abschließen, können Sie eine autorisierende Wiederherstellung von SYSVOL mit diesen anderen Methoden ausführen:  
  
- Wenn Sie zum Replizieren von SYSVOL (File Replication Service, FRS) verwenden, führen Sie die Schritte in [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443) in der Microsoft Knowledge Base, mit der **BurFlags** Registrierungsschlüssels zum erneuten Initialisieren der FRS-Replikat Legt fest, oder bei Bedarf Artikel 315457 [315457](https://support.microsoft.com/kb/315457)zum Neuerstellen der SYSVOL-Struktur. Um zu bestimmen, wenn SYSVOL von FRS repliziert werden, finden Sie unter [bestimmen, ob ein Domänencontroller Ordners "SYSVOL" wird von der DFSR- oder FRS repliziert](https://msdn.microsoft.com/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs).  
- Wenn Sie zum Replizieren von SYSVOL-Replikation (Distributed File System, DFS) verwenden, finden Sie unter [eine autoritative Synchronisierung von DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).  

## <a name="performing-a-nonauthoritative-restore"></a>Eine nicht autoritative Wiederherstellung ausführen

Verwenden Sie das folgende Verfahren zum Ausführen einer nicht autoritativen Wiederherstellung von AD DS und eine autorisierende Wiederherstellung von SYSVOL zur gleichen Zeit mit wbadmin.exe auf einem Domänencontroller, die Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt wird. Die Sicherung muss explizit Systemstatus-Daten enthalten; eine vollständige serversicherung, die für die vollständige Wiederherstellung des Servers verwendet wird, ist nicht möglich. Weitere Informationen zum Erstellen einer Sicherung des Systemstatus finden Sie unter [Sicherung der Systemstatusdaten](AD-Forest-Recovery-Backing-up-System-State.md).  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>Zum Ausführen eine nicht autorisierende Wiederherstellung von AD DS und die autorisierende Wiederherstellung SYSVOL mithilfe von wbadmin.exe  
  
- Enthalten die **- Authsysvol** wechseln Sie in Ihrem Recovery-Befehl, wie im folgenden Beispiel gezeigt:  

   ```  
   wbadmin start systemstaterecovery <otheroptions> -authsysvol  
   ```  

   Zum Beispiel:  

   ```  
   wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
   ```  
  
![Wiederherstellen](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
