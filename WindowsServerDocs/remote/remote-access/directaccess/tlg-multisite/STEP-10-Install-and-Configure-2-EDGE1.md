---
title: Schritt 10 installieren und Konfigurieren von 2-EDGE1
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
ms.assetid: d98d6f7a-a2e6-45b1-9c63-08e2986a5c03
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1640dbae52a1a7c93355b34822d72faa5351bcda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860311"
---
# <a name="step-10-install-and-configure-2-edge1"></a>Schritt 10 installieren und Konfigurieren von 2-EDGE1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

2-EDGE1-Konfiguration umfasst Folgendes:  
  
- Installieren Sie das Betriebssystem auf 2-EDGE1 an. Installieren Sie WindowsServer 2016, Windows Server 2012 R2 oder WindowsServer 2012 auf 2-EDGE1 an.  
  
- Konfigurieren von TCP/IP-Eigenschaften 2-EDGE1 mit statischen Adressen auf beiden Netzwerkschnittstellen zu konfigurieren.  
  
- Konfigurieren des Routings zwischen Subnetzen. Um die Kommunikation zwischen den Subnetzen "Corpnet" und "2-Corpnet" zu ermöglichen, müssen Sie das routing konfigurieren.  
  
- Fügen Sie der Domäne CORP2 2-EDGE1. Fügen Sie der Domäne corp2.corp.contoso.com 2-EDGE1.  
  
- Abrufen von Zertifikaten auf 2-EDGE1. Zertifikate sind erforderlich, damit die IPsec-Verbindung zwischen dem DirectAccess-Clients und RAS-Servers und den IP-HTTPS-Listener zu authentifizieren, wenn Clients über HTTPS herstellen.  
  
- Bieten Sie Zugriff auf "corp\user1" ein. Der Benutzer "corp\user1" ist der Remote-Access-Administrator. Damit diese Benutzer 2-EDGE1 von EDGE1 ändern kann, müssen Sie dem Benutzer Zugriff gewähren.  
  
- Installieren Sie die remotezugriffsrolle auf 2-EDGE1 an. Um eine Bereitstellung für mehrere Standorte zu aktivieren, müssen Sie die Rolle "Remotezugriff" auf 2-EDGE1 installieren.  
  
2-EDGE1 müssen zwei Netzwerkadapter installiert.  
  
## <a name="installOS"></a>Installieren des Betriebssystems auf 2-EDGE1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Führen Sie die Anweisungen zum Abschließen der Installations und geben Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administratorkonto an. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden von 2-EDGE1 mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden Sie eine Netzwerkkarte mit der 2-Corpnet-Subnetz und der andere mit dem simulierten Internet.  
  
## <a name="tcpip"></a>Konfigurieren Sie TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  In **Netzwerkverbindungen**mit der rechten Maustaste auf die Netzwerkverbindung, die mit dem 2-Corpnet-Subnetz verbunden ist, klicken Sie auf **umbenennen**, Typ **2-Corpnet**, und drücken Sie dann die EINGABETASTE.  
  
3.  Mit der rechten Maustaste **2-Corpnet**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.2.0.20**im **Subnetzmaske**, Typ **255.255.255.0**.  
  
6.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. In **Bevorzugter DNS-Server**, Typ **10.2.0.1**, und klicken Sie in **alternativer DNS-Server**, Typ **10.0.0.1**.  
  
7.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
8.  In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK** zweimal.  
  
9. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
10. Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:2::20**im **Subnetzpräfixlänge**, Typ **64**. Klicken Sie auf **verwenden Sie die folgenden DNS-Serveradressen**, und klicken Sie in **Bevorzugter DNS-Server**, Typ **2001:db8:2::1**im **alternativer DNS-Server**, Typ **2001:db8:1::1**.  
  
11. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
12. In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK** zweimal.  
  
13. Auf der **2-Corpnet Eigenschaften** Dialogfeld klicken Sie auf **schließen**.  
  
14. In der **Netzwerkverbindungen** Fenster mit der rechten Maustaste der Netzwerkverbindungs, die mit dem Internet-Subnetz verbunden ist, klicken Sie auf **umbenennen**, Typ **Internet**, und drücken Sie dann die EINGABETASTE .  
  
15. Klicken Sie mit der rechten Maustaste auf **Internet**, und klicken Sie dann auf **Eigenschaften**.  
  
16. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
17. Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **131.107.0.20**. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein.  
  
18. Klicken Sie auf **Erweitert**. Klicken Sie auf der Registerkarte **IP-Einstellungen** im Bereich **IP-Adressen** auf **Hinzufügen**. Auf der **TCP/IP-Adresse** Dialogfeld **IP-Adresse** Typ **131.107.0.21**im **Subnetzmaske** Typ **255.255.255.0** , und klicken Sie dann auf **hinzufügen**.  
  
19. Klicken Sie auf die Registerkarte **DNS**.  
  
20. In **DNS-Suffix für diese Verbindung**, Typ **isp.example.com**, klicken Sie auf **OK** zweimal aus, und klicken Sie dann auf **schließen**.  
  
21. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="routing"></a>Konfigurieren des Routings zwischen Subnetzen  
  
