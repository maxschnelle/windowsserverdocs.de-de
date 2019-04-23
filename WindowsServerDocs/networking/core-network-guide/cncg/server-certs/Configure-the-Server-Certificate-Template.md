---
title: Konfigurieren der Serverzertifikatvorlage
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 238579c945821d19e45dad7e623450d598830596
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886121"
---
# <a name="configure-the-server-certificate-template"></a>Konfigurieren der Serverzertifikatvorlage

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren so konfigurieren Sie die Zertifikatvorlage, die Active Directory&reg; -Zertifikatdienste (AD CS) verwendet als Grundlage für Serverzertifikate, die auf Servern in Ihrem Netzwerk registriert werden.  
  
Bei der Konfiguration dieser Vorlage, können Sie die Server von Active Directory-Gruppe angeben, die automatisch ein Serverzertifikat von AD CS empfangen soll.   
  
Das folgende Verfahren enthält Anweisungen zum Konfigurieren der Vorlage zum Ausstellen von Zertifikaten für alle der folgenden Server-Datentypen:  
  
- Server auf denen RAS-Dienst, einschließlich der RAS-Gateway-Server, die Elemente der **RAS- und IAS-Server** Gruppe.  
- Server, auf denen dem Dienst (Network Policy Server, NPS) sind Mitglieder der **RAS- und IAS-Server** Gruppe.  
  
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.  
  
### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage  
  
1.  Klicken Sie auf ka1, im Server-Manager auf **Tools**, und klicken Sie dann auf **Zertifizierungsstelle**. Die Zertifizierung Autorität für die Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie in der MMC auf den Zertifizierungsstellennamen, mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie dann auf **verwalten**.  
  
3.  Die Zertifikatvorlagenkonsole wird geöffnet. Alle Zertifikatvorlagen werden im Detailbereich angezeigt.  
  
4.  Klicken Sie im Detailbereich auf die **RAS- und IAS-Server** Vorlage.  
  
5.  Klicken Sie auf die **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Die Vorlage **Eigenschaften** Dialogfeld wird geöffnet.  
  
6.  Klicken Sie auf die Registerkarte **Sicherheit**.   
  
7.  Auf der **Sicherheit** Registerkarte **Gruppen-oder Benutzernamen**, klicken Sie auf **RAS- und IAS-Server**.  
  
8.  In **Berechtigungen für RAS- und IAS-Server**unter **zulassen**, sicher, dass **registrieren** ausgewählt ist, und wählen Sie dann die **automatisch registrieren** überprüfen Box. Klicken Sie auf **OK**, und schließen Sie die Zertifikatvorlagen-MMC.  
  
9.  In den Zertifizierungsstellen-MMC, klicken Sie auf **Zertifikatvorlagen**. Auf der **Aktion** Startmenü **neu**, und klicken Sie dann auf **Auszustellende Zertifikatvorlage**. Das Dialogfeld **Zertifikatvorlagen aktivieren** wird geöffnet.  
  
10. In **Zertifikatvorlagen aktivieren**, klicken Sie auf den Namen der Zertifikatvorlage, die Sie gerade konfiguriert, und klicken Sie dann auf **OK**. Z. B. Wenn Sie den Standardname der Zertifikatvorlage nicht geändert haben, klicken Sie auf **Kopie von RAS- und IAS-Server**, und klicken Sie dann auf **OK**.  
  


