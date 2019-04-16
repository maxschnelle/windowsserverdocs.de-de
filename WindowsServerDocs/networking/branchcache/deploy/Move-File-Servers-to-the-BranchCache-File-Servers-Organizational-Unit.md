---
title: Verschieben von Dateiservern in die BranchCache-Dateiserver-Organisationseinheit
description: In diesem Thema ist Teil der BranchCache Deployment Guide für Windows Server 2016, der veranschaulicht, wie Sie BranchCache im verteilten und gehosteter cachemodi zum Optimieren der WAN-Bandbreite in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 09afb4936545cb1f5bb14573261008ff18badd4d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Verschieben von Dateiservern in die BranchCache-Dateiserver-Organisationseinheit

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahren können Hinzufügen von BranchCache-Dateiservern mit einer Organisationseinheit (OU) in Active Directory-Domänendienste (AD DS).  
  
Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe die mindestvoraussetzung, um dieses Verfahren auszuführen.  
  
> [!NOTE]  
> Bevor Sie die Organisationseinheit mit diesem Verfahren Computerkonten hinzufügen, müssen Sie einen BranchCache-Dateiservern Organisationseinheit in der Konsole Active Directory-Benutzer und-Computer erstellen. Weitere Informationen finden Sie unter [Erstellen der BranchCache Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md).  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Zum Verschieben der Datei Dateiserver mit den BranchCache-Organisationseinheit  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS wird, wird im Server-Manager installiert, auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Suchen Sie in der Konsole Active Directory-Benutzer und-Computer das Computerkonto für BranchCache-Dateiserver, mit der linken Maustaste, wählen Sie das Konto, und klicken Sie dann Drag & drop das Computerkonto auf den BranchCache-Dateiservern Organisationseinheit, die Sie zuvor erstellt haben. Beispielsweise, wenn Sie zuvor eine Organisationseinheit Namens erstellt haben **BranchCache-Dateiservern**, Drag & drop das Computerkonto auf dem **BranchCache-Dateiservern** Organisationseinheit.  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden BranchCache-Dateiserver in der Domäne, die Sie auf die Organisationseinheit verschieben möchten.  
  


