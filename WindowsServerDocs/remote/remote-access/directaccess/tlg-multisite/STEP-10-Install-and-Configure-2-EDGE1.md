---
title: 'Schritt 10: Installieren und Konfigurieren von 2-Edge1'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d98d6f7a-a2e6-45b1-9c63-08e2986a5c03
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7d21d80f4970a501e31a053483c37268bdddb811
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314614"
---
# <a name="step-10-install-and-configure-2-edge1"></a>Schritt 10: Installieren und Konfigurieren von 2-Edge1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

2: die Edge1-Konfiguration besteht aus folgendem:  
  
- Installieren Sie das Betriebssystem auf 2 Edge1. Installieren Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 auf 2 Edge1.  
  
- Konfigurieren von TCP/IP-Eigenschaften Konfigurieren Sie 2 Edge1 mit statischen Adressen an beiden Netzwerkschnittstellen.  
  
- Konfigurieren Sie das Routing zwischen Subnetzen. Um die Kommunikation zwischen den Subnetzen Corpnet und 2-Corpnet zu aktivieren, müssen Sie das Routing konfigurieren.  
  
- Join 2 Edge1 zur CORP2-Domäne. Join 2 Edge1 zur corp2.Corp.contoso.com-Domäne.  
  
- Beziehen Sie Zertifikate auf 2 Edge1. Zertifikate sind für die IPSec-Verbindung zwischen DirectAccess-Clients und dem RAS-Server erforderlich und zum Authentifizieren des IP-HTTPS-Listener, wenn Clients eine Verbindung über HTTPS herstellen.  
  
- Gewähren des Zugriffs auf corp\user1. Der Benutzer corp\user1 ist der Remote Zugriffs Administrator. Damit dieser Benutzer Änderungen an 2 Edge1 von Edge1 aus vornehmen kann, müssen Sie dem Benutzer Zugriff erteilen.  
  
- Installieren Sie die Remote Zugriffs Rolle auf 2 Edge1. Um eine Bereitstellung für mehrere Standorte zu aktivieren, müssen Sie die Remote Zugriffs Rolle auf 2 Edge1 installieren.  
  
2 Edge1 es müssen zwei Netzwerkadapter installiert sein.  
  
## <a name="install-the-operating-system-on-2-edge1"></a><a name="installOS"></a>Installieren des Betriebssystems auf 2-Edge1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Befolgen Sie die Anweisungen, um die Installation abzuschließen, indem Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administrator Konto angeben. Melden Sie sich mit dem lokalen Administratorkonto an.  
  
3.  Verbinden Sie 2 Edge1 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Verbinden Sie einen Netzwerkadapter mit dem Subnetz 2-Corpnet und dem anderen mit dem simulierten Internet.  
  
## <a name="configure-tcpip-properties"></a><a name="tcpip"></a>Konfigurieren von TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie unter **Netzwerkverbindungen**mit der rechten Maustaste auf die Netzwerkverbindung, die mit dem Subnetz 2-Corpnet verbunden ist, klicken Sie auf **Umbenennen**, geben Sie **2-Corpnet**ein, und drücken Sie die EINGABETASTE.  
  
3.  Klicken Sie mit der rechten Maustaste auf **2-Corpnet**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie in **IP-Adresse** **10.2.0.20**ein, geben Sie in **Subnetzmaske** **255.255.255.0**ein.  
  
6.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. Geben Sie unter **Bevorzugter DNS-Server** **10.2.0.1 bis**ein, und geben Sie in **Alternativer DNS-Server** **10.0.0.1**ein.  
  
7.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
8.  Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
9. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
10. Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in **IPv6-Adresse** **2001: db8:2:: 20**, in **Subnetzpräfix-Länge**den Wert **64**ein. Klicken Sie auf **folgende DNS-Serveradressen verwenden**, und geben Sie unter **Bevorzugter DNS-Server** **2001: db8:2:: 1**, auf dem **alternativen DNS-Server**den Namen **2001: db8:1:: 1 ein**.  
  
11. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
12. Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
13. Klicken Sie im Dialogfeld **Eigenschaften von 2 Corpnet** auf **Schließen**.  
  
14. Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf die Netzwerkverbindung, die mit dem Subnetz Internet verbunden ist, klicken Sie auf **Umbenennen**, geben Sie **Internet**ein, und drücken Sie dann die EINGABETASTE.  
  
15. Klicken Sie mit der rechten Maustaste auf **Internet**, und klicken Sie dann auf **Eigenschaften**.  
  
16. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
17. Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **131.107.0.20**ein. Geben Sie im Feld **Subnetzmaske** den Wert **255.255.255.0** ein.  
  
18. Klicken Sie auf **Erweitert**. Klicken Sie auf der Registerkarte **IP-Einstellungen** im Bereich **IP-Adressen** auf **Hinzufügen**. Geben Sie im Dialogfeld **TCP/IP-Adresse** unter **IP-Adressentyp** **131.107.0.21**unter **Subnetzmaske** den Wert **255.255.255.0**ein, und klicken Sie dann auf **Hinzufügen**.  
  
19. Klicken Sie auf die Registerkarte **DNS**.  
  
20. Geben Sie unter **DNS-Suffix für diese Verbindung** **ISP.example.com**ein, klicken Sie zweimal auf **OK** , und klicken Sie dann auf **Schließen**.  
  
21. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="configure-routing-between-subnets"></a><a name="routing"></a>Konfigurieren des Routings zwischen Subnetzen  
  
1.  Geben Sie auf dem **Start** Bildschirm**cmd. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Geben Sie im Eingabe Aufforderungs Fenster die folgenden Befehle ein. Drücken Sie nach dem Eingeben der einzelnen Befehle die EINGABETASTE.  
  
    ```  
    netsh interface IPv4 add route 10.0.0.0/24 2-Corpnet 10.2.0.254  
    netsh interface IPv6 add route 2001:db8:1::/64 2-Corpnet 2001:db8:2::fe  
    ```  
  
3.  Geben Sie **ping dc1.Corp.contoso.com**ein, um die Netzwerkkommunikation zwischen 2 Edge1 und DC1 zu überprüfen.  
  
4.  Stellen Sie sicher, dass vier Antworten von der IPv4-Adresse, 10.0.0.1 oder der IPv6-Adresse "2001: db8:1:: 1" vorhanden sind.  
  
5.  Schließen Sie das Eingabeaufforderungsfenster.  
  
## <a name="join-2-edge1-to-the-corp2-domain"></a><a name="Join"></a>Join 2 Edge1 zur CORP2-Domäne  
  
1.  Klicken Sie in der Server-Manager Konsole unter **lokaler Server**im Bereich **Eigenschaften** neben **Computer Name**auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  Geben Sie im Dialogfeld **Computername/Domänen Änderungen** unter **Computername den Namen** **2-Edge1**ein. Klicken Sie unter **Mitglied von**auf **Domäne**, geben Sie **corp2.Corp.contoso.com**ein, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden, geben Sie **Administrator** und Kennwort ein, und klicken Sie dann auf **OK**.  
  
5.  Wenn ein Dialogfeld angezeigt wird, in dem Sie zur Domäne corp2.Corp.contoso.com Willkommen werden, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Klicken Sie nach dem Neustart des Computers auf **Benutzer wechseln**und dann auf **anderer Benutzer** , und melden Sie sich bei der Domäne CORP2 mit dem Administrator Konto an.  
  
## <a name="obtain-certificates-on-2-edge1"></a><a name="certs"></a>Abrufen von Zertifikaten auf 2-Edge1  
  
1.  Geben Sie auf dem **Start** Bildschirm**MMC. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolen Struktur des Zertifikate-Snap-Ins den Bereich **Zertifikate (lokaler Computer) \persönlich**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **persönlich**, zeigen Sie auf **alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Zertifikate anfordern** die Kontrollkästchen **Client-Server-Authentifizierung** und **Webserver** aus, und klicken Sie dann auf **Weitere Informationen sind erforderlich, um dieses Zertifikat zu registrieren**.  
  
8.  Wählen Sie im Dialogfeld **Zertifikat Eigenschaften** auf der **Registerkarte** Antragsteller im Bereich Antragsteller **Name** unter **Typ**den **Namen allgemeiner Name**aus.  
  
9. Geben Sie **2-Edge1.contoso.com**in **value**ein, und klicken Sie dann auf **Hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. Geben Sie **2-Edge1.contoso.com**in **value**ein, und klicken Sie dann auf **Hinzufügen**.  
  
12. Geben Sie auf der Registerkarte **Allgemein** unter Anzeige **Name den Namen** **IP-HTTPS-Zertifikat**ein.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, ob ein neues Zertifikat mit dem Namen 2-Edge1.contoso.com mit dem beabsichtigten Zweck der Server Authentifizierung registriert wurde und ein neues Zertifikat mit dem Namen 2-Edge1.corp2.Corp.contoso.com bei registriert wurde. Beabsichtigte Zwecke der Client Authentifizierung und Server Authentifizierung.  
  
15. Schließen Sie das Konsolenfenster. Wenn Sie zum Speichern der Einstellungen aufgefordert werden, klicken Sie auf **Nein**.  
  
## <a name="provide-access-to-corpuser1"></a><a name="Access"></a>Gewähren des Zugriffs auf "corp\user1"  
  
1.  Geben Sie auf dem **Start** Bildschirm**compmgmt. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich auf **lokale Benutzer und Gruppen**.  
  
3.  Doppelklicken Sie auf **Gruppen**, und doppelklicken Sie dann auf **Administratoren**.  
  
4.  Klicken Sie im Dialogfeld **Administrator Eigenschaften** auf **Hinzufügen**, und klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** auf Speicher **Orte**.  
  
5.  Klicken Sie im Dialogfeld Speicher **Orte** in der Struktur **Speicherort** auf **Corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie unter **Geben Sie die zu** entwernenden Objektnamen ein **User1**ein, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Administrator Eigenschaften** auf **OK**.  
  
8.  Schließen Sie das Fenster Computerverwaltung.  
  
## <a name="install-the-remote-access-role-on-2-edge1"></a><a name="InstallDA"></a>Installieren der Remote Zugriffs Rolle auf 2 Edge1  
  
1.  Klicken Sie in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der**Serverrollen auswählen**die Option**RAS**klicken Sie auf**Features hinzufügen**und klicken Sie dann auf**Weiter**.  
  
4.  Klicken Sie fünfmal auf **Weiter**.  
  
5.  Klicken Sie im Dialogfeld **Installationsauswahl bestätigen** auf **Installieren**.  
  
6.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  


