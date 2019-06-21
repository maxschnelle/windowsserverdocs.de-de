---
title: Festlegen des Zugriffsbereichs für eine DNS-Zone
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 67e6e16d361d6d975c4cf900dc9c6b9e7abd3f20
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282201"
---
# <a name="set-access-scope-for-a-dns-zone"></a>Festlegen des Zugriffsbereichs für eine DNS-Zone

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, zum Zugriffsbereich für eine DNS-Zone mithilfe der IPAM-Clientkonsole festgelegt.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>Beim Festlegen des Zugriffsbereichs für eine DNS-zone  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**. Klicken Sie im Anzeigebereich mit der Maustaste der DNS-Zone für die Sie ändern möchten die Bereich., und klicken Sie dann auf **Zugriffsbereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  Die **Zugriffsbereich festlegen** Dialogfeld wird geöffnet. Wenn für Ihre Bereitstellung erforderlich ist, klicken Sie auf, um die Auswahl aufzuheben **Zugriffsbereich vom übergeordneten Element erben**. In **auswählen des Zugriffsbereichs**, wählen Sie ein Element aus, und klicken Sie dann auf **OK**.  
  
    ![Wählen Sie den Zugriffsbereich](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  Stellen Sie sicher, dass auf der Zugriffsbereich für die Zone geändert wird, im Bereich IPAM Client Console anzeigen.  
  
    ![Stellen Sie sicher, dass auf der Zugriffsbereich für die Zone geändert wird](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffssteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


