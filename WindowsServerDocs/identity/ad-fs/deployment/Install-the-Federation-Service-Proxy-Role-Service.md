---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: Installieren des Verbunddienst-Rollendienst
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: aea1ef335604aa18f0b1a1c22ef13f6fee1601b3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-federation-service-proxy-role-service"></a>Installieren des Verbunddienst-Rollendienst

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und Zertifikate konfigurieren, sind Sie bereit zum Installieren des Verbunddienstproxy-Rollendiensts der Active Directory Federation Services \(AD FS\). Das folgende Verfahren können den Verbunddienstproxy-Rollendienst installieren. Wenn Sie die Verbunddienstproxy-Rollendienst auf einem Computer installieren, wird diesem Computer einen Verbundserverproxy.  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-federation-service-proxy-role-service"></a>So installieren Sie den Verbunddienstproxy-Rollendienst  
  
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
  
9. Auf der **Rollendienste auswählen** Seite der **Verbunddienstproxy** , und klicken Sie dann auf **Weiter**.  
  
10. Auf der **Webserverrolle \(IIS\)** auf **Weiter**.  
  
11. Auf der **Rollendienste auswählen** auf **Weiter**.  
  
12. Nachdem Sie die Informationen auf Überprüfen der **Installationsauswahl bestätigen** Seite auf die **Zielserver bei Bedarf automatisch neu** , und klicken Sie dann auf **installieren**.  
  
13. Auf der **Installationsstatus** Seite, stellen Sie sicher, dass alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **schließen**.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

