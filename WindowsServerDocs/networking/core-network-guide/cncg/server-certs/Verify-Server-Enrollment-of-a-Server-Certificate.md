---
title: Überprüfen der Serverregistrierung eines Serverzertifikats
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: bd80a018-5a30-47c3-89fc-aacb9f5ad298
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d8ff51fa83972e2fc73ee54628eeb89e2927046d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="verify-server-enrollment-of-a-server-certificate"></a>Überprüfen der Serverregistrierung eines Serverzertifikats

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie überprüfen, ob Ihre Server (Network Policy Server, NPS) von der Zertifizierungsstelle (CA) ein Serverzertifikat registriert haben.   
  
>[!NOTE]  
>Mitgliedschaft in der **Domänen-Admins** Gruppe ist mindestens erforderlich, um diese Verfahren abzuschließen.  
  
## <a name="verify-network-policy-server-nps-enrollment-of-a-server-certificate"></a>Überprüfen Sie die Registrierung eines Serverzertifikats (Network Policy Server, NPS)  
  
Da NPS zur Authentifizierung und Autorisierung von verbindungsanforderungen Netzwerk verwendet wird, ist es wichtig, um sicherzustellen, dass das Serverzertifikat, das Sie zum NPS-Server ausgestellt haben Wenn Netzwerkrichtlinien verwendet wird.  
  
Um sicherzustellen, dass ein Serverzertifikat ordnungsgemäß konfiguriert ist und auf dem NPS-Server registriert ist, müssen Sie eine Test-Netzwerk-Richtlinie konfigurieren und Zulassen von NPS, um sicherzustellen, dass NPS das Zertifikat für die Authentifizierung verwenden können.  
  
### <a name="to-verify-nps-server-enrollment-of-a-server-certificate"></a>So überprüfen Sie die NPS-serverregistrierung eines Serverzertifikats  
  
1.  Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Network Policy Server Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie auf **Richtlinien**, mit der rechten Maustaste **Netzwerkrichtlinien**, und klicken Sie auf **neu**. Die Assistenten für neue Netzwerkrichtlinien wird geöffnet.  
  
3.  In **Netzwerk Richtliniennamen angeben und Verbindungstyp**im **Richtlinienname**, Typ **Test Richtlinie**. Stellen Sie sicher, dass **Typ des Netzwerkzugriffsservers** weist den Wert **Unspecified**, und klicken Sie dann auf **Weiter**.  
  
4.  In **Bedingungen angeben**, klicken Sie auf **hinzufügen**. In **wählen Bedingung**, klicken Sie auf **Windows-Gruppen**, und klicken Sie dann auf **hinzufügen**.  
  
5.  In **Gruppen**, klicken Sie auf **Gruppen hinzufügen**. In **Gruppe auswählen**, Typ **Domänenbenutzer**, und drücken Sie dann die EINGABETASTE. Klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
6.  In **Zugriffsberechtigung angeben**, stellen Sie sicher, dass **Zugriff gewährt** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
7.  In **Authentifizierungsmethoden konfigurieren**, klicken Sie auf **hinzufügen**. In **EAP hinzufügen**, klicken Sie auf **Microsoft: geschütztes EAP (PEAP)**, und klicken Sie dann auf **OK**. In **EAP-Typen**Option **Microsoft: geschütztes EAP (PEAP)**, und klicken Sie dann auf **bearbeiten**. Die **Eigenschaften für geschütztes EAP bearbeiten** Dialogfeld wird geöffnet.  
  
8.  In der **Eigenschaften für geschütztes EAP bearbeiten** Dialogfeld **für ausgestellte Zertifikat**, NPS zeigt den Namen des Serverzertifikats im Format *ComputerName*. *Domäne*. Der NPS-Server lautet NPS-01 und Ihre Domäne example.com ist, zeigt NPS z.B. das Zertifikat **NPS-01.example.com**. Darüber hinaus wird beim **Aussteller**, der Namen Ihrer Zertifizierungsstelle wird angezeigt, und im **Ablaufdatum**, das Datum der Ablauf des Serverzertifikats wird angezeigt. Dies zeigt, dass der NPS-Server ein gültiges Serverzertifikat registriert wurde, die sie verwenden kann, um seine Identität gegenüber Clientcomputern ausweisen, die versuchen, den Netzwerkzugriff über Ihre Netzwerkzugriffsserver, z. B. virtuelles privates Netzwerk (VPN), 802.1 X-fähigen Drahtloszugriffspunkten und Remotedesktop-Gatewayservern 802.1 X-fähige Ethernet-switches.  
  
    > [!IMPORTANT]  
    > Wenn NPS ein gültiges Serverzertifikat nicht angezeigt wird und sie die Meldung enthält, die Zertifikat auf dem lokalen Computer gefunden werden kann, gibt es zwei mögliche Ursachen für dieses Problem. Es ist möglich, dass der Gruppenrichtlinie nicht ordnungsgemäß aktualisiert, und der NPS-Server verfügt über ein Zertifikat von der Zertifizierungsstelle nicht registriert. Starten Sie in diesem Fall den NPS-Server neu. Beim Neustart des Computers die Gruppenrichtlinie aktualisiert wird, und Sie können dieses Verfahren erneut, um sicherzustellen, dass das Serverzertifikat registriert ist. Wenn dieses Problem durch Aktualisieren der Gruppenrichtlinie nicht behoben wird, werden die Zertifikatvorlage, automatische Registrierung von Zertifikaten oder beides sind nicht ordnungsgemäß konfiguriert. Um diese Probleme zu beheben, starten Sie am Anfang dieses Handbuchs, und führen Sie alle Schritte erneut, um sicherzustellen, dass die Einstellungen, die Sie eingegeben haben, richtig sind.  
  
9. Wenn Sie das Vorhandensein eines gültigen Zertifikats überprüft haben, klicken Sie auf **OK** und **Abbrechen** zum Beenden des Assistenten für neue Netzwerkrichtlinien.  
  
    > [!NOTE]  
    > Da Sie nicht den Assistenten abschließen, wird die Netzwerkrichtlinie Test nicht auf dem Netzwerkrichtlinienserver erstellt.  
  


