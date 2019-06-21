---
title: Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44db34199257367e98279ccbcbc2d5041ee9884c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283807"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um DNS-Ressourceneinträgen für eine DNS-Zone in der IPAM-Clientkonsole anzuzeigen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>Anzeigen von DNS-Ressourceneinträgen für eine zone  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Im Navigationsbereich, die in einer oberen Navigationsbereich und einer unteren Navigationsbereich unterteilt werden.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**, und erweitern Sie dann die Domäne und Zeitzone-Liste, um zu ermitteln, und wählen Sie die Zone, die Sie anzeigen möchten. Beispielsweise wenn Sie eine Zone namens Dublin haben, klicken Sie auf **Dublin**.  
  
    ![Wählen Sie die Zone, die Sie anzeigen möchten.](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  Ist im Anzeigebereich die Standardansicht der DNS-Server für die Zone. Um die Ansicht zu ändern, klicken Sie auf **aktuelle Ansicht**, und klicken Sie dann auf **Ressourceneinträge**.  
  
    ![Ändern Sie die Ansicht in Ressourceneinträge](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  Die DNS-Ressourceneinträge für die Zone werden angezeigt. Geben Sie zum Filtern der Datensätze, die den Text, der in der gesucht werden soll **Filter**.  
  
    ![Geben Sie Text zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  Um die Ressourcendatensätze nach Typ des hostnamenseintrags, des Zugriffsbereichs oder anderen Kriterien zu filtern, klicken Sie auf **Kriterien hinzufügen**, und klicken Sie dann Optionen in der Liste, und klicken Sie auf **hinzufügen**.  
  
    ![Verwenden Sie die Kriterien zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


