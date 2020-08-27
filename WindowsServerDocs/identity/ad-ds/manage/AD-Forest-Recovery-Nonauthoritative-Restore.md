---
title: AD-Gesamtstruktur Wiederherstellung-nicht autoritative Wiederherstellung
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.openlocfilehash: c46eb76f707b7285e06c01fef14534163df00823
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939650"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Ausführen einer nicht autoritativen Wiederherstellung von Active Directory Domain Services

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Führen Sie das folgende Verfahren aus, um eine nicht autoritative Wiederherstellung durchzuführen.

In den folgenden Verfahren wird der Wbadmin.exe verwendet, um eine nicht autoritative Wiederherstellung von Active Directory oder Active Directory Domain Services (AD DS) auszuführen. Wenn Sie eine andere Sicherungs Lösung verwenden oder wenn Sie beabsichtigen, die autoritative Wiederherstellung von SYSVOL später im Wiederherstellungsprozess der Gesamtstruktur abzuschließen, können Sie eine autoritative Wiederherstellung von SYSVOL mithilfe der folgenden alternativen Methoden ausführen:

- Wenn Sie den Datei Replikations Dienst (File Replication Service, FRS) zum Replizieren von SYSVOL verwenden, befolgen Sie die Schritte im [Artikel 290762](https://go.microsoft.com/fwlink/?LinkId=148443) in der Microsoft Knowledge Base. verwenden Sie dazu den **BurFlags** -Registrierungsschlüssel, um FRS-Replikat [315457](https://support.microsoft.com/kb/315457)315457 Gruppen erneut zu initialisieren Um zu ermitteln, ob SYSVOL von FRS repliziert wird, finden Sie unter [bestimmen, ob der SYSVOL-Ordner eines Domänen Controllers von DFSR oder FRS repliziert wird](/windows/win32/vss/backing-up-and-restoring-an-frs-replicated-sysvol-folder#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs).
- Wenn Sie die Replikation von SYSVOL mithilfe der DFS-Replikation (verteiltes Dateisystem) replizieren, finden Sie unter [Ausführen einer autorisierenden Synchronisierung von DFSR-replizierten SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)

## <a name="performing-a-nonauthoritative-restore"></a>Ausführen einer nicht autorisierenden Wiederherstellung

Verwenden Sie das folgende Verfahren, um eine nicht autoritative Wiederherstellung von AD DS und eine autoritative Wiederherstellung von SYSVOL gleichzeitig mithilfe wbadmin.exe auf einem Domänen Controller auszuführen, auf dem Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt wird. Die Sicherung muss explizit Systemstatus Daten einschließen. eine vollständige Server Sicherung, die für die vollständige Server Wiederherstellung verwendet wird, funktioniert nicht. Weitere Informationen zum Erstellen einer Systemstatus Sicherung finden Sie unter [Sichern der Systemstatus Daten](AD-Forest-Recovery-Backing-up-System-State.md).

### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>So führen Sie eine nicht autoritative Wiederherstellung AD DS und autoritative Wiederherstellung von SYSVOL mithilfe wbadmin.exe

- Schließen Sie den Schalter **-authsysvol** in den Wiederherstellungs Befehl ein, wie im folgenden Beispiel gezeigt:

   ```
   wbadmin start systemstaterecovery <otheroptions> -authsysvol
   ```

   Beispiel:

   ```
   wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol
   ```

![Restore](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
