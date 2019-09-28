---
title: Erstellen einer Benutzerrolle für die Zugriffssteuerung
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 01e3216ca62cdb780342b477e575e00cdeedc6dd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405704"
---
# <a name="create-a-user-role-for-access-control"></a>Erstellen einer Benutzerrolle für die Zugriffssteuerung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um eine neue Access Control Benutzerrolle in der IPAM-Client Konsole zu erstellen.  
  
Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.  
  
> [!NOTE]  
> Nachdem Sie eine Rolle erstellt haben, können Sie eine Zugriffs Richtlinie erstellen, um die Rolle einem bestimmten Benutzer oder einer Active Directory Gruppe zuzuweisen. Weitere Informationen finden Sie unter [Erstellen einer Zugriffs Richtlinie](../../technologies/ipam/Create-an-Access-Policy.md).  
  
### <a name="to-create-a-role"></a>So erstellen Sie eine Rolle  
  
1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.  
  
2.  Klicken Sie im Navigationsbereich auf **Zugriffs Steuerung**, und klicken Sie im unteren Navigationsbereich auf **Rollen**.  
  
    ![Zugriffs Steuerungs Rollen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  Klicken Sie mit der rechten Maustaste auf **Rollen**und dann auf **Benutzerrolle hinzufügen**.  
  
    ![Benutzerrolle hinzufügen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  Das Dialogfeld **Rolle hinzufügen oder bearbeiten** wird geöffnet. Geben Sie unter **Name**einen Namen für die Rolle ein, mit der die Rollen Funktion eindeutig ist. Wenn Sie z. b. eine Rolle erstellen möchten, die es Administratoren ermöglicht, DNS-SRV-Ressourcen Einträge zu verwalten, können Sie der Rolle den Namen **ipamsrv**geben. Scrollen Sie bei Bedarf in den **Vorgängen** nach unten, um den Typ der Vorgänge zu suchen, die Sie für die Rolle definieren möchten. Führen Sie für dieses Beispiel einen Bildlauf nach unten zu den **Verwaltungs Vorgängen für DNS-Ressourcen**  
  
    ![Vorgänge zur Verwaltung von DNS-Ressourcen Einträgen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  Erweitern Sie **DNS-Ressourcen Daten Satz Verwaltung**, und suchen Sie dann nach **SRV-Daten Satz Vorgängen**.  
  
    ![SRV-Daten Satz Vorgänge](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  Erweitern und wählen Sie **SRV-Daten Satz Vorgänge**aus, und klicken Sie dann auf **OK**.  
  
    ![SRV-Daten Satz Vorgänge auswählen](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  Klicken Sie in der IPAM-Client Konsole auf die soeben erstellte Rolle. In der **Detailansicht** werden die zulässigen Vorgänge für die Rolle angezeigt.  
  
    ![Neue Rollen Details](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>Siehe auch  
[Rollenbasierte Access Control](Role-based-Access-Control.md)  
[Verwalten von IPAM](Manage-IPAM.md)  
  


