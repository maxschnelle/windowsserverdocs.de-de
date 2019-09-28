---
title: Aktivieren der Hashveröffentlichung für Dateiserver, die keine Domänenmitglieder sind
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e870863b497c17b4b56265d99d91274e34690767
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356536"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver, die keine Domänenmitglieder sind

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die Hash Veröffentlichung für BranchCache mithilfe der lokalen Computer Gruppenrichtlinie auf einem Dateiserver konfigurieren, auf dem Windows Server 2016 mit dem Rollen Dienst " **BranchCache für Netzwerkdateien** " der Server Rolle "Dateidienste" ausgeführt wird.  
  
Dieses Verfahren ist für die Verwendung auf einem Dateiserver vorgesehen, der nicht Mitglied einer Domäne ist. Wenn Sie dieses Verfahren auf einem Dateiserver ausführen, der Mitglied einer Domäne ist, und außerdem BranchCache mithilfe einer Domänengruppenrichtlinie konfigurieren, überschreiben die Gruppenrichtlinieneinstellungen der Domäne die lokalen Gruppenrichtlinieneinstellungen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
> [!NOTE]  
> Wenn einer oder mehrere Ihrer Dateiserver Mitglied einer Domäne sind, können Sie diese einer Organisationseinheit in Active Directory-Domänendiensten hinzufügen und anschließend mithilfe der Gruppenrichtlinie Hashveröffentlichung für alle Dateiserver gleichzeitig konfigurieren, anstatt jeden Dateiserver einzeln zu konfigurieren. Weitere Informationen finden Sie unter [Aktivieren der Hash Veröffentlichung für Domänen Mitglieds-Dateiserver](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>So aktivieren Sie Hashveröffentlichung für einen einzelnen Dateiserver  
  
1.  Öffnen Sie Windows PowerShell, geben Sie **mmc**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienobjekt-Editor**. Der Gruppenrichtlinien-Assistent wird geöffnet und das Objekt Lokaler Computer ausgewählt. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Erweitern Sie in der MMC des Editors für lokale Gruppenrichtlinien den folgenden Pfad: **Richtlinie für den lokalen Computer**, **Computerkonfiguration**, **Administrative Vorlagen**, **Netzwerk**, **LanMan-Server**. Klicken Sie auf **Lanman-Server**.  
  
5.  Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Das Dialogfeld **Hashveröffentlichung für BranchCache** wird geöffnet.  
  
6.  Klicken Sie im Dialogfeld **Hashveröffentlichung für BranchCache** auf **Aktiviert**.  
  
7.  Klicken Sie unter Optionen auf **Hash Veröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf eine der folgenden **Optionen**:  
  
    1.  Um die Hash Veröffentlichung für alle freigegebenen Ordner auf diesem Computer zu aktivieren, klicken Sie auf **Hash Veröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um Hashveröffentlichung nur für freigegebene Ordner zu aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **Hashveröffentlichung nur für freigegebene Ordner mit aktiviertem BranchCache zulassen.**  
  
    3.  Um keine Hashveröffentlichung für alle freigegebenen Ordner auf dem Computer zuzulassen, auch wenn BranchCache auf den Dateifreigaben aktiviert ist, klicken Sie auf **Hashveröffentlichung für keinen freigegebenen Ordner zulassen**.  
  
8.  Klicken Sie auf **OK**.  
  


