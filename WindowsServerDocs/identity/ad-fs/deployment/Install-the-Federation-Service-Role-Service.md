---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: Installieren des Verbundserver-Rollendiensts
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 80a6cb2bc8e6f0fdb1a777a42f5d245f98ac3dee
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192087"
---
# <a name="install-the-federation-service-role-service"></a>Installieren des Verbundserver-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und die Zertifikate ordnungsgemäß konfiguriert haben, sind Sie bereit zum Installieren des Verbunddienst-Rollendienst, der Active Directory Federation Services \(AD FS\). Wenn Sie den Verbunddienst auf einem Computer installieren, wird dieser Computer einem Verbundserver aus.  
  
> [!NOTE]  
> Für die einzelnen für Federated Web\-anmelden\-auf \(SSO\) -Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation . Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Sie können das folgende Verfahren verwenden, installieren Sie die Verbunddienst-Rollendienst von AD FS auf einem Computer, der den ersten Verbundserver werden soll, oder auf einem Computer, der einen Verbundserver für eine Verbundserverfarm werden soll.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Stellen Sie sicher, dass ein SSL-Zertifikat mit dem privaten Schlüssel ist bereits installiert oder in den lokalen Zertifikatspeicher importiert \(persönlichen Speicher\) , bevor Sie dieses Verfahren starten. Wenn Sie ein Token verwenden\-Signaturzertifikat, das von einer Zertifizierungsstelle ausgestellt wurde \(Zertifizierungsstelle\), überprüfen Sie, ob ein Token\-Signaturzertifikat mit dem privaten Schlüssel bereits installiert oder wurde importiert dem lokalen Zertifikatspeicher \(persönlichen Speicher\) , bevor Sie dieses Verfahren starten. Als Alternative können Sie ein selbstsigniertes erstellen\-token signiert,\-Signaturzertifikat mithilfe des Assistenten zum Hinzufügen von Rollen, wie in diesem Verfahren beschrieben. Weitere Informationen zu Token\-Signieren von Zertifikaten, finden Sie [Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
#### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst  
  
1.  Auf der **starten** geben**Server-Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features** zum Hinzufügen von Rollen und Features-Assistenten zu starten.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Auf der **Installationstyp** auf **Rolle\-oder featurebasierte\-basierten Installation**, und klicken Sie auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, stellen Sie sicher, dass der Zielcomputer wird hervorgehoben, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Federation Services**, und klicken Sie dann auf Weiter.  
  
    > [!NOTE]  
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework- oder Windows Process Activation Service-Funktionen zu installieren, klicken Sie auf **Features hinzufügen** , diese zu installieren.  
  
7.  Auf der **Funktionen auswählen** Seite, stellen Sie sicher, dass die Funktionen festgelegt sind, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Active Directory Federation Service \(AD FS\)**  auf **Weiter**.  
  
9. Auf der **Rollendienste auswählen** Seite die **Verbunddienst** , und klicken Sie dann auf **Weiter**.  
  
10. Auf der **Webserverrolle \(IIS\)**  auf **Weiter**.  
  
11. Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.  
  
12. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten** , und klicken Sie dann auf **Installieren**.  
  
13. Überprüfen Sie auf der Seite **Installationsfortschritt** , ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.  
  