1.  Auf der **starten** geben**cmd.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Befehl die folgenden Befehle aus. Drücken Sie nach der Eingabe jedes Befehls die EINGABETASTE.  
  
    ```  
    netsh interface IPv4 add route 10.0.0.0/24 2-Corpnet 10.2.0.254  
    netsh interface IPv6 add route 2001:db8:1::/64 2-Corpnet 2001:db8:2::fe  
    ```  
  
3.  Um die Netzwerkkommunikation zwischen 2-EDGE1 und DC1 zu überprüfen, geben Sie **ping dc1.corp.contoso.com**.  
  
4.  Stellen Sie sicher, dass es vier Antworten von entweder die IPv4-Adresse 10.0.0.1, sind oder über die IPv6-Adresse, 2001:db8:1::1.  
  
5.  Schließen Sie das Eingabeaufforderungsfenster.  
  
## <a name="Join"></a>Fügen Sie der Domäne CORP2 2-EDGE1  
  
1.  In der Server-Manager-Konsole in **lokalen Server**in die **Eigenschaften** Bereich, der neben **Computername**, klicken Sie auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  Auf der **Änderung des Computernamens bzw. der Domäne** Dialogfeld **Computername**, Typ **2-EDGE1**. In **Mitglied**, klicken Sie auf **Domäne**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
4.  Wenn Sie für einen Benutzernamen und Kennwort aufgefordert werden, geben Sie **Administrator** und dessen Kennwort und klicken Sie dann auf **OK**.  
  
5.  Wenn Sie ein Dialogfeld, das Begrüßungsdialogfeld für die Domäne corp2.corp.contoso.com sehen, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Klicken Sie nach dem Neustart des Computers, auf **Benutzer wechseln**, und klicken Sie dann auf **anderer Benutzer** und melden Sie sich bei der CORP2-Domäne mit dem Administratorkonto an.  
  
## <a name="certs"></a>Abrufen von Zertifikaten auf 2-EDGE1  
  
1.  Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-ins hinzufügen oder entfernen** auf **Zertifikate**, **Hinzufügen**, **Computerkonto**, **Weiter**, **Lokaler Computer**, **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikate-Snap-Ins **Zertifikate (lokaler Computer) \Personal**.  
  
5.  Mit der rechten Maustaste **persönliche**, zeigen Sie auf **alle Aufgaben**, und klicken Sie dann auf **neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite die **Client-/ Serverauthentifizierung** und **Webserver** Kontrollkästchen, und klicken Sie dann auf **Weitere Informationen finden Sie für diese zertifikatsregistrierung benötigt**.  
  
8.  Auf der **Zertifikateigenschaften** das Dialogfeld der **Betreff** Registerkarte der **Antragstellername** Bereich im **Typ**wählen  **Allgemeiner Name**.  
  
9. In **Wert**, Typ **2-edge1.contoso.com**, und klicken Sie dann auf **hinzufügen**.  
  
10. Wählen Sie unter **Alternativer Name** für **Typ** die Option **DNS** aus.  
  
11. In **Wert**, geben Sie **2-edge1.contoso.com**, und klicken Sie dann auf **hinzufügen**.  
  
12. Auf der **allgemeine** Registerkarte **Anzeigenamen**, Typ **IP-HTTPS-Zertifikat**.  
  
13. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
14. Im Detailbereich des Zertifikat-Snap-in stellen Sie sicher, dass ein neues Zertifikat mit dem Name-2-edge1.contoso.com vorgesehen Zwecke registriert wurde, und ein neues Zertifikat mit dem Name-2-edge1.corp2.corp.contoso.com registriert wurde Beabsichtigte Zwecke der Authentifizierung des Clients und Server-Authentifizierung.  
  
15. Das Konsolenfenster zu schließen. Wenn Sie aufgefordert werden, um Einstellungen zu speichern, klicken Sie auf **keine**.  
  
## <a name="Access"></a>Ermöglichen den Zugriff auf "corp\user1"  
  
1.  Auf der **starten** geben**compmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich auf **lokale Benutzer und Gruppen**.  
  
3.  Doppelklicken Sie auf **Gruppen**, und doppelklicken Sie dann auf **Administratoren**.  
  
4.  Auf der **Administratoreigenschaften** Dialogfeld klicken Sie auf **hinzufügen**, und klicken Sie auf die **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** im Dialogfeld klicken Sie auf  **Speicherorte**.  
  
5.  Auf der **Speicherorte** Dialogfeld die **Speicherort** Struktur, klicken Sie auf **"corp.contoso.com"**, und klicken Sie dann auf **OK**.  
  
6.  In der **Geben Sie die zu verwendenden Objektnamen** Typ **"user1"**, und klicken Sie dann auf **OK**.  
  
7.  Auf der **Administratoreigenschaften** Dialogfeld klicken Sie auf **OK**.  
  
8.  Schließen Sie das Fenster "Computerverwaltung".  
  
## <a name="InstallDA"></a>Installieren Sie die remotezugriffsrolle auf 2-EDGE1  
  
1.  In der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der**Serverrollen auswählen**die Option**RAS**klicken Sie auf**Features hinzufügen**und klicken Sie dann auf**Weiter**.  
  
4.  Klicken Sie fünfmal auf **Weiter**.  
  
5.  Klicken Sie im Dialogfeld **Installationsauswahl bestätigen** auf **Installieren**.  
  
6.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  


