---
title: Überprüfen der Serverregistrierung eines Serverzertifikats
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: bd80a018-5a30-47c3-89fc-aacb9f5ad298
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 45ba7a9a7fc5b9622ab1b9a94f38f4bf4de13192
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850901"
---
# <a name="verify-server-enrollment-of-a-server-certificate"></a>Überprüfen der Serverregistrierung eines Serverzertifikats

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um sicherzustellen, dass Ihre Server (Network Policy Server, NPS) ein Serverzertifikat von der Zertifizierungsstelle (CA) registriert haben.   
  
>[!NOTE]  
>Mitgliedschaft in der **Domänen-Admins** Gruppe ist die mindestvoraussetzung zum Abschließen dieser Verfahren.  
  
## <a name="verify-network-policy-server-nps-enrollment-of-a-server-certificate"></a>Überprüfen der Registrierung (Network Policy Server, NPS), ein Serverzertifikat  
  
Da NPS zum Authentifizieren und Autorisieren von netzwerkanforderungen für die Verbindung verwendet wird, ist es wichtig, um sicherzustellen, dass das Serverzertifikat an, die, das Sie für NPSs ausgestellt haben, gültig, wenn Sie in den Netzwerkrichtlinien verwendet wird.  
  
Um sicherzustellen, dass ein Serverzertifikat ordnungsgemäß konfiguriert ist und an den NPS registriert ist, müssen Sie Konfigurieren einer Netzwerkrichtlinie für Test und Zulassen von NPS, um sicherzustellen, dass NPS das Zertifikat für die Authentifizierung verwenden können.  
  
### <a name="to-verify-nps-enrollment-of-a-server-certificate"></a>Um NPS-Registrierung ein Serverzertifikat zu überprüfen.  
  
1.  Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Network Policy Server Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie auf **Richtlinien**, mit der rechten Maustaste **Netzwerkrichtlinien**, und klicken Sie auf **neu**. Der Assistent für neue Netzwerkrichtlinien wird geöffnet.  
  
3.  In **Netzwerk-Richtliniennamen angeben und Verbindungstyp**im **Richtlinienname**, Typ **Testrichtlinie**. Sicherstellen, dass **Typ des Netzwerkzugriffsservers** hat den Wert **Unspecified**, und klicken Sie dann auf **Weiter**.  
  
4.  In **angeben von Bedingungen**, klicken Sie auf **hinzufügen**. In **wählen Bedingung**, klicken Sie auf **Windows-Gruppen**, und klicken Sie dann auf **hinzufügen**.  
  
5.  In **Gruppen**, klicken Sie auf **Gruppen hinzufügen**. In **Gruppe auswählen**, Typ **Domänenbenutzer**, und drücken Sie dann die EINGABETASTE. Klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
6.  In **Zugriffsberechtigung geben**, sicher, dass **Zugriffsgewährung** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
7.  In **Authentifizierungsmethoden konfigurieren**, klicken Sie auf **hinzufügen**. In **EAP hinzufügen**, klicken Sie auf **Microsoft: Geschütztes EAP (PEAP)**, und klicken Sie dann auf **OK**. In **EAP-Typen**Option **Microsoft: Geschütztes EAP (PEAP)**, und klicken Sie dann auf **bearbeiten**. Die **Eigenschaften für geschütztes EAP bearbeiten** Dialogfeld wird geöffnet.  
  
8.  In der **Eigenschaften für geschütztes EAP bearbeiten** Dialogfeld **Zertifikat ausgestellt für**, NPS zeigt den Namen des Serverzertifikats im Format *ComputerName*. *Domäne*. Wenn Sie den NPS den NPS-01-Namen und die Domäne "example.com", zeigt NPS z. B. das Zertifikat **NPS-01.example.com**. Darüber hinaus werden in **Aussteller**, der Namen Ihrer Zertifizierungsstelle wird angezeigt, und klicken Sie in **Ablaufdatum**, das Datum des Ablaufs des Serverzertifikats wird angezeigt. Dies beweist, dass Ihre NPS ein gültiges Serverzertifikat registriert wurde, die sie verwenden kann, um seine Identität gegenüber Clientcomputern ausweisen kann, die versuchen, Zugriff auf das Netzwerk über Ihre Netzwerkzugriffsserver, z. B. virtuelles privates Netzwerk (VPN)-Server, 802.1 X-fähig drahtlose Zugriffspunkte, Remotedesktopgateway-Server und 802.1 werden die X-fähiger Ethernet-switches.  
  
    > [!IMPORTANT]  
    > Wenn Sie NPS ein gültiges Serverzertifikat nicht angezeigt wird und sie die Nachricht enthält, die solche ein Zertifikat auf dem lokalen Computer nicht gefunden werden kann, gibt es zwei mögliche Gründe für dieses Problem. Es ist möglich, dass der Gruppenrichtlinie nicht ordnungsgemäß aktualisiert, und der NPS verfügt über ein Zertifikat von der Zertifizierungsstelle nicht registriert. In diesem Fall Neustarten des NPS. Beim Neustart des Computers die Gruppenrichtlinie aktualisiert wird, und durchführen können diese Prozedur erneut aus, um sicherzustellen, dass das Zertifikat registriert ist. Wenn die Aktualisierung der Gruppenrichtlinie dieses Problem nicht behebt, sind entweder die Zertifikatvorlage, automatische Registrierung von Zertifikaten oder beides nicht ordnungsgemäß konfiguriert. Um diese Probleme zu beheben, beginnen Sie am Anfang dieses Handbuchs, und führen Sie alle Schritte erneut aus, um sicherzustellen, dass die Einstellungen, die Sie angegeben haben, richtig sind.  
  
9. Wenn Sie das Vorhandensein ein gültiges Serverzertifikat überprüft haben, können Sie klicken **OK** und **Abbrechen** zum Beenden des Assistenten für neue Netzwerkrichtlinien.  
  
    > [!NOTE]  
    > Da Sie den Assistenten nicht abschließen, wird die Netzwerkrichtlinie Test nicht auf dem Netzwerkrichtlinienserver erstellt.  
  


