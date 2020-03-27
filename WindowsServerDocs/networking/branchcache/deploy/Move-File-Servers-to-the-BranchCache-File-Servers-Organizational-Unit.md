---
title: Verschieben von Dateiservern in die Organisationseinheit mit den BranchCache-Dateiservern
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 045764f9ed7cb7eef5a996748e293b48ec6018fb
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319204"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Verschieben von Dateiservern in die Organisationseinheit mit den BranchCache-Dateiservern

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit diesem Verfahren können Sie BranchCache-Dateiserver einer Organisationseinheit (OE) in Active Directory Domain Services (AD DS) hinzufügen.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
> [!NOTE]  
> Sie müssen zuerst eine Organisationseinheit mit BranchCache-Dateiservern in der Konsole Active Directory-Benutzer und -Computer erstellen, bevor Sie der Organisationseinheit mit diesem Verfahren Computerkonten hinzufügen können. Weitere Informationen finden Sie unter [Erstellen der BranchCache-Dateiserver-Organisationseinheit](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md).  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>So verschieben Sie Dateiserver in die Organisationseinheit der BranchCache-Dateiserver  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS installiert ist, in Server-Manager auf **Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Suchen Sie in der Konsole Active Directory-Benutzer und -Computer das Computerkonto für BranchCache-Dateiserver, wählen Sie es mit der linken Maustaste aus, und ziehen Sie es dann mithilfe von Drag &amp; Drop in die Organisationseinheit mit den BranchCache-Dateiservern, die Sie zuvor erstellt haben. Wenn Sie z. b. zuvor eine Organisationseinheit mit dem Namen **BranchCache-Dateiserver**erstellt haben, ziehen Sie das Computer Konto in die Organisationseinheit für die **BranchCache-Dateiserver** .  
  
3.  Wiederholen Sie den vorherigen Schritt für jeden BranchCache-Dateiserver in der Domäne, die Sie in die Organisationseinheit verschieben möchten.  
  


