---
title: Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 786c1ee8fd673bd17465ab9586dd1e0bcfd7971c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die DNS-Ressourceneinträgen für eine DNS-Zone in der IPAM-Clientkonsole anzeigen.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>Anzeigen von DNS-Ressourceneinträgen für eine zone  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Der Navigationsbereich unterteilt in ein im oberen Navigationsbereich und einen unteren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich, klicken Sie auf **Forward-Lookup**, und erweitern Sie dann die Domäne und Zeitzone Liste zu suchen, und wählen Sie die Zone, die Sie anzeigen möchten. Z. B. Wenn Sie eine Zone namens Dublin haben, klicken Sie auf **Dublin**.  
  
    ![Wählen Sie die Zone, die Sie anzeigen möchten.](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  Klicken Sie im Anzeigebereich ist die Standardansicht der DNS-Server für die Zone. Um die Ansicht ändern möchten, klicken Sie auf **aktuelle Ansicht**, und klicken Sie dann auf **Ressourceneinträge**.  
  
    ![Ändern der Ansicht für Ressourceneinträge](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  Die DNS-Ressourceneinträge für die Zone werden angezeigt. Zum Filtern der Datensätze, geben Sie den Text, die Sie in suchen möchten **Filter**.  
  
    ![Geben Sie Text zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  Um die Ressource nach Datensatztyp, Zugriffsbereich oder anderen Kriterien filtern, klicken Sie auf **Kriterien hinzufügen**, und treffen Sie die Kriterien aus, und klicken Sie auf **hinzufügen**.  
  
    ![Verwenden von Kriterien zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


