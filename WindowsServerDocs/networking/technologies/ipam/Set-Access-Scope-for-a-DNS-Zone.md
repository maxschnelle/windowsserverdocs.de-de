---
title: Festlegen des Zugriffsbereichs für eine DNS-Zone
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6155cee3f1924486f1358632dcef2fba7046edb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355125"
---
# <a name="set-access-scope-for-a-dns-zone"></a>Festlegen des Zugriffsbereichs für eine DNS-Zone

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Client Konsole den Zugriffs Bereich für eine DNS-Zone festlegen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>So legen Sie den Zugriffs Bereich für eine DNS-Zone fest  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**. Klicken Sie im Anzeigebereich mit der rechten Maustaste auf die DNS-Zone, für die Sie den Zugriffs Bereich ändern möchten. Klicken Sie dann auf **Zugriffs Bereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  Das Dialogfeld **Zugriffs Bereich festlegen** wird geöffnet. Wenn dies für Ihre Bereitstellung erforderlich ist, klicken Sie hierauf, um die Auswahl **des Zugriffsbereichs des übergeordneten** Wählen Sie unter **Zugriffs Bereich auswählen**ein Element aus, und klicken Sie dann auf **OK**.  
  
    ![Zugriffs Bereich auswählen](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  Überprüfen Sie im Anzeigebereich der IPAM-Client Konsole, ob der Zugriffs Bereich für die Zone geändert wurde.  
  
    ![Überprüfen Sie, ob der Zugriffs Bereich für die Zone geändert wurde.](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Access Control](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


