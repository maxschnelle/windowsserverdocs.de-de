---
title: Verschieben von Dateiservern in die Organisationseinheit mit den BranchCache-Dateiservern
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 037b354bb6725ac7f91fc323b81bbdf15d03ac15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885901"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Verschieben von Dateiservern in die Organisationseinheit mit den BranchCache-Dateiservern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, BranchCache-Dateiserver zu einer Organisationseinheit (OU) hinzufügen, in Active Directory Domain Services (AD DS).  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Sie müssen zuerst eine Organisationseinheit mit BranchCache-Dateiservern in der Konsole Active Directory-Benutzer und -Computer erstellen, bevor Sie der Organisationseinheit mit diesem Verfahren Computerkonten hinzufügen können. Weitere Informationen finden Sie unter [Erstellen der BranchCache Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md).  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Zum Verschieben der Datei Dateiserver, die BranchCache-Organisationseinheit  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS wird, wird im Server-Manager installiert, auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Suchen Sie in der Konsole Active Directory-Benutzer und -Computer das Computerkonto für BranchCache-Dateiserver, wählen Sie es mit der linken Maustaste aus, und ziehen Sie es dann mithilfe von Drag &amp; Drop in die Organisationseinheit mit den BranchCache-Dateiservern, die Sie zuvor erstellt haben. Angenommen, eine Organisationseinheit mit dem Namen, das Sie zuvor erstellt haben **BranchCache-Dateiservern**Drag & drop das Computerkonto für den **BranchCache-Dateiservern** Organisationseinheit.  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden BranchCache-Dateiserver in der Domäne, die Sie für die Organisationseinheit verschieben möchten.  
  


