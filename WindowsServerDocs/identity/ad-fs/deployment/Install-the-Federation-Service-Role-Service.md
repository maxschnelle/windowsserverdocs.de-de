---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: Installieren Sie den Verbunddienst-Rollendienst
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c520cbe22739f2bde263e133c7feb681d824d251
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-federation-service-role-service"></a>Installieren Sie den Verbunddienst-Rollendienst

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nun, dass Sie einen Computer mit den erforderlichen Anwendungen und Zertifikate ordnungsgemäß konfiguriert haben, sind Sie bereit zum Installieren des Verbunddienst-Rollendiensts der Active Directory Federation Services \(AD FS\). Wenn Sie den Verbunddienst auf einem Computer installieren, wird diesem Computer eines Verbundservers.  
  
> [!NOTE]  
> Für den Federated-Web-Single\-Sign\-On \(SSO\)-Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation. Weitere Informationen finden Sie unter [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx).  
  
Das folgende Verfahren können so installieren Sie den Verbunddienst-Rollendienst von AD FS auf einem Computer, der den ersten Verbundserver verwendet werden sollen, oder auf einem Computer, der für einen vorhandenen Verbundserverfarm einen Verbundserver verwendet werden sollen.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Stellen Sie sicher, dass ein SSL-Zertifikat mit dem privaten Schlüssel bereits installiert oder in den Zertifikatspeicher Store \(Personal store\) importiert werden, bevor Sie mit diesem Verfahren beginnen. Wenn Sie ein Token\-Signaturzertifikat verwenden, die von einer Zertifizierungsstelle ausgestellt wird \(CA\), stellen Sie sicher, dass ein Token\-Signaturzertifikat mit dem privaten Schlüssel bereits installiert oder in den Zertifikatspeicher Store \(Personal store\) importiert werden, bevor Sie mit diesem Verfahren beginnen. Alternativ können Sie ein Zertifikat signierte mit deren Hilfe, Token\ signieren, die mithilfe des Assistenten zum Hinzufügen von Rollen erstellen, wie in diesem Verfahren beschrieben. Weitere Informationen zu Token\ Signieren von Zertifikaten finden Sie unter [Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx).  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
#### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst  
  
1.  Auf der **starten** geben**Server-Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features** zum Hinzufügen von Rollen und Features-Assistenten zu starten.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer markiert ist, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Federation Services**, und klicken Sie dann auf Weiter.  
  
    > [!NOTE]  
    > Wenn Sie aufgefordert werden, installieren Sie zusätzliche Funktionen von .NET Framework oder Windows-Prozessaktivierungsdienst, klicken Sie auf **Features hinzufügen** installiert.  
  
7.  Auf der **Features auswählen** sicher, dass die Funktionen festgelegt sind, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Active Directory-Verbunddienste \(AD FS\)** auf **Weiter**.  
  
9. Auf der **Rollendienste auswählen** Seite der **Verbunddienst** , und klicken Sie dann auf **Weiter**.  
  
10. Auf der **Webserverrolle \(IIS\)** auf **Weiter**.  
  
11. Auf der **Rollendienste auswählen** auf **Weiter**.  
  
12. Nachdem Sie die Informationen auf Überprüfen der **Installationsauswahl bestätigen** Seite auf die **Zielserver bei Bedarf automatisch neu** , und klicken Sie dann auf **installieren**.  
  
13. Auf der **Installationsstatus** Seite, stellen Sie sicher, dass alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **schließen**.  
  

