---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: Installieren des Verbundserverproxy-Rollendiensts
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6e78c52f1928a3401c0532ab7c25616b012a1d8b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192101"
---
# <a name="install-the-federation-service-proxy-role-service"></a>Installieren des Verbundserverproxy-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und die Zertifikate konfigurieren, sind Sie bereit zum Installieren des Verbunddienstproxy-Rollendienst, der Active Directory Federation Services \(AD FS\). Sie können das folgende Verfahren verwenden, den Verbunddienstproxy-Rollendienst installieren. Wenn Sie die Verbunddienstproxy-Rollendienst auf einem Computer installieren, wird dieser Computer einen Verbundserverproxy.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>So installieren Sie die Verbunddienstproxy-Rollendienst, der mit dem Server-Manager
  
1.  Auf der **starten** geben**Server-Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features** zum Hinzufügen von Rollen und Features-Assistenten zu starten.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Auf der **Installationstyp** auf **Rolle\-oder featurebasierte\-basierten Installation**, und klicken Sie auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer wird hervorgehoben, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **RAS**, und klicken Sie dann auf Weiter.  
  
    > [!NOTE]  
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework- oder Windows Process Activation Service-Funktionen zu installieren, klicken Sie auf **Features hinzufügen** , diese zu installieren.  
  
7. Auf der **Rollendienste auswählen** Seite die **Federation Service Proxy** , und klicken Sie dann auf **Weiter**.  

8. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten** , und klicken Sie dann auf **Installieren**.  
  
13. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>So installieren Sie die Verbunddienstproxy-Rollendienst, der mithilfe von PowerShell

1. Öffnen Sie Windows PowerShell (als Administrator ausführen)

2. Geben Sie den folgenden Befehl und drücken Sie **EINGABETASTE**:

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

