---
title: Festlegen des Zugriffsbereichs für eine DNS-Zone
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
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a4e84f249e57df6bfd04203c8b825ff5d4d643b2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="set-access-scope-for-a-dns-zone"></a>Festlegen des Zugriffsbereichs für eine DNS-Zone

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Clientkonsole Zugriffsbereich für eine DNS-Zone festlegen.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>Festlegen des Zugriffsbereichs für eine DNS-Zone  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**. Klicken Sie im Anzeigebereich mit der Maustaste der DNS-Zone für die Sie ändern möchten Bereich. Zugriff, und klicken Sie dann auf **Zugriffsbereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  Die **Zugriffsbereich festlegen** Dialogfeld wird geöffnet. Wenn für Ihre Bereitstellung erforderlich ist, klicken Sie auf zum Aufheben der Auswahl **erben Zugriffsbereich vom übergeordneten Element**. In **Zugriffsbereich auswählen**, wählen Sie ein Element, und klicken Sie dann auf **OK**.  
  
    ![Wählen Sie den Zugriffsbereich](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  Im Anzeigebereich IPAM Client Console stellen Sie sicher, dass der Zugriffsbereich für die Zone geändert wird.  
  
    ![Stellen Sie sicher, dass der Zugriffsbereich für die Zone geändert wird](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffsteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


