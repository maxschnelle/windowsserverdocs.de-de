---
title: Filtern der Ansicht von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fed5e1f923d3560b91f514d1e59d79b847557c8b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847801"
---
# <a name="filter-the-view-of-dns-resource-records"></a>Filtern der Ansicht von DNS-Ressourceneinträgen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um DNS-Ressourceneinträge in der IPAM-Clientkonsole die Ansicht zu filtern.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>Filtern die Ansicht von DNS-Ressourceneinträgen  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Im Navigationsbereich, die in einer oberen Navigationsbereich und einer unteren Navigationsbereich unterteilt werden.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**. Alle IPAM verwalteten DNS-Forward-Lookup-Zonen werden in den Suchergebnissen der Anzeige im Bereich angezeigt.  
  
4.  Klicken Sie auf die Zone, deren Datensätze, die Sie anzeigen und filtern möchten.  
  
5.  Klicken Sie im Anzeigebereich auf **aktuelle Ansicht**, und klicken Sie dann auf **Ressourceneinträge**. Der Ressourceneinträge für die Zone werden im Anzeigebereich angezeigt.  
  
6.  Klicken Sie im Anzeigebereich auf **Kriterien hinzufügen**.  
  
    ![Kriterien hinzufügen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  Wählen Sie ein Kriterium aus der Dropdown-Liste ein. Z. B. Wenn Sie einen bestimmten Datensatztyp anzeigen möchten, klicken Sie auf **Datensatztyp**.  
  
    ![Wählen Sie ein Kriterium](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  Klicken Sie auf **Hinzufügen**.  
  
    ![Die Kriterien hinzufügen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **Datensatztyp** als Suchparameter hinzugefügt wird. Geben Sie Text für den Typ des Datensatzes, der gesucht werden soll. Geben Sie beispielsweise, wenn Sie nur die SRV-Einträge anzeigen möchten, **SRV**.  
  
    ![Geben Sie den Typ des Datensatzes, der gesucht werden soll](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Drücken Sie die EINGABETASTE. Die DNS-Ressourceneinträge gemäß den Kriterien gefiltert werden, und suchen Ausdruck, den Sie angegeben haben.  
  
    ![Führen Sie den filter](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


