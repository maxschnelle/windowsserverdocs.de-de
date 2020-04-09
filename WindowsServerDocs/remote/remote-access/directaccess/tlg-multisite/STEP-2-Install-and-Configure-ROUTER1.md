---
title: Schritt 2 ROUTER1 installieren und Konfigurieren von
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: dc20b1a0-540d-4531-a176-50b87c071600
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5e2b0759e85c05b4ee33971849bd1096d4c8419c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861603"
---
# <a name="step-2-install-and-configure-router1"></a>Schritt 2 ROUTER1 installieren und Konfigurieren von

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In dieser Test Umgebungs Anleitung für mehrere Standorte stellt der Routercomputer eine IPv4-und IPv6-Brücke zwischen den Subnetzen "Corpnet" und "2-Corpnet" bereit und fungiert als Router für den IP-HTTPS-und Teredo-Datenverkehr.  
  
- Installieren des Betriebssystems auf ROUTER1 
  
- Konfigurieren von TCP/IP-Eigenschaften und Umbenennen des Computers  
  
- Deaktivieren der Firewall
  
- Konfigurieren von Routing und Weiterleitung
  
## <a name="install-the-operating-system-on-router1"></a>Installieren des Betriebssystems auf ROUTER1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
### <a name="to-install-the-operating-system-on-router1"></a>So installieren Sie das Betriebssystem auf ROUTER1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation).  
  
2.  Folgen Sie den Installationsanweisungen, und legen Sie ein sicheres Kennwort für das lokale Administratorkonto fest. Melden Sie sich mit dem lokalen Administratorkonto an.  
  
3.  Verbinden Sie ROUTER1 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Verbinden Sie ROUTER1 mit den Subnetzen Corpnet und 2-Corpnet.  
  
## <a name="configure-tcpip-properties-and-rename-the-computer"></a>Konfigurieren von TCP/IP-Eigenschaften und Umbenennen des Computers  
Konfigurieren Sie die TCP/IP-Einstellungen auf dem Router, und benennen Sie den Computer in ROUTER1 um.  
  
### <a name="to-configure-tcpip-properties-and-rename-the-computer"></a>So konfigurieren Sie TCP/IP-Eigenschaften und benennen den Computer um  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf den mit Corpnet verbundenen Netzwerkadapter, klicken Sie auf **Umbenennen**, geben Sie **Corpnet**ein, und drücken Sie die EINGABETASTE.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Corpnet**, und klicken Sie auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **10.0.0.254**ein. Geben Sie **255.255.255.0**in **Subnetzmaske**ein, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
7.  Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in der **IPv6-Adresse** **2001: db8:1:: FE ein**. Geben Sie **unter Subnetzpräfix-Länge** **64**ein, und klicken Sie dann auf **OK**.  
  
8.  Klicken Sie im Dialogfeld **Corpnet-Eigenschaften** auf **Schließen**.  
  
9. Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf den Netzwerkadapter, der mit 2-Corpnet verbunden ist, klicken Sie auf **Umbenennen**, geben Sie **2-Corpnet**ein, und drücken Sie die EINGABETASTE.  
  
10. Klicken Sie mit der rechten Maustaste auf **2-Corpnet**, und klicken Sie dann auf **Eigenschaften**.  
  
11. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
12. Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **10.2.0.254**ein. Geben Sie **255.255.255.0**in **Subnetzmaske**ein, und klicken Sie dann auf **OK**.  
  
13. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
14. Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in **IPv6-Adresse** **2001: db8:2:: FE**ein. Geben Sie **unter Subnetzpräfix-Länge** **64**ein, und klicken Sie dann auf **OK**.  
  
15. Klicken Sie im Dialogfeld **Eigenschaften von 2 Corpnet** auf **Schließen**.  
  
16. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
17. Klicken Sie in der Server-Manager Konsole unter **lokaler Server**im Bereich **Eigenschaften** neben **Computer Name**auf den Link.  
  
18. Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
19. Geben Sie im Dialogfeld **Computername/Domänen Änderungen** unter **Computername den Namen** **ROUTER1**ein, und klicken Sie dann auf **OK**.  
  
20. Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
21. Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
22. Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
23. Nachdem der Computer neu gestartet wurde, melden Sie sich mit dem lokalen Administrator Konto an.  
  
## <a name="turn-off-the-firewall"></a>Deaktivieren der Firewall  
Dieser Computer ist nur für die Bereitstellung des Routings zwischen den Subnetzen "Corpnet" und "2-Corpnet" konfiguriert. Daher muss die Firewall ausgeschaltet werden.  
  
### <a name="to-turn-off-the-firewall"></a>So schalten Sie die Firewall aus  
  
1.  Geben Sie auf dem **Start** Bildschirm**WF. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in Windows-Firewall mit erweiterter Sicherheit im **Aktions** Bereich auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Windows-Firewall mit** erweiterter Sicherheit auf der Registerkarte **Domänen Profil** unter Firewallstatus auf **aus**. **Firewall state**  
  
4.  Klicken Sie im Dialogfeld **Windows-Firewall mit** erweiterter Sicherheit auf der Registerkarte **privates Profil** unter Firewallstatus auf **Firewall state** **aus**.  
  
5.  Klicken Sie im Dialogfeld **Windows-Firewall mit** erweiterter Sicherheit auf der Registerkarte **Öffentliches Profil** unter Firewallstatus auf **Firewall state** **aus**, und klicken Sie dann auf **OK**.  
  
6.  Schließen Sie Windows-Firewall mit erweiterter Sicherheit.  
  
## <a name="configure-routing-and-forwarding"></a>Konfigurieren von Routing und Weiterleitung  
Um Routing-und Weiterleitungs Dienste zwischen den Subnetzen Corpnet und 2-Corpnet bereitzustellen, müssen Sie die Weiterleitung auf den Netzwerkschnittstellen aktivieren und statische Routen zwischen den Subnetzen konfigurieren.  
  
### <a name="to-configure-static-routes"></a>So konfigurieren Sie statische Routen  
  
1.  Geben Sie auf dem **Start** Bildschirm**cmd. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Aktivieren Sie die Weiterleitung an IPv4-und IPv6-Schnittstellen beider Netzwerkadapter mithilfe der folgenden Befehle. Drücken Sie nach dem Eingeben der einzelnen Befehle die EINGABETASTE.  
  
    ```  
    netsh interface IPv4 set interface Corpnet forwarding=enabled  
    netsh interface IPv4 set interface 2-Corpnet forwarding=enabled  
    netsh interface IPv6 set interface Corpnet forwarding=enabled  
    netsh interface IPv6 set interface 2-Corpnet forwarding=enabled  
    ```  
  
3.  Aktivieren Sie das IP-HTTPS-Routing zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
    ```  
    netsh interface IPv6 add route 2001:db8:1:1000::/59 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:db8:2:2000::/59 2-Corpnet 2001:db8:2::20  
    ```  
  
4.  Aktivieren Sie das Teredo-Routing zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
    ```  
    netsh interface IPv6 add route 2001:0:836b:2::/64 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:0:836b:14::/64 2-Corpnet 2001:db8:2::20  
    ```  
  
5.  Schließen Sie das Eingabeaufforderungsfenster.
