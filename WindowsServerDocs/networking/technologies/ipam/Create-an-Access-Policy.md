---
title: Erstellen einer Zugriffsrichtlinie
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 807f02387a64a26ed8b1c58a387b165bece83168
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814813"
---
# <a name="create-an-access-policy"></a>Erstellen einer Zugriffsrichtlinie

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um eine Zugriffs Richtlinie in der IPAM-Client Konsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
> [!NOTE]  
> Sie können in Active Directory eine Zugriffs Richtlinie für einen bestimmten Benutzer oder eine Benutzergruppe erstellen. Wenn Sie eine Zugriffs Richtlinie erstellen, müssen Sie entweder eine integrierte IPAM-Rolle oder eine benutzerdefinierte Rolle auswählen, die Sie erstellt haben. Weitere Informationen zu benutzerdefinierten Rollen finden Sie unter [Erstellen einer Benutzerrolle für Access Control](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md).  
  
### <a name="to-create-an-access-policy"></a>So erstellen Sie eine Zugriffs Richtlinie  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich auf **Zugriffs Steuerung**. Klicken Sie im unteren Navigationsbereich mit der rechten Maustaste auf **Zugriffsrichtlinien**, und klicken Sie dann auf **Zugriffs Richtlinie hinzufügen**.  
  
    ![Zugriffs Richtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  Das Dialogfeld **Zugriffs Richtlinie hinzufügen** wird geöffnet. Klicken Sie unter **Benutzereinstellungen**auf **Hinzufügen**.  
  
    ![Zugriffs Richtlinie hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  Das Dialogfeld **Benutzer oder Gruppe auswählen** wird geöffnet. Klicken Sie auf **Standorte**.  
  
    ![Benutzer-oder Gruppen Standorte](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  Das Dialogfeld Speicher **Orte** wird geöffnet. Navigieren Sie zu dem Speicherort, der das Benutzerkonto enthält, wählen Sie den Speicherort aus, und klicken Sie dann auf **OK**. Das Dialogfeld Speicher **Orte** wird geschlossen.  
  
    ![Speicherort auswählen](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  Geben Sie im Dialogfeld **Benutzer oder Gruppe auswählen** unter **Geben Sie die zu**erstellenden Objektnamen ein den Namen des Benutzerkontos ein, für das Sie eine Zugriffs Richtlinie erstellen möchten. Klicken Sie auf **OK**.  
  
7.  Unter **Zugriffs Richtlinie hinzufügen**unter **Benutzereinstellungen**enthält **Benutzeralias** jetzt das Benutzerkonto, für das die Richtlinie gilt. Klicken Sie unter **Zugriffs Einstellungen**auf **neu**.  
  
    ![Neue Zugriffs Einstellung](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  In **Zugriffs Richtlinie hinzufügen**ändert sich die Einstellung **Zugriffs Einstellungen** in **neue Einstellung**.  
  
    ![Dialog Feld Name in neue Einstellung ändern](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. Klicken Sie auf **Rolle auswählen** , um die Liste der Rollen zu erweitern. Wählen Sie eine der integrierten Rollen aus, oder wählen Sie, wenn Sie neue Rollen erstellt haben, eine der Rollen aus, die Sie erstellt haben. Wenn Sie z. b. die ipamsrv-Rolle erstellt haben, die für den Benutzer gelten soll, klicken Sie auf **ipamsrv**.  
  
    ![Rolle auswählen](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. Klicken Sie auf **Einstellung hinzufügen**.  
  
    ![Neue Einstellung hinzufügen](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. Die Rolle wird der Zugriffs Richtlinie hinzugefügt. Um zusätzliche Zugriffsrichtlinien zu erstellen, **Klicken Sie**auf übernehmen, und wiederholen Sie dann diese Schritte für jede Richtlinie, die Sie erstellen möchten. Wenn Sie keine weiteren Richtlinien erstellen möchten, klicken Sie auf **OK**.  
  
    ![Klicken Sie auf anwenden oder OK.](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. Überprüfen Sie im Anzeigebereich der IPAM-Client Konsole, ob die neue Zugriffs Richtlinie erstellt wurde.  
  
    ![Anzeigen der neuen Zugriffs Richtlinie](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>Weitere Informationen  
[Rollenbasierte Access Control](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


