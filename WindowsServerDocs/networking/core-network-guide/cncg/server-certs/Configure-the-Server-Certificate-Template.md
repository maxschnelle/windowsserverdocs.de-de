---
title: Konfigurieren der Serverzertifikatvorlage
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e747fedd74dfc55c2c4df457d7f107b618423b8e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-server-certificate-template"></a>Konfigurieren der Serverzertifikatvorlage

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können dieses Verfahren so konfigurieren Sie die Zertifikatvorlage, die Active Directory&reg; verwendet der Zertifikatdienste (AD CS) als Grundlage für Serverzertifikate, die auf Servern im Netzwerk angemeldet werden.  
  
Beim Konfigurieren diese Vorlage, können Sie die Server anhand der Active Directory-Gruppe angeben, die automatisch ein Zertifikat von AD CS erhalten soll.   
  
Das folgende Verfahren enthält eine Anleitung für die Vorlage zum Ausstellen von Zertifikaten für alle der folgenden Server konfigurieren:  
  
- Server mit der RAS-Dienst, einschließlich der RAS-Gateway-Server, die Mitglieder der **RAS- und IAS-Server** Gruppe.  
- Server, auf denen dem Netzwerkrichtlinienserver (Network Policy Server, NPS)-Dienst sind Mitglieder der **RAS- und IAS-Server** Gruppe.  
  
Mitgliedschaften in den **Organisations-Admins** und der Stammdomäne **Domänen-Admins** Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  
  
### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage  
  
1.  Klicken Sie auf der Zertifizierungsstelle 1, im Server-Manager auf **Tools**, und klicken Sie dann auf **Zertifizierungsstelle**. Die Zertifizierung Autorität für die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie in der MMC auf den Namen der Zertifizierungsstelle, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **verwalten**.  
  
3.  Die Zertifikatvorlagenkonsole wird geöffnet. Alle Zertifikatvorlagen werden im Detailbereich angezeigt.  
  
4.  Klicken Sie im Detailbereich auf die **RAS- und IAS-Server** Vorlage.  
  
5.  Klicken Sie auf die **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Die Vorlage **Eigenschaften** Dialogfeld wird geöffnet.  
  
6.  Klicken Sie auf die **Security** Registerkarte.   
  
7.  Auf der **Security** Registerkarte **Gruppen-oder Benutzernamen**, klicken Sie auf **RAS- und IAS-Server**.  
  
8.  In **Berechtigungen für RAS- und IAS-Server**unter **zulassen**, stellen Sie sicher, dass **registrieren** aktiviert ist, und wählen Sie dann die **automatisch registrieren** Kontrollkästchen. Klicken Sie auf **OK**, und schließen Sie die Zertifikatvorlagen-MMC.  
  
9.  In der Zertifizierungsstellen-MMC, klicken Sie auf **Zertifikatvorlagen**. Auf der **Aktion** auf **neu**, und klicken Sie dann auf **Auszustellende Zertifikatvorlage**. Die **Zertifikatvorlagen aktivieren** Dialogfeld wird geöffnet.  
  
10. In **Zertifikatvorlagen aktivieren**, klicken Sie auf den Namen der Zertifikatvorlage, die Sie gerade konfiguriert, und klicken Sie dann auf **OK**. Z. B. Wenn Sie der Standardname der Zertifikatvorlage nicht geändert haben, klicken Sie auf **Kopie von RAS- und IAS-Server**, und klicken Sie dann auf **OK**.  
  


