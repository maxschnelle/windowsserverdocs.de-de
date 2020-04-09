---
title: Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 613796c933498d104db4895733c9a9b1957cb952
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860613"
---
# <a name="set-access-scope-for-dns-resource-records"></a>Festlegen des Zugriffsbereichs für DNS-Ressourceneinträge

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

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
  
## <a name="see-also"></a>Weitere Informationen  
[Rollenbasierte Access Control](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


