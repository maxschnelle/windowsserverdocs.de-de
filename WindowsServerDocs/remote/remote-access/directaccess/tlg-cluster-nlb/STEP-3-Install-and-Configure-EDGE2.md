---
title: Schritt 3 installieren und Konfigurieren von EDGE2
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f04eb11e-ed5f-42a1-a77b-57a248ba2d10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0692d47d50d84a66b5c3cc41d2ba2fca1004cafe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870881"
---
# <a name="step-3-install-and-configure-edge2"></a>Schritt 3 installieren und Konfigurieren von EDGE2

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

EDGE2 ist das zweite Element eine Testumgebungsbereitstellung eines remotezugriffsclusters. EDGE2 installiert und konfiguriert werden, vor dem Aktivieren der Clusterkonfiguration.

Führen Sie die folgenden Schritte zum Konfigurieren von EDGE2:

## <a name="installOS"></a>Installieren Sie das Betriebssystem auf von EDGE2  
  
1.  Starten Sie auf EDGE2 die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 aus.  
  
2.  Führen Sie die Anweisungen zum Abschließen der Installations und geben Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administratorkonto an. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden von EDGE2 mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden Sie einen Netzwerkadapter, mit dem Corpnet-Subnetz oder den virtuellen Switch, der das Subnetz "Corpnet" und die andere für Internet-Subnetz oder denselben virtuellen Switch, der das Internet-Subnetz darstellt darstellt.  
  
## <a name="TCP"></a>Konfigurieren Sie TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  In der **Netzwerkverbindungen** rechten Maustaste auf die Netzwerkverbindung, die mit dem Subnetz "Corpnet" oder den virtuellen Switch verbunden ist, und klicken Sie dann auf **umbenennen**.  
  
3.  Typ **"Corpnet"**, und drücken Sie dann die EINGABETASTE.  
  
4.  Mit der rechten Maustaste **"Corpnet"**, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
6.  Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.0.0.8**. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein.  
  
7.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. Geben Sie im Feld **Bevorzugter DNS-Server** den Wert **10.0.0.1** ein.  
  
8.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
9. In **DNS-Suffix für diese Verbindung**, Typ **"corp.contoso.com"**, klicken Sie auf **OK** zweimal.  
  
10. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
11. Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:1::8**. In **Subnetzpräfixlänge**, Typ **64**.  
  
12. Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. In **Bevorzugter DNS-Server**, Typ **2001:db8:1::1**.  
  
13. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
14. In **DNS-Suffix für diese Verbindung**, Typ **"corp.contoso.com"**, klicken Sie auf **OK** zweimal aus, und klicken Sie dann auf **schließen**.  
  
15. In der **Netzwerkverbindungen** rechten Maustaste auf die Netzwerkverbindung, die mit dem Internet-Subnetz verbunden ist, und klicken Sie dann auf **umbenennen**.  
  
16. Typ **Internet**, und drücken Sie dann die EINGABETASTE.  
  
17. Klicken Sie mit der rechten Maustaste auf **Internet**, und klicken Sie dann auf **Eigenschaften**.  
  
18. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
19. Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, geben Sie **131.107.0.8**. In **Subnetzmaske**, geben Sie **255.255.255.0**.  
  
20. Klicken Sie auf die **DNS** Registerkarte  
  
21. In **DNS-Suffix für diese Verbindung**, Typ **isp.example.com**, und klicken Sie dann auf **OK** zweimal aus, und klicken Sie dann auf **schließen**.  
  
22. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
23. Um die Netzwerkkommunikation zwischen EDGE2 und DC1 zu überprüfen, klicken Sie auf **starten**, Typ **Cmd**, und drücken Sie dann die EINGABETASTE.  
  
24. Geben Sie im Eingabeaufforderungsfenster Befehl **ping dc1.corp.contoso.com** und drücken Sie EINGABETASTE. Stellen Sie sicher, dass vier Antworten von 10.0.0.1 vorhanden sind oder die IPv6-Adresse 2001:db8:1::1  
  
25. Schließen Sie das Eingabeaufforderungsfenster.  
  
## <a name="rename"></a>Umbenennen von EDGE2, und fügen Sie ihn in die Domäne  
  
1.  In der Server-Manager-Konsole in **lokalen Server**in die **Eigenschaften** Bereich, der neben **Computername**, klicken Sie auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  Auf der **Änderung des Computernamens bzw. der Domäne** Dialogfeld die **Computername** geben **EDGE2**. In der **Mitglied** Bereich, klicken Sie auf **Domäne**, und geben Sie in das Textfeld ein **"corp.contoso.com"**, und klicken Sie dann auf **OK**.  
  
4.  Geben Sie, wenn Sie zur Angabe eines Benutzernamens und eines Kennworts aufgefordert werden, **User1** und das zugehörige Kennwort ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **OK**, wenn das Begrüßungsdialogfeld für die Domäne %%amp;quot;corp.contoso.com%%amp;quot; angezeigt wird.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Nach dem Neustart, melden Sie sich als "corp\user1".  
  
## <a name="IPHTTPSCert"></a>Installieren Sie das IP-HTTPS-Zertifikat  
  
1.  Auf der **starten** geben**mmc.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Auf der **hinzufügen oder Entfernen von-Snap-ins** Dialogfeld klicken Sie auf **Zertifikate**, klicken Sie auf **hinzufügen**, klicken Sie auf **Computerkonto**, klicken Sie auf  **Nächste**, klicken Sie auf **Fertig stellen**, und klicken Sie dann auf **OK**.  
  
4.  Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \Personal\Certificates**. Klicken Sie mit der rechten Maustaste auf die **Zertifikate** Knoten, zeigen Sie auf **alle Aufgaben**, und klicken Sie dann auf **neues Zertifikat anfordern**.  
  
5.  Klicken Sie auf den Assistenten für die Zertifikatregistrierung auf **Weiter** zweimal.  
  
6.  Auf der **Zertifikate anfordern** Seite die **Webserver** , und klicken Sie dann auf **zusätzliche Informationen für diese zertifikatsregistrierung benötigt**.  
  
7.  Auf der **Zertifikateigenschaften** Dialogfelds die **Betreff** Registerkarte die **Antragstellername** Bereich in der **Typ** auf **Allgemeiner Name**.  
  
8.  In **Wert**, Typ **edge1.contoso.com**, und klicken Sie dann auf **hinzufügen**.  
  
9. In der **alternativen Namen** Bereich, in der **Typ** auf **DNS**.  
  
10. In **Wert**, Typ **edge1.contoso.com**, und klicken Sie dann auf **hinzufügen**.  
  
11. Auf der **allgemeine** Registerkarte **Anzeigenamen**, Typ **IP-HTTPS-Zertifikat**.  
  
12. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
13. Stellen Sie sicher, dass ein neues Zertifikat mit dem Namen edge1.contoso.com bei vorgesehen Zwecke registriert wurde, klicken Sie im Detailbereich des Zertifikat-Snap-in.  
  
14. Das Konsolenfenster zu schließen. Wenn Sie aufgefordert werden, um Einstellungen zu speichern, klicken Sie auf **keine**.  
  
## <a name="InstallDA"></a>Installieren Sie die remotezugriffsrolle auf EDGE2  
  
1.  In der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der**Serverrollen auswählen**die Option**RAS**klicken Sie auf**Features hinzufügen**und klicken Sie dann auf**Weiter**.  
  
4.  Klicken Sie fünfmal auf **Weiter**.  
  
5.  Klicken Sie im Dialogfeld **Installationsauswahl bestätigen** auf **Installieren**.  
  
6.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  


