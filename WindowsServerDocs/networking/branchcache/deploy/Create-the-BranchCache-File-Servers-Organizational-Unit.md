---
title: Erstellen der BranchCache-Dateiserver-Organisationseinheit
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f058dbec42997f22106666b014508191a8861694
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406488"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Erstellen der BranchCache-Dateiserver-Organisationseinheit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie eine Organisationseinheit (OU) in Active Directory Domain Services (AD DS) für BranchCache-Dateiserver erstellen.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>So erstellen Sie die Organisationseinheit "BranchCache-Dateiserver"  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS installiert ist, in Server-Manager auf **Extras, und**klicken Sie dann auf **Active Directory Benutzer und Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Klicken Sie in der Konsole Active Directory-Benutzer und -Computer mit der rechten Maustaste auf die Domäne, der Sie eine Organisationseinheit hinzufügen möchten. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie mit der rechten Maustaste auf **beispiel.com**. Zeigen Sie auf **Neu**, und klicken Sie dann auf **Organisationseinheit**. Das Dialogfeld **Neues Objekt-Organisationseinheit** wird geöffnet.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt-Organisationseinheit** unter **Name**einen Namen für die neue Organisationseinheit ein. Wenn Sie die Organisationseinheit beispielsweise „BranchCache-Dateiserver“ nennen möchten, geben Sie **BranchCache-Dateiserver** ein, und klicken dann auf **OK**.  
  


