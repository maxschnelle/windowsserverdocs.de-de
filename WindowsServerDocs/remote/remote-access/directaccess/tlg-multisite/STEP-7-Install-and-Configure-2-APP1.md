---
title: 'Schritt 7: Installieren und Konfigurieren von 2-App1'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cc0abc6-be4d-4cbe-bd0c-cc448bf294f6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c5a316e1230692fb800c088d752c26ec4a0f3349
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388265"
---
# <a name="step-7-install-and-configure-2-app1"></a>Schritt 7: Installieren und Konfigurieren von 2-App1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

2 App1 stellt Web-und Dateifreigabe Dienste bereit. 2: die App1-Konfiguration besteht aus folgendem:  
  
- Installieren des Betriebssystems auf 2-App1  
  
- Konfigurieren von TCP/IP-Eigenschaften  
  
- Join 2 App1 zur CORP2-Domäne  
  
- Installieren Sie die Rolle "Webserver (IIS)" auf 2 App1  
  
- Erstellen eines freigegebenen Ordners auf 2-App1 
  
## <a name="bkmk_InstallOS"></a>Installieren des Betriebssystems auf 2-App1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
#### <a name="to-install-the-operating-system-on-2-app1"></a>So installieren Sie das Betriebssystem auf 2-App1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation).  
  
2.  Folgen Sie den Installationsanweisungen, und legen Sie ein sicheres Kennwort für das lokale Administratorkonto fest. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden Sie 2 App1 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Verbinden Sie 2 App1 mit dem Subnetz 2-Corpnet.  
  
## <a name="bkmk_TCP"></a>Konfigurieren von TCP/IP-Eigenschaften  
Konfigurieren Sie die TCP/IP-Eigenschaften für 2 App1.  
  
#### <a name="to-configure-tcpip-properties"></a>So konfigurieren Sie die TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf **verkabelte Ethernet-Verbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **10.2.0.3**ein. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein. Geben Sie unter **Standard Gateway**den Namen **10.2.0.254**ein.  
  
5.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. Geben Sie unter **Bevorzugter DNS-Server** **10.2.0.1 bis**ein.  
  
6.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**. Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie zweimal auf **OK** .  
  
7.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
8.  Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in der **IPv6-Adresse** **2001: db8:2:: 3**ein. Geben Sie unter **Subnetzpräfix-Länge**den Wert **64**ein. Geben Sie unter **Standard Gateway**den Wert **2001: db8:2:: FE**ein. Klicken Sie auf **folgende DNS-Serveradressen verwenden**, und geben Sie unter **Bevorzugter DNS-Server** **2001: db8:2:: 1 ein**.  
  
9. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
10. Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
11. Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Schließen**.  
  
12. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="bkmk_JoinDomain"></a>Join 2 App1 zur CORP2-Domäne  
Join 2 App1 zur corp2.Corp.contoso.com-Domäne.  
  
#### <a name="to-join-2-app1-to-the-corp2-domain"></a>So verknüpfen Sie 2 App1 mit der CORP2-Domäne  
  
1.  Klicken Sie in der Server-Manager Konsole unter **lokaler Server**im Bereich **Eigenschaften** neben **Computer Name**auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  Geben Sie unter **Computer Name den Namen** **2-App1**ein. Klicken Sie unter **Mitglied von**auf **Domäne**, geben Sie **corp2.Corp.contoso.com**ein, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie **Administrator** und Kennwort ein, und klicken Sie dann auf **OK**.  
  
5.  Wenn ein Dialogfeld angezeigt wird, in dem Sie zur Domäne corp2.Corp.contoso.com Willkommen werden, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Klicken Sie nach dem Neustart des Computers auf **Benutzer wechseln**und dann auf **anderer Benutzer** , und melden Sie sich bei der Domäne CORP2 mit dem Administrator Konto an.  
  
## <a name="bkmk_IIS"></a>Installieren Sie die Rolle "Webserver (IIS)" auf 2 App1  
Installieren Sie die Rolle "Webserver (IIS)", um "2 App1 a Web Server" zu erstellen.  
  
#### <a name="to-install-the-web-server-iis-role"></a>So installieren Sie die Rolle "Webserver (IIS)"  
  
1.  Klicken Sie in der Server-Manager-Konsole auf dem **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **weiter** , um zum Bildschirm für die Server Rollenauswahl zu gelangen.  
  
3.  Wählen Sie auf der Seite **Server Rollen auswählen** die Option **Webserver (IIS)** aus, und klicken Sie dann vier Mal auf **weiter** .  
  
4.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
5.  Überprüfen Sie, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
## <a name="bkmk_Share"></a>Erstellen eines freigegebenen Ordners auf 2-App1  
Erstellen Sie einen freigegebenen Ordner und eine Textdatei im Ordner auf 2 App1.  
  
#### <a name="to-create-a-shared-folder"></a>So erstellen Sie einen freigegebenen Ordner  
  
1.  Geben Sie auf dem **Start** Bildschirm**Explorer. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie auf **Computer**, und doppelklicken Sie dann auf lokaler Datenträger **(C:)** .  
  
3.  Klicken Sie auf **neuer Ordner**, geben Sie **Dateien**ein, und drücken Sie die EINGABETASTE. Lassen Sie das Fenster **lokaler** Datenträger geöffnet.  
  
4.  Geben Sie im **Start** Bildschirm**Notepad. exe**ein, klicken Sie mit der rechten Maustaste auf **Notepad**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**.  
  
5.  Geben Sie im Fenster " **unbenanntes Notepad** " **eine freigegebene Datei in "2-App1" ein**.  
  
6.  Klicken Sie auf **Datei**, klicken Sie auf **Speichern**, klicken Sie auf **Computer**, doppelklicken Sie auf lokaler Datenträger **(C:)** , und doppelklicken Sie dann auf den Ordner **Dateien** .  
  
7.  Geben Sie unter **Dateiname die Bezeichnung** **example. txt**ein, und klicken Sie dann auf **Speichern**. Schließen Sie Editor.  
  
8.  Klicken Sie im Fenster **lokaler** Datenträger mit der rechten Maustaste auf den Ordner **Dateien** , zeigen Sie auf **Freigeben**für, und klicken Sie dann auf **bestimmte Personen**.  
  
9. Klicken Sie im Dialogfeld **Dateifreigabe** in der Dropdown Liste auf **alle**, und klicken Sie dann auf **Hinzufügen**. Klicken Sie in **Berechtigungsstufe** für **alle**auf **Lesen/Schreiben**.  
  
10. Klicken Sie auf **Freigeben**und dann auf **done**.  
  
11. Schließen Sie das Fenster **lokaler** Datenträger.  
  


