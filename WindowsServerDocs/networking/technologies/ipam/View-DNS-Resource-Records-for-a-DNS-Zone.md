---
title: Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca2cf532fc9fa7e1f12e5294b40d29863fd42261
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312332"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>Anzeigen von DNS-Ressourceneinträgen für eine DNS-Zone

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um DNS-Ressourcen Einträge für eine DNS-Zone in der IPAM-Client Konsole anzuzeigen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>So zeigen Sie DNS-Ressourcen Einträge für eine Zone an  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-Zonen**.  Der Navigationsbereich gliedert sich in einen oberen Navigationsbereich und einen niedrigeren Navigationsbereich.  
  
3.  Klicken Sie im unteren Navigationsbereich auf **Forward-Lookup**, und erweitern Sie dann die Liste Domäne und Zone, um die Zone zu suchen und auszuwählen, die Sie anzeigen möchten. Wenn Sie z. b. eine Zone mit dem Namen Dublin haben, klicken Sie auf **Dublin**.  
  
    ![Wählen Sie die Zone aus, die Sie anzeigen möchten.](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  Im Anzeigebereich ist die Standardansicht der DNS-Server für die Zone. Um die Ansicht zu ändern, klicken Sie auf **Aktuelle Ansicht**und dann auf **Ressourcen Einträge**.  
  
    ![Ändern der Ansicht in Ressourcen Einträge](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  Die DNS-Ressourcen Einträge für die Zone werden angezeigt. Um die Datensätze zu filtern, geben Sie den Text ein, der in **Filter**gesucht werden soll.  
  
    ![Typtext zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  Klicken Sie zum Filtern der Ressourcen Datensätze nach Daten Satz Typen, Zugriffs Bereich oder anderen Kriterien auf **Kriterien hinzufügen**, und treffen Sie dann in der Kriterienliste eine Auswahl, und klicken Sie auf **Hinzufügen**.  
  
    ![Verwenden von Kriterien zum Filtern von Datensätzen](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[DNS-Zonenverwaltung](DNS-Zone-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


