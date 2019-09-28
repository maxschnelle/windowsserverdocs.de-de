---
title: Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b1790f2cbf84fd68f33ca30d2fe7663dde824240
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405643"
---
# <a name="set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Client Konsole den Zugriffs Bereich für DNS-Ressourcen Einträge festlegen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourcen Einträge  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich auf **DNS-Zonen**.  Erweitern Sie im unteren Navigationsbereich **Forward Lookup** , navigieren Sie zu der Zone, die die Ressourcen Einträge enthält, deren Zugriffs Bereich Sie ändern möchten, und wählen Sie Sie aus.  
  
3.  Suchen Sie im Anzeigebereich die Ressourcen Einträge, deren Zugriffs Bereich Sie ändern möchten, und wählen Sie Sie aus.  
  
    ![Ressourcen Einträge auswählen](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  Klicken Sie mit der rechten Maustaste auf die ausgewählten DNS-Ressourcen Einträge, und klicken Sie dann auf **Zugriffs Bereich festlegen**.  
  
    ![Zugriffsbereich festlegen](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  Das Dialogfeld **Zugriffs Bereich festlegen** wird geöffnet. Wenn dies für Ihre Bereitstellung erforderlich ist, klicken Sie hierauf, um die Auswahl **des Zugriffsbereichs des übergeordneten** Wählen Sie unter **Zugriffs Bereich auswählen**ein Element aus, und klicken Sie dann auf **OK**.  
  
    ![Zugriffs Bereich auswählen](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Access Control](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


