---
title: Filtern der Ansicht von DNS-Ressourceneinträgen
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
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 35c0e822daa9f2c8c49ae7e6f2f40ec0411cb6fa
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="filter-the-view-of-dns-resource-records"></a>Filtern der Ansicht von DNS-Ressourceneinträgen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die Ansicht der DNS-Ressourceneinträge in der IPAM-Clientkonsole filtern.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>Zum Filtern der Ansicht von DNS-Ressourceneinträgen  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Der Navigationsbereich unterteilt in ein im oberen Navigationsbereich und einen unteren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich, klicken Sie auf **Forward-Lookup**. Alle IPAM verwalteten DNS-Forward-Lookupzonen werden im Bereich der Suchergebnisse angezeigt.  
  
4.  Klicken Sie auf die Zone, deren Datensätze, die Sie anzeigen und filtern möchten.  
  
5.  Klicken Sie im Anzeigebereich auf **aktuelle Ansicht**, und klicken Sie dann auf **Ressourceneinträge**. Klicken Sie im Anzeigebereich werden die Ressourceneinträge für die Zone angezeigt.  
  
6.  Klicken Sie im Anzeigebereich auf **Kriterien hinzufügen**.  
  
    ![Hinzufügen von Kriterien](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  Wählen Sie ein Kriterium aus der Dropdown Liste. Beispielsweise, wenn Sie einen bestimmten Datensatztyp anzeigen möchten, klicken Sie auf **Datensatztyp**.  
  
    ![Wählen Sie ein Kriterium](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  Klicken Sie auf **hinzufügen**.  
  
    ![Die Kriterien hinzufügen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **Datensatztyp** wird als Suchparameter hinzugefügt. Geben Sie Text für den Typ des Eintrags, den Sie suchen möchten. Geben Sie beispielsweise, wenn Sie nur die SRV-Einträge anzeigen möchten, **SRV**.  
  
    ![Geben Sie den Eintrag, der gesucht werden soll](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Drücken Sie die EINGABETASTE. Die DNS-Ressourceneinträge werden gemäß den Kriterien gefiltert und suchen Sie einen Ausdruck, den Sie angegeben.  
  
    ![Führen Sie den filter](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


