---
title: Erstellen einer Zugriffsrichtlinie
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3e72d47dc3c32db7465f7c47b16dcdc777636fd9
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282222"
---
# <a name="create-an-access-policy"></a>Erstellen einer Zugriffsrichtlinie

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, erstellen Sie eine Zugriffsrichtlinie in der IPAM-Clientkonsole.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
> [!NOTE]  
> Sie können eine Zugriffsrichtlinie für einen bestimmten Benutzer oder eine Benutzergruppe in Active Directory erstellen. Wenn Sie eine Zugriffsrichtlinie erstellen, müssen Sie auswählen, einer integrierten IPAM-Rolle oder eine benutzerdefinierte Rolle, die Sie erstellt haben. Weitere Informationen zu benutzerdefinierten Rollen finden Sie unter [Erstellen einer Benutzerrolle für die Zugriffssteuerung](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md).  
  
### <a name="to-create-an-access-policy"></a>Erstellen eine Zugriffsrichtlinie  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **ZUGRIFFSSTEUERUNG**. Im unteren Navigationsbereich, mit der Maustaste **Zugriffsrichtlinien**, und klicken Sie dann auf **Zugriffsrichtlinie hinzufügen**.  
  
    ![Zugriffsrichtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  Die **Zugriffsrichtlinie hinzufügen** Dialogfeld wird geöffnet. In **Benutzereinstellungen**, klicken Sie auf **hinzufügen**.  
  
    ![Zugriffsrichtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  Die **Benutzer oder Gruppe auswählen** Dialogfeld wird geöffnet. Klicken Sie auf **Speicherorte**.  
  
    ![Benutzer oder eine Gruppe von Standorten](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  Die **Speicherorte** Dialogfeld wird geöffnet. Navigieren Sie zum Speicherort, die dem Benutzerkonto aus, wählen Sie den Speicherort, und klicken Sie dann auf **OK**. Die **Speicherorte** Dialogfeld wird geschlossen.  
  
    ![Speicherort auswählen](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  In der **Benutzer oder Gruppe auswählen** Dialogfeld **Geben Sie den zu verwendenden Objektnamen**, geben Sie den Benutzerkontonamen, für die Sie eine Zugriffsrichtlinie erstellen möchten. Klicken Sie auf **OK**.  
  
7.  In **Zugriffsrichtlinie hinzufügen**im **Benutzereinstellungen**, **Benutzeralias** enthält jetzt das Benutzerkonto, das für die die Richtlinie gilt. In **Zugriffseinstellungen**, klicken Sie auf **neu**.  
  
    ![Neue Einstellung für den Zugriff](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  In **Zugriffsrichtlinie hinzufügen**, **Zugriffseinstellungen** Änderungen an **neue Einstellung**.  
  
    ![Dialogfeld den Namen ändern, um die neue Einstellung](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. Klicken Sie auf **; Rollendienste auswählen%** zum Erweitern der Liste der Rollen. Wählen Sie eine der integrierten Rollen oder, wenn Sie neue Rollen erstellt haben, wählen Sie eine der Rollen, die Sie erstellt haben. Z. B. Wenn Sie für den Benutzer gelten die IPAMSrv Rolle erstellt haben, klicken Sie auf **IPAMSrv**.  
  
    ![Rolle auswählen](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. Klicken Sie auf **Einstellung hinzufügen**.  
  
    ![Neue Einstellung hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. Die Rolle wird der Zugriffsrichtlinie hinzugefügt. Um zusätzliche Richtlinien zu erstellen, klicken Sie auf **übernehmen**, und wiederholen Sie diese Schritte für jede Richtlinie, die Sie erstellen möchten. Wenn Sie nicht, um zusätzliche Richtlinien zu erstellen möchten, klicken Sie auf **OK**.  
  
    ![Klicken Sie auf Anwenden oder ' OK '](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. Stellen Sie sicher, dass die neue Richtlinie erstellt wurde, im Bereich IPAM Client Console anzeigen.  
  
    ![Die neue Richtlinie anzeigen](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffssteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


