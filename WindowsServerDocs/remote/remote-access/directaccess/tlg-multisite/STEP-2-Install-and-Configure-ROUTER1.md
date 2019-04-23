---
title: Schritt 2 installieren und Konfigurieren von ROUTER1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc20b1a0-540d-4531-a176-50b87c071600
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6a771b5eb8587d23bc67a7e7769264251afdb5bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838511"
---
# <a name="step-2-install-and-configure-router1"></a>Schritt 2 installieren und Konfigurieren von ROUTER1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Handbuch für mehrere Standorte Test Lab der Router-Computer stellt eine IPv4- und IPv6-Brücke zwischen den Subnetzen "Corpnet" und "2-Corpnet", und fungiert als Router für die IP-HTTPS und Teredo-Verkehr.  
  
- Installieren des Betriebssystems auf ROUTER1 
  
- Konfigurieren Sie TCP/IP-Eigenschaften, und benennen Sie den computer  
  
- Die Firewall ausschalten
  
- Konfigurieren von routing und Weiterleiten
  
## <a name="install-the-operating-system-on-router1"></a>Installieren des Betriebssystems auf ROUTER1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
### <a name="to-install-the-operating-system-on-router1"></a>So installieren Sie das Betriebssystem auf ROUTER1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation).  
  
2.  Folgen Sie den Installationsanweisungen, und legen Sie ein sicheres Kennwort für das lokale Administratorkonto fest. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden von ROUTER1 mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden von ROUTER1 den Subnetzen "Corpnet" und "2-Corpnet".  
  
## <a name="configure-tcpip-properties-and-rename-the-computer"></a>Konfigurieren Sie TCP/IP-Eigenschaften, und benennen Sie den computer  
Konfigurieren von TCP/IP-Einstellungen auf dem Router, und benennen Sie den Computer, von ROUTER1.  
  
### <a name="to-configure-tcpip-properties-and-rename-the-computer"></a>Zum Konfigurieren von TCP/IP-Eigenschaften, und benennen Sie den computer  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  In der **Netzwerkverbindungen** Fenster mit der rechten Maustaste in des Netzwerkadapter, die mit Corpnet verbunden ist, klicken Sie auf **umbenennen**, Typ **"Corpnet"**, und drücken Sie EINGABETASTE.  
  
3.  Mit der rechten Maustaste **"Corpnet"**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.0.0.254**. In **Subnetzmaske**, Typ **255.255.255.0**, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
7.  Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:1::fe**. In **Subnetzpräfixlänge**, Typ **64**, und klicken Sie dann auf **OK**.  
  
8.  Auf der **Corpnet Eigenschaften** Dialogfeld auf **schließen**.  
  
9. In der **Netzwerkverbindungen** Fenster mit der rechten Maustaste in des Netzwerkadapter, die mit 2-Corpnet verbunden ist, klicken Sie auf **umbenennen**, Typ **2-Corpnet**, und drücken Sie EINGABETASTE.  
  
10. Mit der rechten Maustaste **2-Corpnet**, und klicken Sie dann auf **Eigenschaften**.  
  
11. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
12. Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.2.0.254**. In **Subnetzmaske**, Typ **255.255.255.0**, und klicken Sie dann auf **OK**.  
  
13. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
14. Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:2::fe**. In **Subnetzpräfixlänge**, Typ **64**, und klicken Sie dann auf **OK**.  
  
15. Auf der **2-Corpnet Eigenschaften** Dialogfeld auf **schließen**.  
  
16. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
17. In der Server-Manager-Konsole in **lokalen Server**in die **Eigenschaften** Bereich, der neben **Computername**, klicken Sie auf den Link.  
  
18. Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
19. Auf der **Änderung des Computernamens bzw. der Domäne** Dialogfeld **Computername**, Typ **ROUTER1**, und klicken Sie dann auf **OK**.  
  
20. Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
21. Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
22. Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
23. Melden Sie sich nach dem Neustart des Computers mit dem lokalen Administratorkonto an.  
  
## <a name="turn-off-the-firewall"></a>Die Firewall ausschalten  
Dieser Computer ist nur für konfiguriert routing zwischen den Subnetzen "Corpnet" und "2-Corpnet"; aus diesem Grund muss die Firewall deaktiviert werden.  
  
### <a name="to-turn-off-the-firewall"></a>So deaktivieren Sie die firewall  
  
1.  Auf der **starten** geben**wf.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der Windows-Firewall mit erweiterter Sicherheit in der **Aktionen** Bereich, klicken Sie auf **Eigenschaften**.  
  
3.  Auf der **Windows-Firewall mit erweiterter Sicherheit** Dialogfeld auf die **Domänenprofil** Registerkarte **Firewall-Status**, klicken Sie auf **aus**.  
  
4.  Auf der **Windows-Firewall mit erweiterter Sicherheit** Dialogfeld auf die **privates Profil** Registerkarte **Firewall-Status**, klicken Sie auf **aus**.  
  
5.  Auf der **Windows-Firewall mit erweiterter Sicherheit** Dialogfeld auf die **öffentliches Profil** Registerkarte **Firewall-Status**, klicken Sie auf **aus**, und klicken Sie dann Klicken Sie auf **OK**.  
  
6.  Schließen Sie Windows-Firewall mit erweiterter Sicherheit.  
  
## <a name="configure-routing-and-forwarding"></a>Konfigurieren von routing und Weiterleiten  
Um und Weiterleitung Dienste zwischen den Subnetzen "Corpnet" und "2-Corpnet" zu gewährleisten, müssen Sie Weiterleitung auf die die Netzwerkschnittstellen zu aktivieren und konfigurieren statische Routen zwischen den Subnetzen.  
  
### <a name="to-configure-static-routes"></a>Zum Konfigurieren von statischer Routen  
  
1.  Auf der **starten** geben**cmd.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Aktivieren Sie die Weiterleitung auf die IPv4- und IPv6-Schnittstellen der beiden Netzwerkadapter mit den folgenden Befehlen. Drücken Sie nach der Eingabe jedes Befehls die EINGABETASTE.  
  
    ```  
    netsh interface IPv4 set interface Corpnet forwarding=enabled  
    netsh interface IPv4 set interface 2-Corpnet forwarding=enabled  
    netsh interface IPv6 set interface Corpnet forwarding=enabled  
    netsh interface IPv6 set interface 2-Corpnet forwarding=enabled  
    ```  
  
3.  Aktivieren Sie die IP-HTTPS-routing zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
    ```  
    netsh interface IPv6 add route 2001:db8:1:1000::/59 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:db8:2:2000::/59 2-Corpnet 2001:db8:2::20  
    ```  
  
4.  Aktivieren Sie Teredo routing zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
    ```  
    netsh interface IPv6 add route 2001:0:836b:2::/64 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:0:836b:14::/64 2-Corpnet 2001:db8:2::20  
    ```  
  
5.  Schließen Sie das Eingabeaufforderungsfenster.
