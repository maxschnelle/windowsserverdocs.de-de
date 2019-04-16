---
title: Erstellen einer Zugriffsrichtlinie
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
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ac8229952c7e038f9af8fc4f9287b1821db887ac
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-access-policy"></a>Erstellen einer Zugriffsrichtlinie

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie um eine Zugriffsrichtlinie in der IPAM-Clientkonsole erstellen.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Sie können eine Zugriffsrichtlinie für einen bestimmten Benutzer oder eine Benutzergruppe in Active Directory erstellen. Wenn Sie eine Richtlinie erstellen, müssen Sie auswählen, eine integrierte Rolle und IPAM oder eine benutzerdefinierte Funktion, die Sie erstellt haben. Weitere Informationen zu benutzerdefinierten Rollen finden Sie unter [Erstellen einer Benutzerrolle für die Zugriffssteuerung](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md).  
  
### <a name="to-create-an-access-policy"></a>Erstellen eine Zugriffsrichtlinie  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **ZUGRIFFSSTEUERUNG**. Klicken Sie im unteren Navigationsbereich, mit der rechten Maustaste **Zugriffsrichtlinien**, und klicken Sie dann auf **Richtlinie hinzufügen**.  
  
    ![Zugriffsrichtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  Die **Richtlinie hinzufügen** Dialogfeld wird geöffnet. In **Benutzereinstellungen**, klicken Sie auf **hinzufügen**.  
  
    ![Zugriffsrichtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  Die **Benutzer oder Gruppe auswählen** Dialogfeld wird geöffnet. Klicken Sie auf **Speicherorte**.  
  
    ![Benutzer oder Gruppe Speicherorte](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  Die **Speicherorte** Dialogfeld wird geöffnet. Navigieren Sie zu dem Speicherort, an dem Benutzerkonto an, wählen Sie den Speicherort und klicken Sie dann auf **OK**. Die **Speicherorte** Dialogfeld geschlossen wird.  
  
    ![Speicherort auswählen](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie die zu verwendenden Objektnamen ein**, geben Sie den Kontonamen des Benutzers für die Sie eine Richtlinie erstellen möchten. Klicken Sie auf **OK**.  
  
7.  In **Richtlinie hinzufügen**im **Benutzereinstellungen**, **Benutzeralias** enthält jetzt das Benutzerkonto, dem die Richtlinie angewendet wird. In **Zugriffseinstellungen**, klicken Sie auf **neu**.  
  
    ![Neue Einstellung](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  In **Richtlinie hinzufügen**, **Zugriffseinstellungen** ändert sich in **neue Einstellung**.  
  
    ![Dialogfeld den Namen ändern, um die neue Einstellung](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. Klicken Sie auf **Rolle auswählen** um die Liste der Rollen zu erweitern. Wählen Sie eine der integrierten Rollen oder, wenn Sie neue Rollen erstellt haben, wählen Sie eine der Rollen, die Sie erstellt haben. Wenn beispielsweise Sie die IPAMSrv Rolle für den Benutzer gelten erstellt haben, klicken Sie auf **IPAMSrv**.  
  
    ![Wählen Sie Rolle](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. Klicken Sie auf **Einstellung hinzufügen**.  
  
    ![Fügen Sie neue Einstellung](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. Die Richtlinie wird die Rolle hinzugefügt. Um weitere Richtlinien zu erstellen, klicken Sie auf **übernehmen**, und wiederholen Sie diese Schrittefür jede Richtlinie, die Sie erstellen möchten. Wenn Sie keine weiteren Richtlinien erstellen möchten, klicken Sie auf **OK**.  
  
    ![Klicken Sie auf Anwenden oder OK](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. Klicken Sie im IPAM Client Console Anzeigebereich stellen Sie sicher, dass die neue Richtlinie erstellt wird.  
  
    ![Die neue Richtlinie anzeigen](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffsteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


