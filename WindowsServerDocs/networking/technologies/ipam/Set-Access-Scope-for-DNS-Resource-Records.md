---
title: Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c79e1f63b9bcb43520a57defca8228b76db68a31
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283869"
---
# <a name="set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, auf den Zugriffsbereich für eine DNS-Ressourceneinträge mithilfe der IPAM-Clientkonsole festlegen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträgen  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**.  Erweitern Sie im unteren Navigationsbereich, **Forward-Lookup** und navigieren Sie zu, und wählen Sie die Zone, die die Ressourceneinträge enthält, deren Zugriffsbereich, die Sie ändern möchten.  
  
3.  Klicken Sie im Anzeigebereich suchen Sie, und wählen Sie die Ressourceneinträge, deren Zugriffsbereich, die Sie ändern möchten.  
  
    ![Wählen Sie die Ressourceneinträge](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  Mit der rechten Maustaste in die ausgewählte DNS-Ressourceneinträge, und klicken Sie dann auf **Zugriffsbereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  Die **Zugriffsbereich festlegen** Dialogfeld wird geöffnet. Wenn für Ihre Bereitstellung erforderlich ist, klicken Sie auf, um die Auswahl aufzuheben **Zugriffsbereich vom übergeordneten Element erben**. In **auswählen des Zugriffsbereichs**, wählen Sie ein Element aus, und klicken Sie dann auf **OK**.  
  
    ![Wählen Sie den Zugriffsbereich](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffssteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


