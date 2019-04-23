---
title: Erstellen der BranchCache-Dateiserver-Organisationseinheit
description: Dieses Thema ist Teil von BranchCache Deployment Guide für Windows Server 2016, die veranschaulicht, wie Sie BranchCache in verteilter und gehosteter Cachemodus zur Optimierung der WAN-bandbreitennutzung in Zweigstellen bereitstellen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b7b26ec5808f5b11141e81dc5e738c83c94ef6b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874081"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Erstellen der BranchCache-Dateiserver-Organisationseinheit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, zum Erstellen einer Organisationseinheit (OU), in Active Directory Domain Services (AD DS) für BranchCache-Dateiserver.  
  
Für dieses Verfahren müssen Sie mindestens Mitglied der Gruppe **Domänen-Admins** oder einer gleichwertigen Gruppe sein.  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Um die BranchCache Dateiserver-Organisationseinheit zu erstellen.  
  
1.  Klicken Sie auf einem Computer, auf dem AD DS wird, wird im Server-Manager installiert, auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.  
  
2.  Klicken Sie in der Konsole Active Directory-Benutzer und -Computer mit der rechten Maustaste auf die Domäne, der Sie eine Organisationseinheit hinzufügen möchten. Wenn Ihre Domäne beispielsweise den Namen „beispiel.com“ besitzt, klicken Sie mit der rechten Maustaste auf **beispiel.com**. Zeigen Sie auf **Neu**, und klicken Sie dann auf **Organisationseinheit**. Die **neues Objekt – Organisationseinheit** Dialogfeld wird geöffnet.  
  
3.  In der **neues Objekt – Organisationseinheit** Dialogfeld **Namen**, geben Sie einen Namen für die neue Organisationseinheit. Wenn Sie die Organisationseinheit beispielsweise „BranchCache-Dateiserver“ nennen möchten, geben Sie **BranchCache-Dateiserver** ein, und klicken dann auf **OK**.  
  


