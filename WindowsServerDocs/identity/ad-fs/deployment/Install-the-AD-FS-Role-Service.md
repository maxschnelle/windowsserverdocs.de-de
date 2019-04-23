---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: Installieren des AD FS-Rollendiensts
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9851134d1ad73092ee44c34c99bc2d873d20ca07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831171"
---
# <a name="install-the-ad-fs-role-service"></a>Installieren des AD FS-Rollendiensts

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Sie können das folgende Verfahren verwenden, auf den AD FS-Rollendienst auf einem Computer installieren, auf denen Windows Server 2012 R2 zu den ersten Verbundserver in einer Verbundserverfarm oder einen Verbundserver in einer vorhandenen Verbundserverfarm ausgeführt wird.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden, auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>So installieren Sie die AD FS-Serverrolle über den Assistenten zum Hinzufügen von Rollen und features  
  
1.  Öffnen Sie den Server-Manager. Klicken Sie zum Öffnen des Server-Managers auf **Server-Manager** auf die **starten** Bildschirm oder **Server-Manager** in der Taskleiste auf dem Desktop. Klicken Sie auf der Seite **Dashboard** auf der Kachel für **Willkommen** auf der Registerkarte **Schnellstart** auf **Rollen und Features hinzufügen**. Alternativ können Sie im Menü **Verwalten** auf **Rollen und Features hinzufügen** klicken.  
  
2.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
3.  Auf der **Installationstyp** auf **Rolle\-oder featurebasierte\-basierten Installation**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite  **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, überprüfen Sie, ob der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Verbunddienste**, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Features auswählen** auf **Weiter**. Die erforderlichen Komponenten sind für Sie vorausgewählt. Sie müssen keine weiteren Features auswählen.  
  
7.  Auf der **Active Directory Federation Service \(AD FS\)**  auf **Weiter**.  
  
8.  Nachdem Sie die Informationen überprüfen, die sich auf die **Installationsauswahl bestätigen** auf **installieren**.  
  
9. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>So installieren Sie die AD FS-Serverrolle mithilfe von Windows PowerShell  
  
1.  Klicken Sie auf dem Computer, die Sie als Verbundserver konfigurieren möchten, öffnen Sie Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl: `Install-windowsfeature adfs-federation –IncludeManagementTools`.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

