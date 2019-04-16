---
title: Erstellen der BranchCache-Dateiserver-Organisationseinheit
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a92cb3110e4aecb1ef09a45ed14173305722c655
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Erstellen der BranchCache-Dateiserver-Organisationseinheit

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahren können zum Erstellen einer Organisationseinheit (OU) in Active Directory-Domänendienste (AD DS) für BranchCache-Dateiserver.  
  
Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Zum Erstellen der BranchCache Dateiserver-Organisationseinheit  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS wird, wird im Server-Manager installiert, auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Klicken Sie in der Konsole Active Directory-Benutzer und -Computer auf der Domäne, zu der Sie eine Organisationseinheit hinzufügen möchten. Beispielsweise, wenn Ihre Domäne example.com benannt wird, mit der rechten Maustaste **example.com**. Zeigen Sie auf **neu**, und klicken Sie dann auf **Organisationseinheit**. Die **neues Objekt – Organisationseinheit** Dialogfeld wird geöffnet.  
  
3.  In der **neues Objekt – Organisationseinheit** Dialogfeld **Namen**, geben Sie einen Namen für die neue Organisationseinheit. Geben Sie beispielsweise, wenn Sie die Organisationseinheit BranchCache-Dateiservern benennen möchten, **BranchCache-Dateiservern**, und klicken Sie dann auf **OK**.  
  


