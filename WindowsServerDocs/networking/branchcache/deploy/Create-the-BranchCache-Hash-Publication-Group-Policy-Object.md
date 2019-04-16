---
title: Erstellen der BranchCache-Hash Publikation Gruppenrichtlinienobjekt
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4510d13c806adc2db46dfccce02a5a1b2814a2c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>Erstellen der BranchCache-Hash Publikation Gruppenrichtlinienobjekt

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie die BranchCache-hashveröffentlichung (Group Policy Object, GPO) erstellen.  
  
Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Vor dem Ausführen dieses Verfahrens müssen Sie die BranchCache Dateiserver-Organisationseinheit erstellen und Dateiserver in die Organisationseinheit verschieben. Weitere Informationen finden Sie unter [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>Erstellen des Gruppenrichtlinienobjekts für BranchCache-hashveröffentlichung  
  
1.  Öffnen Sie Windows PowerShell, geben **Mmc**, und drücken Sie dann die EINGABETASTE. Die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  In der MMC auf die **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**. Die **hinzufügen oder Entfernen von Snap-Ins** Dialogfeld wird geöffnet.  
  
3.  In **hinzufügen oder Entfernen von Snap-Ins**im **Verfügbare Snap-Ins**, doppelklicken Sie auf **Gruppenrichtlinienverwaltung**, und klicken Sie dann auf **OK**.  
  
4.  In der Gruppenrichtlinien-Verwaltungskonsole erweitern Sie den Pfad zu den BranchCache-Dateiservern Organisationseinheit, die Sie zuvor erstellt haben. Z.B. die Gesamtstruktur lautet example.com, den Namen Ihrer Domäne example1.com, und der Name der Organisationseinheit heißt BranchCache-Dateiservern, erweitern Sie den folgenden Pfad: **Gruppenrichtlinienverwaltung**, **Gesamtstruktur: example.com**, **Domänen**, **example1.com**, **BranchCache-Dateiservern**.  
  
5.  Mit der rechten Maustaste **BranchCache-Dateiservern**, und klicken Sie dann auf **ein Gruppenrichtlinienobjekt in dieser Domäne erstellen und verknüpfen Sie es hier**. Die **Gruppenrichtlinienobjekt** Dialogfeld wird geöffnet. In **Namen**, geben Sie einen Namen für das neue Gruppenrichtlinienobjekt. Geben Sie beispielsweise, wenn Sie das BranchCache-Hashveröffentlichung-Objekt zu benennen möchten, **BranchCache-Hashveröffentlichung**. Klicken Sie auf **OK**.  
  


