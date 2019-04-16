---
title: Aktivieren von Hashveröffentlichung für Dateiserver für die keine Domänenmitglieder sind
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4cb3d217115cff3a9b30ee11acb7ba0de6672b24
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>Aktivieren von Hashveröffentlichung für Dateiserver für die keine Domänenmitglieder sind

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Verwenden Sie dieses Verfahren zum Konfigurieren von hashveröffentlichung für BranchCache mithilfe der Gruppenrichtlinie des lokalen Computers auf einem Dateiserver, auf denen Windows Server2016 mit ausgeführt, wird die **BranchCache für Netzwerkdateien** Rollendienst der Dateidienste-Serverrolle installiert.  
  
Dieses Verfahren dient zur Verwendung auf einem Dateiserver für die keine Domänenmitglieder sind. Wenn Sie dieses Verfahren, auf die Datei ein Domänenmitgliedsserver ausführen, und außerdem BranchCache mithilfe der Gruppenrichtlinie der Domäne konfigurieren, überschreiben Gruppenrichtlinien lokale Gruppenrichtlinien-Einstellungen.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Wenn Sie eine oder mehrere Datei Domänenmitgliedsserver haben, Sie mit einer Organisationseinheit (OU) in Active Directory-Domänendiensten hinzugefügt und anschließend mithilfe der Gruppenrichtlinie hashveröffentlichung für alle Dateiserver gleichzeitig konfigurieren, anstatt jeden Dateiserver einzeln zu konfigurieren. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>Aktivieren von hashveröffentlichung für einen einzelnen Dateiserver  
  
1.  Öffnen Sie Windows PowerShell, geben **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  In der MMC auf die **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.  
  
3.  In **hinzufügen oder Entfernen von Snap-Ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **Gruppenrichtlinienobjekt-Editor**. Der Gruppenrichtlinien-Assistent wird geöffnet, mit dem lokalen Computer-Objekt ausgewählt. Klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Erweitern Sie in der MMC Editor für lokale Gruppenrichtlinien den folgenden Pfad: **Richtlinie des lokalen Computers**, **Computerkonfiguration**, **Administrative Vorlagen**, **Netzwerk**, **Lanman-Server**. Klicken Sie auf **Lanman-Server**.  
  
5.  Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Die **Hashveröffentlichung für BranchCache** Dialogfeld wird geöffnet.  
  
6.  In der **Hashveröffentlichung für BranchCache** Dialogfeld, klicken Sie auf **aktiviert**.  
  
7.  In **Optionen**, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf eine der folgenden:  
  
    1.  Klicken Sie zum Aktivieren von hashveröffentlichung für alle freigegebenen Ordner auf diesem Computer auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um hashveröffentlichung nur für freigegebene Ordner aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **zulassen hashveröffentlichung nur für freigegebene Ordner auf dem BranchCache aktiviert ist**.  
  
    3.  Um hashveröffentlichung für alle Ordner auf dem Computer, freigegebenen auch wenn BranchCache, auf die Dateifreigaben aktiviert ist zu sperren, klicken Sie auf **verbieten Sie hashveröffentlichung für alle freigegebenen Ordner**.  
  
8.  Klicken Sie auf **OK**.  
  


