---
title: Schritt 5 DC1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70357156-fcb0-4346-a61e-4ea963e3ffb0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: aa251ccc0cc48e3805667a247047711c2ae4fcf6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388301"
---
# <a name="step-5-configure-dc1"></a>Schritt 5 DC1 konfigurieren

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

DC1 fungiert als Domänen Controller, DNS-Server und DHCP-Server für die Corp.contoso.com-Domäne.  
  
Um den Remote Zugriff für die Verwendung einer Topologie mit mehreren Standorten zu konfigurieren, müssen Sie einen zusätzlichen Active Directory Domain Services (AD DS)-Standort für den zweiten Domänen Controller 2 DC1 hinzufügen und das Routing zwischen den Subnetzen konfigurieren.  
  
1. Zum Konfigurieren des Standard Gateways auf dem Domänen Controller. Konfigurieren Sie das Standard Gateway auf DC1.  
  
2. Erstellen Sie Sicherheitsgruppen für DirectAccess-Clients unter Windows 7 auf DC1. Wenn DirectAccess konfiguriert ist, werden automatisch Gruppenrichtlinie Objekte (GPOs) und GPO-Einstellungen erstellt, die auf DirectAccess-Clients und-Server angewendet werden. Das DirectAccess-Client-GPO wird auf bestimmte Active Directory Sicherheitsgruppen angewendet.  
  
3. Zum Hinzufügen einer neuen AD DS Website. Erstellen Sie eine zweite AD DS Website.  
  
## <a name="to-configure-the-default-gateway-on-the-domain-controller"></a>So konfigurieren Sie das Standard Gateway auf dem Domänen Controller  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste auf **verkabelte Ethernet-Verbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im **Standard Gateway** **10.0.0.254**ein, und geben Sie in **Alternativer DNS-Server** **10.2.0.1 bis**ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
6.  Geben Sie im **Standard Gateway** **2001: db8:1:: FE ein**, und geben Sie auf dem **alternativen DNS-Server** **2001: db8:2:: 1 ein**, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Schließen**.  
  
8.  Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="create-security-groups-for-windows-7-directaccess-clients-on-dc1"></a>Erstellen von Sicherheitsgruppen für Windows 7-DirectAccess-Clients auf DC1  
Erstellen Sie die DirectAccess-Sicherheitsgruppen für Windows 7 mit dem folgenden Verfahren.  
  
 Windows 7-Client Computer müssen Mitglieder von separaten Sicherheitsgruppen sein, da Sie nur über einen einzigen Einstiegspunkt eine Verbindung mit internen Ressourcen herstellen können. Wenn beim Aktivieren der Unterstützung für mehrere Standorte oder beim Hinzufügen von Einstiegspunkten eine Windows 7-Unterstützung angefordert wird, wird von DirectAccess für Windows 7-Clients für jeden Einstiegspunkt automatisch ein separates GPO erstellt.  
  
### <a name="create-security-groups"></a>Erstellen von Sicherheitsgruppen  
  
1.  Geben Sie auf dem **Start** Bildschirm**DSA. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Erweitern Sie im linken Bereich **Corp.contoso.com**, klicken Sie auf **Benutzer**, klicken Sie dann mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt-Gruppe** unter **Gruppenname**den Namen **Win7_Clients_Site1**ein.  
  
4.  Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
5.  Doppelklicken Sie auf die Sicherheitsgruppe **Win7_Clients_Site1** , und klicken Sie im Dialogfeld **Win7_Clients_Site1-Eigenschaften** auf die Registerkarte **Mitglieder** .  
  
6.  Auf der Registerkarte **Mitglieder** klicken Sie auf **Hinzufügen**.  
  
7.  Klicken Sie im Dialogfeld **Benutzer, Kontakte, Computer oder Dienst Konten auswählen** auf **Objekttypen**. Wählen Sie im Dialogfeld **Objekttypen** die Option **Computer**aus, und klicken Sie dann auf **OK**.  
  
8.  Geben Sie im Feld **Geben Sie die zu ausgewäfnenden Objektnamen ein den Namen** **client2**ein, klicken Sie auf **OK**, und klicken Sie dann im Dialogfeld **Win7_Clients_Site1-Eigenschaften** auf **OK**  
  
9. Klicken Sie in der Konsole **Active Directory Benutzer und Computer** im linken Bereich mit der rechten Maustaste auf **Benutzer**, zeigen Sie auf **neu**, und klicken Sie dann auf **Gruppe**.  
  
10. Geben Sie im Dialogfeld **Neues Objekt-Gruppe** unter **Gruppenname**den Namen **Win7_Clients_Site2**ein.  
  
11. Klicken Sie unter **Gruppenbereich** auf **Global**, unter **Gruppentyp** auf **Sicherheit** und anschließend auf **OK**.  
  
12. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer** .  
  
## <a name="to-add-a-new-ad-ds-site"></a>So fügen Sie eine neue AD DS Site hinzu  
  
1.  Geben Sie auf dem **Start** Bildschirm**dssite. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsole Active Directory Standorte und Dienste in der Konsolen Struktur mit der rechten Maustaste auf **Standorte**, und klicken Sie dann auf **neuer Standort**.  
  
3.  Geben Sie im Dialogfeld **Neues Objekt-Standort** im Feld **Name den Namen** **Second-Site**ein.  
  
4.  Klicken Sie im Listenfeld auf **DEFAULTIPSITELINK**, und klicken Sie dann zweimal auf **OK** .  
  
5.  Erweitern Sie in der Konsolen Struktur **Standorte**, klicken Sie mit der rechten Maustaste auf **Subnetze**, und klicken Sie dann auf **Neues Subnetz**.  
  
6.  Geben Sie im Dialogfeld **Neues Objekt-Subnetz** unter **Präfix** **10.0.0.0/24**ein, klicken Sie in der Liste **Wählen Sie ein Standort Objekt für dieses Präfix aus** auf **Default-First-Site-Name**, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Subnetze**, und klicken Sie dann auf **Neues Subnetz**.  
  
8.  Geben Sie im Dialogfeld **Neues Objekt-Subnetz** unter **Präfix**Folgendes ein: **2001: db8:1::/64**, klicken Sie in der Liste **Wählen Sie ein Standort Objekt für dieses Präfix aus** auf **Default-First-Site-Name**, und klicken Sie dann auf **OK**.  
  
9. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Subnetze**, und klicken Sie dann auf **Neues Subnetz**.  
  
10. Geben Sie im Dialogfeld **Neues Objekt-Subnetz** unter **Präfix** **10.2.0.0/24**ein, klicken Sie in der Liste **Wählen Sie ein Standort Objekt für dieses Präfix aus** auf **zweiter Standort**, und klicken Sie dann auf **OK**.  
  
11. Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf **Subnetze**, und klicken Sie dann auf **Neues Subnetz**.  
  
12. Geben Sie im Dialogfeld **Neues Objekt-Subnetz** unter **Präfix**Folgendes ein: **2001: db8:2::/64**, klicken Sie in der Liste **Wählen Sie ein Standort Objekt für dieses Präfix aus** auf **zweiter Standort**, und klicken Sie dann auf **OK**.  
  
13. Schließen Sie Active Directory Websites und Dienste.  
  


