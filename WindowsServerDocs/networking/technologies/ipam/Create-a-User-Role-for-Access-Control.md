---
title: Erstellen einer Benutzerrolle für die Zugriffssteuerung
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
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
ms.openlocfilehash: 69d7acec19a460b51819bdc30ce40e21089c7bcf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823581"
---
# <a name="create-a-user-role-for-access-control"></a>Erstellen einer Benutzerrolle für die Zugriffssteuerung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um eine neue Benutzerrolle für die Zugriffssteuerung in der IPAM-Clientkonsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
> [!NOTE]  
> Nachdem Sie eine Rolle erstellt haben, können Sie eine Zugriffsrichtlinie zum Zuweisen der Rolle für einen bestimmten Benutzer oder die Active Directory-Gruppe erstellen. Weitere Informationen finden Sie unter [Erstellen einer Zugriffsrichtlinie](../../technologies/ipam/Create-an-Access-Policy.md).  
  
### <a name="to-create-a-role"></a>Zum Erstellen einer Rolle  
  
1.  Klicken Sie im Server-Manager **IPAM**. Die IPAM-Clientkonsole angezeigt wird.  
  
2.  Klicken Sie im Navigationsbereich auf **ZUGRIFFSSTEUERUNG**, und klicken Sie im unteren Navigationsbereich auf **Rollen**.  
  
    ![Zugriffssteuerungsrollen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  Mit der rechten Maustaste **Rollen**, und klicken Sie dann auf **Benutzerrolle hinzufügen**.  
  
    ![Benutzerrolle hinzufügen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  Die **hinzufügen oder Bearbeiten von Rolle** Dialogfeld wird geöffnet. In **Namen**, geben Sie einen Namen für die Rolle, mit der die Rolle-Funktion deaktivieren. Beispielsweise sollten Sie eine Rolle zu erstellen, die Administratoren zum Verwalten von DNS-SRV-Ressourceneinträge ermöglicht, Sie können benennen Sie die Rolle **IPAMSrv**. Bei Bedarf einen Bildlauf **Vorgänge** Arten von Vorgängen finden Sie für die Rolle definieren möchten. In diesem Beispiel führen Sie einen Bildlauf nach unten zum **DNS-datensatzverwaltung Ressourcenvorgänge**.  
  
    ![DNS-datensatzverwaltung Ressourcenvorgänge](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  Erweitern Sie **DNS-datensatzverwaltung Ressourcenvorgänge**, und suchen Sie dann **SRV-Datensatz Vorgänge**.  
  
    ![SRV-Datensatz-Vorgänge](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  Erweitern und auszuwählen, **SRV-Datensatz Vorgänge**, und klicken Sie dann auf **OK**.  
  
    ![SRV-Datensatz Vorgänge auswählen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  Klicken Sie in der IPAM-Clientkonsole auf die Rolle, die Sie gerade erstellt haben. In **Detailansicht** zulässigen Vorgänge für die Rolle werden angezeigt.  
  
    ![Rollendetails der neuen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Zugriffssteuerung](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


