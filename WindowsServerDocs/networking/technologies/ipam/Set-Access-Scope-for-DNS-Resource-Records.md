---
title: Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge
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
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 06c33a633975497e80863cc8d42b14a0f9ac8193
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Clientkonsole Festlegen des Zugriffsbereichs für eine DNS-Ressourceneinträge.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**.  Erweitern Sie im unteren Navigationsbereich **Forward-Lookup** und navigieren Sie zu, und wählen Sie die Zone, die die Ressourceneinträge enthält, dessen Zugriffsbereich, die Sie ändern möchten.  
  
3.  Klicken Sie im Anzeigebereich suchen Sie, und wählen Sie die Ressourceneinträge, deren Zugriffsbereich, die Sie ändern möchten.  
  
    ![Wählen Sie die Ressourceneinträge](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  Maustaste auf die ausgewählten DNS-Ressourceneinträge, und klicken Sie dann auf **Zugriffsbereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  Die **Zugriffsbereich festlegen** Dialogfeld wird geöffnet. Wenn für Ihre Bereitstellung erforderlich ist, klicken Sie auf zum Aufheben der Auswahl **erben Zugriffsbereich vom übergeordneten Element**. In **Zugriffsbereich auswählen**, wählen Sie ein Element, und klicken Sie dann auf **OK**.  
  
    ![Wählen Sie den Zugriffsbereich](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffsteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


