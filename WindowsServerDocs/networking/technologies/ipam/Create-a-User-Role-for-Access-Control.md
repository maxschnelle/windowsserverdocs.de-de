---
title: Erstellen einer Benutzerrolle für die Zugriffssteuerung
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
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa0ed71d399ad638a648946952fe170d93f69ceb
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-user-role-for-access-control"></a>Erstellen einer Benutzerrolle für die Zugriffssteuerung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie um eine neue Benutzerrolle für die Steuerung des Zugriffs in der IPAM-Clientkonsole erstellen.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Nachdem Sie eine Rolle erstellt haben, können Sie eine Zugriffsrichtlinie zum Zuweisen der Rolle an einen bestimmten Benutzer oder die Active Directory-Gruppe erstellen. Weitere Informationen finden Sie unter [Erstellen einer Zugriffsrichtlinie](../../technologies/ipam/Create-an-Access-Policy.md).  
  
### <a name="to-create-a-role"></a>Um eine Rolle zu erstellen.  
  
1.  Klicken Sie im Server-Manager auf **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **ZUGRIFFSSTEUERUNG**, und klicken Sie im unteren Navigationsbereich, klicken Sie auf **Rollen**.  
  
    ![Zugriffssteuerungsrollen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  Mit der rechten Maustaste **Rollen**, und klicken Sie dann auf **Benutzerrolle hinzufügen**.  
  
    ![Benutzerrolle hinzufügen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  Die **hinzufügen oder bearbeiten Rolle** Dialogfeld wird geöffnet. In **Namen**, geben Sie einen Namen für die Rolle, die die Funktion löschen kann. Z.B., wenn eine Rolle zu erstellen, die Administratoren die Verwaltung von DNS-SRV-Ressourceneinträge gestattet werden soll, Sie möglicherweise den Namen der Rolle **IPAMSrv**. Bei Bedarf einen Bildlauf im **Operations** Art der Vorgänge finden Sie für die Rolle definieren möchten. In diesem Beispiel einen Bildlauf nach unten zu **DNS-Resource Record Verwaltungsvorgänge**.  
  
    ![DNS-Resource Record Verwaltungsvorgänge](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  Erweitern Sie **DNS-Resource Record Verwaltungsvorgänge**, und suchen Sie **SRV-Datensatz Operations**.  
  
    ![SRV-Datensatz operations](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  Erweitern und wählen Sie **SRV-Datensatz Operations**, und klicken Sie dann auf **OK**.  
  
    ![Wählen Sie SRV-Datensatz operations](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  Klicken Sie in der IPAM-Clientkonsole auf die Rolle, die Sie gerade erstellt haben. In **Ansicht mit Detail zur** werden die zulässigen Vorgänge für die Rolle angezeigt.  
  
    ![Neue Rollendetails](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffsteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


