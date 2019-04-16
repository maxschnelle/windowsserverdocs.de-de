---
title: Löschen von DNS-Ressourceneinträgen
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
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f9ebfeca1da9e36cd00272113f2e86c33174074b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="delete-dns-resource-records"></a>Löschen von DNS-Ressourceneinträgen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie um einen oder mehrere DNS-Ressourceneinträge zu löschen, indem Sie mithilfe der IPAM-Clientkonsole.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-delete-dns-resource-records"></a>So löschen Sie DNS-Ressourceneinträgen  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Der Navigationsbereich unterteilt in ein im oberen Navigationsbereich und einen unteren Navigationsbereich.  
  
3.  Erweitern Sie **Forward-Lookup** und der Domäne, in denen die Zone und Ressource Datensätze, die Sie löschen möchten befinden. Klicken Sie auf die Zone, und klicken Sie im Anzeigebereich, klicken Sie auf **aktuelle Ansicht**. Klicken Sie auf **Ressourceneinträge**.  
  
4.  Klicken Sie im Anzeigebereich suchen Sie, und wählen Sie die Ressourceneinträge, die Sie löschen möchten.  
  
    ![Wählen Sie die Ressource, die zu löschende Datensätze](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  Maustaste auf die ausgewählten Einträge, und klicken Sie dann auf **Löschen von DNS-Ressourceneintrag**.  
  
    ![Löschen Sie die Datensätze](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  Die **Löschen von DNS-Ressourceneintrag** Dialogfeld wird geöffnet. Stellen Sie sicher, dass der richtige DNS-Server aktiviert ist. Wenn sie nicht der Fall ist, klicken Sie auf **DNS-Server** und wählen Sie den Server, von dem Sie die Ressourceneinträge löschen möchten. Klicken Sie auf **OK**. IPAM löscht die Ressourceneinträge aus der DNS-Server.  
  
    ![Stellen Sie sicher, dass der richtige DNS-Server aktiviert ist, und Löschen von Datensätzen](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


