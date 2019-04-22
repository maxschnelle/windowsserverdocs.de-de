---
title: Aktivieren der Hashveröffentlichung für Dateiserver, die keine Domänenmitglieder sind
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00be97abbd583e4c5e762775ea563ba0720d5142
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814951"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>Aktivieren der Hashveröffentlichung für Dateiserver, die keine Domänenmitglieder sind

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwenden Sie dieses Verfahren zum Konfigurieren von hashveröffentlichung für BranchCache mithilfe der Gruppenrichtlinie des lokalen Computers auf einem Dateiserver, die Ausführung von Windows Server 2016 mit den **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste Server-Rolle installiert.  
  
Dieses Verfahren ist für die Verwendung auf einem Dateiserver nicht Mitglied einer Domäne vorgesehen. Wenn Sie dieses Verfahren auf einem Dateiserver ausführen, der Mitglied einer Domäne ist, und außerdem BranchCache mithilfe einer Domänengruppenrichtlinie konfigurieren, überschreiben die Gruppenrichtlinieneinstellungen der Domäne die lokalen Gruppenrichtlinieneinstellungen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  
  
> [!NOTE]  
> Wenn einer oder mehrere Ihrer Dateiserver Mitglied einer Domäne sind, können Sie diese einer Organisationseinheit in Active Directory-Domänendiensten hinzufügen und anschließend mithilfe der Gruppenrichtlinie Hashveröffentlichung für alle Dateiserver gleichzeitig konfigurieren, anstatt jeden Dateiserver einzeln zu konfigurieren. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>So aktivieren Sie Hashveröffentlichung für einen einzelnen Dateiserver  
  
1.  Öffnen Sie Windows PowerShell, geben Sie **mmc**ein, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Klicken Sie in der MMC im Menü **Datei** auf **Snap-In hinzufügen/entfernen**. Das Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** wird geöffnet.  
  
3.  Doppelklicken Sie in **Snap-Ins hinzufügen bzw. entfernen** unter **Verfügbare Snap-Ins** auf **Gruppenrichtlinienobjekt-Editor**. Der Gruppenrichtlinien-Assistent wird geöffnet und das Objekt Lokaler Computer ausgewählt. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Erweitern Sie in der MMC des Editors für lokale Gruppenrichtlinien den folgenden Pfad: **Lokale Computerrichtlinie**, **Computerkonfiguration**, **Administrative Vorlagen**, **Netzwerk**, **Lanman-Server**. Klicken Sie auf **Lanman-Server**.  
  
5.  Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Das Dialogfeld **Hashveröffentlichung für BranchCache** wird geöffnet.  
  
6.  Klicken Sie im Dialogfeld **Hashveröffentlichung für BranchCache** auf **Aktiviert**.  
  
7.  In **Optionen**, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf einen der folgenden:  
  
    1.  Um hashveröffentlichung für alle freigegebenen Ordner auf diesem Computer aktivieren möchten, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um Hashveröffentlichung nur für freigegebene Ordner zu aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **Hashveröffentlichung nur für freigegebene Ordner mit aktiviertem BranchCache zulassen.**  
  
    3.  Um keine Hashveröffentlichung für alle freigegebenen Ordner auf dem Computer zuzulassen, auch wenn BranchCache auf den Dateifreigaben aktiviert ist, klicken Sie auf **Hashveröffentlichung für keinen freigegebenen Ordner zulassen**.  
  
8.  Klicken Sie auf **OK**.  
  


