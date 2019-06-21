---
title: Löschen von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ecbe5dcc452aa39a9afca7e1c8d5fe70d8d4528d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283979"
---
# <a name="delete-dns-resource-records"></a>Löschen von DNS-Ressourceneinträgen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um eine oder mehrere DNS-Ressourceneinträge mithilfe der IPAM-Clientkonsole zu löschen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-delete-dns-resource-records"></a>So löschen Sie die DNS-Ressourceneinträgen  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich in **ÜBERWACHEN und verwalten**, klicken Sie auf **DNS-Zonen**.  Im Navigationsbereich, die in einer oberen Navigationsbereich und einer unteren Navigationsbereich unterteilt werden.  
  
3.  Erweitern Sie **Forward-Lookup** und die Domäne, in dem sich die Zone und die Ressourcendatensätze, die Sie löschen möchten befinden. Klicken Sie auf die Zone, und klicken Sie im Anzeigebereich erscheint, klicken Sie auf **aktuelle Ansicht**. Klicken Sie auf **Ressourceneinträge**.  
  
4.  Klicken Sie im Anzeigebereich suchen Sie, und wählen Sie die Ressourceneinträge, die Sie löschen möchten.  
  
    ![Wählen Sie die, die zu löschende Ressourcendatensätze](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  Mit der rechten Maustaste in die ausgewählten Datensätze, und klicken Sie dann auf **Löschen von DNS-Ressourceneintrag**.  
  
    ![Löschen Sie die Datensätze](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  Die **Löschen von DNS-Ressourceneintrag** Dialogfeld wird geöffnet. Stellen Sie sicher, dass der richtige DNS-Server ausgewählt ist. Wenn sie nicht der Fall ist, klicken Sie auf **DNS-Server** , und wählen Sie den Server aus dem Sie die Ressourceneinträge löschen möchten. Klicken Sie auf **OK**. IPAM löscht die Ressourcendatensätze vom DNS-Server.  
  
    ![Stellen Sie sicher, dass der richtige DNS-Server aktiviert ist, und Löschen von Datensätzen](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[DNS-Datensatz Ressourcenverwaltung](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


