---
title: Löschen von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a5658e53aebf9f6fa20a5de9f3f7cb5a0287b408
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860673"
---
# <a name="delete-dns-resource-records"></a>Löschen von DNS-Ressourceneinträgen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema können Sie mithilfe der IPAM-Client Konsole einen oder mehrere DNS-Ressourcen Einträge löschen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
### <a name="to-delete-dns-resource-records"></a>So löschen Sie DNS-Ressourcen Einträge  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich unter **überwachen und verwalten**auf **DNS-Zonen**.  Der Navigationsbereich gliedert sich in einen oberen Navigationsbereich und einen niedrigeren Navigationsbereich.  
  
3.  Klicken Sie, um **Forward-Lookup** und die Domäne zu erweitern, in der sich die zu löschenden Zonen-und Ressourcen Einträge befinden. Klicken Sie auf die Zone, und klicken Sie im Anzeigebereich auf **Aktuelle Ansicht**. Klicken Sie auf **Ressourcen Einträge**.  
  
4.  Suchen Sie im Anzeigebereich die Ressourcen Einträge, die Sie löschen möchten, und wählen Sie Sie aus.  
  
    ![Zu löschende Ressourcen Einträge auswählen](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  Klicken Sie mit der rechten Maustaste auf die ausgewählten Einträge, und klicken Sie dann auf **DNS-Ressourcen Eintrag löschen**.  
  
    ![Löschen der Datensätze](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  Das Dialogfeld **DNS-Ressourcen Daten Satz löschen** wird geöffnet. Vergewissern Sie sich, dass der richtige DNS-Server ausgewählt ist. Wenn dies nicht der Fall ist, klicken Sie auf **DNS-Server** , und wählen Sie den Server aus, auf dem Sie die Ressourcen Einträge löschen möchten. Klicken Sie auf **OK**. IPAM löscht die Ressourcen Einträge vom DNS-Server.  
  
    ![Überprüfen, ob der richtige DNS-Server ausgewählt ist, und Datensätze löschen](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[Verwaltung von DNS-Ressourcen Einträgen](DNS-Resource-Record-Management.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


