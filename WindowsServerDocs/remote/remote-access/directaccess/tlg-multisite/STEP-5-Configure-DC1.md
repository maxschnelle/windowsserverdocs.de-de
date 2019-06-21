---
title: Schritt 5 Konfigurieren von DC1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70357156-fcb0-4346-a61e-4ea963e3ffb0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 108e517923c75f685d817cdf9fad9b14132e3bb0
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281435"
---
# <a name="step-5-configure-dc1"></a>Schritt 5 Konfigurieren von DC1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

DC1 fungiert als Domänencontroller, DNS-Server und DHCP-Server für die Domäne "corp.contoso.com".  
  
Zum Konfigurieren des Remotezugriffs um eine Topologie mit mehreren Standorten verwenden, ist es erforderlich, zum Hinzufügen eines zusätzlichen Standorts von Active Directory Domain Services (AD DS) für die zweite Domäne-Controller 2-DC1, und Konfigurieren des Routings zwischen den Subnetzen.  
  
1. Das Standard-Gateway auf dem Domänencontroller zu konfigurieren. Konfigurieren Sie auf DC1 das Standardgateway ein.  
  
2. Erstellen Sie Sicherheitsgruppen für DirectAccess unter Windows 7-Clients auf DC1 an. Wenn DirectAccess konfiguriert wurde, erstellt es automatisch Gruppenrichtlinienobjekte (GPOs) und GPO-Einstellungen, die für DirectAccess-Clients und-Server angewendet werden. Das DirectAccess-Client-Gruppenrichtlinienobjekt wird auf bestimmte Active Directory-Sicherheitsgruppen angewendet.  
  
3. Um eine neue AD DS-Standort hinzuzufügen. Erstellen Sie einen zweite AD DS-Standort.  
  
## <a name="to-configure-the-default-gateway-on-the-domain-controller"></a>So konfigurieren Sie die Standard-Gateway auf dem Domänencontroller  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  Im Fenster Netzwerkverbindungen mit der Maustaste **verkabelte Ethernetverbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  In **Standardgateway**, Typ **10.0.0.254**, und klicken Sie in **alternativer DNS-Server**, Typ **10.2.0.1**, und klicken Sie dann auf **OK** .  
  
5.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
6.  In **Standardgateway**, Typ **2001:db8:1::fe**, und klicken Sie in **alternativer DNS-Server**, Typ **2001:db8:2::1**, und klicken Sie dann auf **OK**.  
  
7.  Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld klicken Sie auf **schließen**.  
  
8.  Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="create-security-groups-for-windows-7-directaccess-clients-on-dc1"></a>Erstellen von Sicherheitsgruppen für DirectAccess unter Windows 7-Clients auf DC1  
Erstellen Sie die Sicherheitsgruppen für DirectAccess für Windows 7 mithilfe des folgenden Verfahrens.  
  
 Windows 7-Clientcomputer müssen separate Sicherheitsgruppen angehören, da sie auf interne Ressourcen über einen einzigen Einstiegspunkt nur eine Verbindung herstellen können. Beim Aktivieren der Unterstützung mehrerer Standorte oder Eintrag hinzufügen, verweist, wenn Windows 7-Unterstützung angefordert wird, wird automatisch ein separates Gruppenrichtlinienobjekt von DirectAccess für Windows 7-Clients für jeden Einstiegspunkt erstellt werden.  
  
### <a name="create-security-groups"></a>Erstellen von Sicherheitsgruppen  
  
1.  Auf der **starten** geben**dsa.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich **"corp.contoso.com"** , klicken Sie auf **Benutzer**, klicken Sie dann mit der rechten Maustaste **Benutzer**, zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.  
  
3.  Auf der **neues Objekt – Gruppe** Dialogfeld **Gruppenname**, geben Sie **Win7_Clients_Site1**.  
  
4.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
5.  Doppelklicken Sie auf die **Win7_Clients_Site1** Sicherheitsgruppe ein, und klicken Sie auf die **Win7_Clients_Site1 Eigenschaften** im Dialogfeld klicken Sie auf die **Mitglieder** Registerkarte.  
  
6.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
7.  Auf der **Auswahl von Benutzern, Kontakten, Computern oder Dienstkonten** Dialogfeld klicken Sie auf **Objekttypen**. Auf der **Objekttypen** wählen Sie im Dialogfeld **Computer**, und klicken Sie dann auf **OK**.  
  
8.  In **Geben Sie die zu verwendenden Objektnamen**, Typ **client2**, und klicken Sie dann auf **OK**, und klicken Sie dann auf die **Win7_Clients_Site1 Eigenschaften** Dialogfeld auf **OK**.  
  
9. In der **Active Directory-Benutzer und-Computer** mit der rechten Maustaste der Verwaltungskonsole im linken Bereich **Benutzer**, zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe** .  
  
10. Auf der **neues Objekt – Gruppe** Dialogfeld **Gruppenname**, geben Sie **Win7_Clients_Site2**.  
  
11. Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
12. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer** .  
  
## <a name="to-add-a-new-ad-ds-site"></a>Hinzufügen einen neuen AD DS-Standort  
  
1.  Auf der **starten** geben**dssite.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der Konsole Active Directory-Standorte und-Dienste in der Konsolenstruktur mit der Maustaste **Websites**, und klicken Sie dann auf **neuen Standort**.  
  
3.  Auf der **neues Objekt - Standort** Dialogfeld die **Namen** geben **Sekunde-Site**.  
  
4.  Klicken Sie in das Listenfeld **DEFAULTIPSITELINK**, und klicken Sie dann auf **OK** zweimal.  
  
5.  Erweitern Sie in der Konsolenstruktur **Websites**, mit der rechten Maustaste **Subnetze**, und klicken Sie dann auf **neues Subnetz**.  
  
6.  Auf der **neues Objekt – Subnetz** Dialogfeld **Präfix**, Typ **10.0.0.0/24**in die **Standortobjekt für dieses Präfix auswählen** auf **Standardname-des-ersten-Standorts**, und klicken Sie dann auf **OK**.  
  
7.  In der Konsolenstruktur mit der Maustaste **Subnetze**, und klicken Sie dann auf **neues Subnetz**.  
  
8.  Auf der **neues Objekt – Subnetz** Dialogfeld **Präfix**, Typ **2001:db8:1:: / 64**in die **Standortobjekt für dieses Präfix auswählen** Liste Klicken Sie auf **Standardname-des-ersten-Standorts**, und klicken Sie dann auf **OK**.  
  
9. In der Konsolenstruktur mit der Maustaste **Subnetze**, und klicken Sie dann auf **neues Subnetz**.  
  
10. Auf der **neues Objekt – Subnetz** Dialogfeld **Präfix**, Typ **10.2.0.0/24**in die **Standortobjekt für dieses Präfix auswählen** auf **Sekunde-Site**, und klicken Sie dann auf **OK**.  
  
11. In der Konsolenstruktur mit der Maustaste **Subnetze**, und klicken Sie dann auf **neues Subnetz**.  
  
12. Auf der **neues Objekt – Subnetz** Dialogfeld **Präfix**, Typ **2001:db8:2:: / 64**in die **Standortobjekt für dieses Präfix auswählen** Liste Klicken Sie auf **Sekunde-Site**, und klicken Sie dann auf **OK**.  
  
13. Schließen Sie die Active Directory-Standorte und Dienste.  
  


