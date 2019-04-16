---
title: Konfigurieren Sie das BranchCache-Hash Publikation Gruppenrichtlinienobjekt
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6f528c9f0a8a39b286ad7ac4fa728d93c311f779
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>Konfigurieren Sie das BranchCache-Hash Publikation Gruppenrichtlinienobjekt

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können die BranchCache-hashveröffentlichung (Group Policy Object, GPO) so konfigurieren, dass alle Server, die Sie der Organisationseinheit hinzugefügt haben die gleiche Richtlinie hashveröffentlichungseinstellung angewendet haben.  
  
Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Vor dem Ausführen dieses Verfahrens müssen Sie die BranchCache Dateiserver-Organisationseinheit, erstellen Verschieben von Dateiservern in die Organisationseinheit und Gruppenrichtlinienobjekt für BranchCache-hashveröffentlichung erstellen. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>So konfigurieren Sie die BranchCache-hashveröffentlichung Gruppenrichtlinienobjekt  
  
1.  Führen Sie Windows PowerShell als Administrator, Typ **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  In der MMC auf die **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.  
  
3.  In **hinzufügen oder Entfernen von Snap-Ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **OK**.  
  
4.  In der Gruppenrichtlinien-Verwaltungskonsole erweitern Sie den Pfad zu den BranchCache-hashveröffentlichung Gruppenrichtlinienobjekt, das Sie zuvor erstellt haben. Z. B. wenn die Gesamtstruktur den Namen "Beispiel.com" ist, den Namen Ihrer Domäne beispiel1.com und des Gruppenrichtlinienobjekts **BranchCache-Hashveröffentlichung**, erweitern Sie den folgenden Pfad: **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: "Beispiel.com"**, **Domänen**, **beispiel1.com**, **Group Policy Objects**, **BranchCache-Hashveröffentlichung**.  
  
5.  Mit der rechten Maustaste die **BranchCache-Hashveröffentlichung** Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**. Die Konsole des Gruppenrichtlinienverwaltungs-Editor wird geöffnet.  
  
6.  Erweitern Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor den folgenden Pfad: **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **Netzwerk**, **Lanman-Server**.  
  
7.  Klicken Sie in der Konsole Gruppenrichtlinienverwaltungs-Editor auf **Lanman-Server**. Doppelklicken Sie im Detailbereich auf **Hashveröffentlichung für BranchCache**. Die **Hashveröffentlichung für BranchCache** Dialogfeld wird geöffnet.  
  
8.  In der **Hashveröffentlichung für BranchCache** Dialogfeld, klicken Sie auf **aktiviert**.  
  
9. In **Optionen**, klicken Sie auf **hashveröffentlichung für alle freigegebenen Ordner zulassen**, und klicken Sie dann auf eine der folgenden:  
  
    1.  Klicken Sie zum Aktivieren von hashveröffentlichung für alle freigegebenen Ordner für alle Dateiserver, die Sie mit der Organisationseinheit hinzugefügt **hashveröffentlichung für alle freigegebenen Ordner zulassen**.  
  
    2.  Um hashveröffentlichung nur für freigegebene Ordner aktivieren, für die BranchCache aktiviert ist, klicken Sie auf **zulassen hashveröffentlichung nur für freigegebene Ordner auf dem BranchCache aktiviert ist**.  
  
    3.  Um hashveröffentlichung für alle Ordner auf dem Computer, freigegebenen auch wenn BranchCache, auf die Dateifreigaben aktiviert ist zu sperren, klicken Sie auf **verbieten Sie hashveröffentlichung für alle freigegebenen Ordner**.  
  
10. Klicken Sie auf **OK**.  
  
> [!NOTE]  
> In den meisten Fällen müssen Sie die MMC-Konsole speichern und aktualisieren, um die Änderungen an der Konfiguration angezeigt, die Sie vorgenommen haben.  
  


