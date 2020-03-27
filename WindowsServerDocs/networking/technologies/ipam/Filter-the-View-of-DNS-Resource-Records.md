---
title: Filtern der Ansicht von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4e032e2c5b89dc362fceb34e06525d8632f7b19e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312407"
---
# <a name="filter-the-view-of-dns-resource-records"></a>Filtern der Ansicht von DNS-Ressourceneinträgen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um die Ansicht der DNS-Ressourcen Einträge in der IPAM-Client Konsole zu filtern.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>So filtern Sie die Ansicht der DNS-Ressourcen Einträge  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-Zonen**.  Der Navigationsbereich gliedert sich in einen oberen Navigationsbereich und einen niedrigeren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**. Alle von IPAM verwalteten DNS-Forward-Lookupzonen werden in den Suchergebnissen des Anzeige Bereichs angezeigt.  
  
4.  Klicken Sie auf die Zone, deren Datensätze Sie anzeigen und filtern möchten.  
  
5.  Klicken Sie im Anzeigebereich auf **Aktuelle Ansicht**, und klicken Sie dann auf **Ressourcen Einträge**. Die Ressourcen Einträge für die Zone werden im Anzeigebereich angezeigt.  
  
6.  Klicken Sie im Anzeigebereich auf **Kriterien hinzufügen**.  
  
    ![Kriterien hinzufügen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  Wählen Sie ein Kriterium aus der Dropdown Liste aus. Wenn Sie z. b. einen bestimmten Daten Satz Typen anzeigen möchten, klicken Sie auf **Typ aufzeichnen**.  
  
    ![Kriterien auswählen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  Klicken Sie auf **Hinzufügen**.  
  
    ![Kriterien hinzufügen](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. Der **Datensatz-Typ** wird als Suchparameter hinzugefügt. Geben Sie Text für den Typ des Datensatzes ein, den Sie suchen möchten. Wenn Sie z. b. nur SRV-Einträge anzeigen möchten, geben Sie **SRV**ein.  
  
    ![Geben Sie den Typ des Datensatzes an, den Sie suchen möchten.](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Drücken Sie die EINGABETASTE. Die DNS-Ressourcen Einträge werden nach den von Ihnen angegebenen Kriterien und der angegebenen Such Phrase gefiltert.  
  
    ![Ausführen des Filters](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[Verwaltung von DNS-Ressourcen Einträgen](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


