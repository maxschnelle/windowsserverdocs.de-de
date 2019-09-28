---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: Installieren des Verbundserverproxy-Rollendiensts
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1f66e863c28aea7c9214c8363328a103b0a92f06
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359567"
---
# <a name="install-the-federation-service-proxy-role-service"></a>Installieren des Verbundserverproxy-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und Zertifikaten konfiguriert haben, können Sie den Verbunddienstproxy-Rollen Dienst Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 installieren. Mit dem folgenden Verfahren können Sie den Verbunddienstproxy-Rollen Dienst installieren. Wenn Sie den Verbunddienstproxy-Rollen Dienst auf einem Computer installieren, wird dieser Computer zu einem Verbund Server Proxy.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>So installieren Sie den Verbunddienstproxy-Rollen Dienst mithilfe der Server-Manager
  
1.  Geben Sie auf dem **Start** Bildschirm**Server-Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **Verwalten**und dann auf **Rollen und Features hinzufügen** , um den Assistenten zum Hinzufügen von Rollen und Features zu starten.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rolle @ no__t-2based oder Feature @ no__t-3based Installation**, und klicken Sie auf **weiter**.  
  
5.  Klicken Sie auf der Seite **Zielserver auswählen** auf **einen Server aus dem Server Pool auswählen**, überprüfen Sie, ob der Zielcomputer hervorgehoben ist, und klicken Sie dann auf **weiter**.  
  
6.  Klicken Sie auf der Seite **Server Rollen auswählen** auf **Remote Zugriff**, und klicken Sie dann auf Weiter.  
  
    > [!NOTE]  
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework-oder Windows Process Activation Service-Features zu installieren, klicken Sie auf **Features hinzufügen** , um Sie zu installieren.  
  
7. Aktivieren Sie auf der Seite **Rollen Dienste auswählen** das Kontrollkästchen **Verbunddienstproxy** , und klicken Sie dann auf **weiter**.  

8. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten** , und klicken Sie dann auf **Installieren**.  
  
13. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>So installieren Sie den Verbunddienstproxy-Rollen Dienst mithilfe von PowerShell

1. Öffnen Sie Windows PowerShell (als Administrator ausführen).

2. Geben Sie den folgenden Befehl ein, und drücken **Sie Eingabe**:

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

