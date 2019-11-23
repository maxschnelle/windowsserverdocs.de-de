---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: Installieren des Verbundserver-Rollendiensts
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 73c564e1c1117b229f759ca114b18a2d4c8002fa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408385"
---
# <a name="install-the-federation-service-role-service"></a>Installieren des Verbundserver-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und Zertifikaten ordnungsgemäß konfiguriert haben, können Sie den Verbunddienst-Rollen Dienst Active Directory-Verbunddienste (AD FS) \(AD FS\)installieren. Wenn Sie die Verbunddienst auf einem Computer installieren, wird dieser Computer zu einem Verbund Server.  
  
> [!NOTE]  
> Für den Verbund-SSO-\-Sign\-on \(SSO\) Design müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Mithilfe des folgenden Verfahrens können Sie den Verbunddienst-Rollen Dienst von AD FS auf einem Computer installieren, der als erster Verbund Server oder auf einem Computer, der als Verbund Server für eine vorhandene Verbund Serverfarm verwendet wird, verwendet werden soll.  
  
## <a name="prerequisites"></a>Voraussetzungen  
Vergewissern Sie sich, dass ein SSL-Zertifikat mit dem privaten Schlüssel bereits installiert oder in den lokalen Zertifikat Speicher \(persönlichen Speicher\) importiert wurde, bevor Sie mit diesem Verfahren beginnen. Wenn Sie ein Token\-Signaturzertifikat verwenden, das von einer Zertifizierungsstelle \(ca-\)ausgestellt wird, überprüfen Sie, ob ein Token\-Signaturzertifikat mit dem privaten Schlüssel bereits installiert oder in den lokalen Zertifikat Speicher \(persönlichen Speicher importiert wurde, bevor Sie mit diesem Verfahren beginnen.\) Als Alternative können Sie mithilfe des Assistenten zum Hinzufügen von Rollen ein selbst\-signiertes Token\-Signaturzertifikat erstellen, wie in diesem Verfahren beschrieben. Weitere Informationen zu Token\-Signatur Zertifikaten finden Sie unter [Zertifikat Anforderungen für Verbund Server](https://technet.microsoft.com/library/dd807040.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
#### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst  
  
1.  Geben Sie auf dem **Start** Bildschirm**Server-Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **Verwalten**und dann auf **Rollen und Features hinzufügen** , um den Assistenten zum Hinzufügen von Rollen und Features zu starten.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollen\-basiert oder Feature\-basierte Installation**, und klicken Sie auf **weiter**.  
  
5.  Klicken Sie auf der Seite **Zielserver auswählen** auf **einen Server aus dem Server Pool auswählen**, überprüfen Sie, ob der Zielcomputer hervorgehoben ist, und klicken Sie dann auf **weiter**.  
  
6.  Klicken Sie auf der Seite **Server Rollen auswählen** auf **Active Directory-Verbunddienste (AD FS)** , und klicken Sie dann auf Weiter.  
  
    > [!NOTE]  
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework-oder Windows Process Activation Service-Features zu installieren, klicken Sie auf **Features hinzufügen** , um Sie zu installieren.  
  
7.  Überprüfen Sie auf der Seite **Features auswählen** , ob die Features festgelegt sind, und klicken Sie dann auf **weiter**.  
  
8.  Klicken Sie auf der Seite **Active Directory Verbunddienst \(AD FS\)** auf **weiter**.  
  
9. Aktivieren Sie auf der Seite **Rollen Dienste auswählen** das Kontrollkästchen **Verbunddienst** , und klicken Sie dann auf **weiter**.  
  
10. Klicken Sie auf der Seite **Webserver Rolle \(IIS-\)** auf **weiter**.  
  
11. Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.  
  
12. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten** , und klicken Sie dann auf **Installieren**.  
  
13. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  
  

