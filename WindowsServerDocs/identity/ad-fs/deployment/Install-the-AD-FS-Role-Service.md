---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: Installieren des AD FS-Rollendiensts
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9851134d1ad73092ee44c34c99bc2d873d20ca07
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-ad-fs-role-service"></a>Installieren des AD FS-Rollendiensts

>Gilt für: Windows Server 2016, Windows Server2012 R2

Das folgende Verfahren können die AD FS-Rollendiensts auf einem Computer installieren, auf denen Windows Server 2012 R2 zu den ersten Verbundserver in einer Verbundserverfarm oder einen Verbundserver in einer vorhandenen Verbundserverfarm ausgeführt wird.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>So installieren Sie die AD FS-Serverrolle über den Assistenten zum Hinzufügen von Rollen und features  
  
1.  Öffnen Sie Server-Manager. Klicken Sie zum Öffnen des Server-Managers auf **Server-Manager** auf die **starten** Bildschirm oder **Server-Manager** auf der Taskleiste auf dem Desktop. In der **Quick Start** auf der Registerkarte der **Willkommen** Kachel auf der **Dashboard** auf **Hinzufügen von Rollen und Features**. Alternativ können Sie klicken **Hinzufügen von Rollen und Features** auf die **verwalten** Menü.  
  
2.  Auf der **vor dem Beginn** auf **Weiter**.  
  
3.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Serverrollen auswählen** auf **Active Directory Federation Services**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Features auswählen** auf **Weiter**. Die erforderlichen Komponenten sind bereits für Sie ausgewählt werden. Sie müssen keine anderen Features zu aktivieren.  
  
7.  Auf der **Active Directory-Verbunddienste \(AD FS\)** auf **Weiter**.  
  
8.  Nachdem Sie die Informationen überprüfen, die sich auf die **Installationsauswahl bestätigen** auf **installieren**.  
  
9. Auf der **Installationsstatus** Seite, stellen Sie sicher, dass alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **schließen**.  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>So installieren Sie die AD FS-Serverrolle über Windows PowerShell  
  
1.  Auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl: `Install-windowsfeature adfs-federation –IncludeManagementTools`.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

