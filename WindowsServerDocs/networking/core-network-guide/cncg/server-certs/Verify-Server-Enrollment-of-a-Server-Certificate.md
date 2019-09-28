---
title: Überprüfen der Serverregistrierung eines Serverzertifikats
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: bd80a018-5a30-47c3-89fc-aacb9f5ad298
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5f87db78d6f07d11c36193b1a56cf66bd44e7160
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356101"
---
# <a name="verify-server-enrollment-of-a-server-certificate"></a>Überprüfen der Serverregistrierung eines Serverzertifikats

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie überprüfen, ob die NPS-Server (Network Policy Server) ein Server Zertifikat von der Zertifizierungsstelle (Certification Authority, ca) registriert haben.   
  
>[!NOTE]  
>Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins** sein, um diese Verfahren ausführen zu können.  
  
## <a name="verify-network-policy-server-nps-enrollment-of-a-server-certificate"></a>Überprüfen der Netzwerk Richtlinien Server-Registrierung eines Server Zertifikats  
  
Da NPS zum Authentifizieren und Autorisieren von Netzwerk Verbindungsanforderungen verwendet wird, ist es wichtig sicherzustellen, dass das Serverzertifikat, das Sie für NPSS ausgestellt haben, bei Verwendung in Netzwerk Richtlinien gültig ist.  
  
Um sicherzustellen, dass ein Serverzertifikat ordnungsgemäß konfiguriert und beim NPS registriert ist, müssen Sie eine Test Netzwerk Richtlinie konfigurieren und NPS erlauben, zu überprüfen, ob das Zertifikat von NPS für die Authentifizierung verwendet werden kann.  
  
### <a name="to-verify-nps-enrollment-of-a-server-certificate"></a>So überprüfen Sie die NPS-Registrierung eines Serverzertifikats  
  
1.  Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **Netzwerk Richtlinien Server**. Der Netzwerk Richtlinien Server Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie auf **Richtlinien**, klicken Sie mit der rechten Maustaste auf **Netzwerk Richtlinien**und dann auf **neu**. Der Assistent für neue Netzwerk Richtlinien wird geöffnet.  
  
3.  Geben Sie unter **Netzwerk Richtlinien Name und Verbindungstyp angeben**in **Richtlinien Name die Bezeichnung** **Test Richtlinie**ein. Stellen Sie sicher, dass **für den Typ des Netzwerk Zugriffs Servers** der Wert **nicht angegeben**ist, und klicken Sie dann auf **weiter**.  
  
4.  Klicken Sie unter **Bedingungen angeben**auf **Hinzufügen**. Klicken Sie unter **Bedingung auswählen**auf **Windows-Gruppen**, und klicken Sie dann auf **Hinzufügen**.  
  
5.  Klicken Sie unter **Gruppen**auf **Gruppen hinzufügen**. Geben **Sie in Gruppe auswählen** **Domänen Benutzer**ein, und drücken Sie dann die EINGABETASTE. Klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
6.  Stellen Sie unter **Zugriffsberechtigung angeben**sicher, dass der **Zugriff gewährt** ausgewählt ist, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie unter **Authentifizierungsmethoden konfigurieren**auf **Hinzufügen**. Klicken Sie in **EAP hinzufügen**auf **Microsoft: Geschütztes EAP (PEAP)** , und klicken Sie dann auf **OK**. Wählen Sie in **EAP-Typen** **Microsoft: Geschütztes EAP (PEAP)** , und klicken Sie dann auf **Bearbeiten**. Das Dialogfeld **geschützte EAP-Eigenschaften bearbeiten** wird geöffnet.  
  
8.  Im Dialogfeld **geschützte EAP-Eigenschaften bearbeiten** wird in **Zertifikat ausgestellt für**NPS der Name des Serverzertifikats im Format *Computername*angezeigt. *Domäne*: Wenn Ihr NPS beispielsweise NPS-01 heißt und Ihre Domäne example.com ist, zeigt NPS das Zertifikat **NPS-01.example.com**an. Außerdem wird der Name Ihrer Zertifizierungsstelle im **Aussteller**angezeigt, und im **Ablaufdatum**wird das Ablaufdatum des Serverzertifikats angezeigt. Dies zeigt, dass Ihr NPS ein gültiges Serverzertifikat registriert hat, mit dem die Identität für Client Computer nachgewiesen werden kann, die über Ihre Netzwerk Zugriffs Server auf das Netzwerk zugreifen möchten, z. b. VPN-Server (virtuelles privates Netzwerk), 802.1 x-fähig. drahtlos Zugriffspunkte, Remotedesktop Gateway-Server und 802.1 x-fähige Ethernet-Switches.  
  
    > [!IMPORTANT]  
    > Wenn für NPS kein gültiges Serverzertifikat angezeigt wird und die Meldung angezeigt wird, dass ein solches Zertifikat nicht auf dem lokalen Computer gefunden werden kann, gibt es zwei mögliche Ursachen für dieses Problem. Möglicherweise wurde Gruppenrichtlinie nicht ordnungsgemäß aktualisiert, und das NPS hat kein Zertifikat von der Zertifizierungsstelle registriert. Starten Sie in diesem Fall den NPS neu. Wenn der Computer neu gestartet wird, wird Gruppenrichtlinie aktualisiert, und Sie können dieses Verfahren erneut ausführen, um zu überprüfen, ob das Serverzertifikat registriert ist. Wenn das Problem durch das Aktualisieren Gruppenrichtlinie nicht behoben werden kann, sind entweder die Zertifikat Vorlage, die automatische Zertifikat Registrierung oder beides nicht ordnungsgemäß konfiguriert. Um diese Probleme zu beheben, beginnen Sie am Anfang dieses Handbuchs, und führen Sie alle Schritte erneut aus, um sicherzustellen, dass die von Ihnen bereitgestellten Einstellungen korrekt sind.  
  
9. Wenn Sie überprüft haben, ob ein gültiges Serverzertifikat vorhanden ist, können Sie auf **OK** klicken und **Abbrechen** , um den Assistenten für neue Netzwerk Richtlinien zu beenden.  
  
    > [!NOTE]  
    > Da Sie den Assistenten nicht abschließen, wird die Test Netzwerk Richtlinie nicht in NPS erstellt.  
  


