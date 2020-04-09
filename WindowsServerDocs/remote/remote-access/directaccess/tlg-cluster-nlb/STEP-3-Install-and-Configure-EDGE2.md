---
title: Schritt 3 installieren und Konfigurieren von EDGE2
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: f04eb11e-ed5f-42a1-a77b-57a248ba2d10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f50103777fafee330d37e2523dc6371e3a32c81d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819293"
---
# <a name="step-3-install-and-configure-edge2"></a>Schritt 3 installieren und Konfigurieren von EDGE2

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

EDGE2 ist das zweite Mitglied eines Remote Zugriffs Clusters. EDGE2 wird vor dem Aktivieren der Cluster Konfiguration installiert und konfiguriert.

Führen Sie die folgenden Schritte aus, um EDGE2 zu konfigurieren:

## <a name="install-the-operating-system-on-edge2"></a><a name="installOS"></a>Installieren des Betriebssystems auf EDGE2  
  
1.  Starten Sie auf EDGE2 die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Befolgen Sie die Anweisungen, um die Installation abzuschließen, indem Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administrator Konto angeben. Melden Sie sich mit dem lokalen Administratorkonto an.  
  
3.  Verbinden Sie EDGE2 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Verbinden Sie einen Netzwerkadapter mit dem Subnetz "Corpnet" oder dem virtuellen Switch, der das Subnetz "Corpnet" darstellt, und der andere mit dem Internet Subnetz oder dem virtuellen Switch, der das Internet-Subnetz darstellt.  
  
## <a name="configure-tcpip-properties"></a><a name="TCP"></a>Konfigurieren von TCP/IP-Eigenschaften  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf die Netzwerkverbindung, die mit dem Subnetz "Corpnet" oder dem virtuellen Switch verbunden ist, und klicken Sie dann auf **Umbenennen**.  
  
3.  Geben Sie **Corpnet**ein, und drücken Sie dann die EINGABETASTE.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Corpnet**, und klicken Sie auf **Eigenschaften**.  
  
5.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
6.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **10.0.0.8**ein. Geben Sie im Feld **Subnetzmaske** den Wert **255.255.255.0** ein.  
  
7.  Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. Geben Sie im Feld **Bevorzugter DNS-Server** den Wert **10.0.0.1** ein.  
  
8.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
9. Geben Sie unter **DNS-Suffix für diese Verbindung** **Corp.contoso.com**ein, und klicken Sie zweimal auf **OK** .  
  
10. Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
11. Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in der **IPv6-Adresse** **2001: db8:1:: 8 ein**. Geben Sie unter **Subnetzpräfix-Länge**den Wert **64**ein.  
  
12. Klicken Sie auf **Folgende DNS-Serveradressen verwenden**. Geben Sie unter **Bevorzugter DNS-Server** **2001: db8:1:: 1**ein.  
  
13. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
14. Geben Sie unter **DNS-Suffix für diese Verbindung** **Corp.contoso.com**ein, klicken Sie zweimal auf **OK** , und klicken Sie dann auf **Schließen**.  
  
15. Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf die Netzwerkverbindung, die mit dem Subnetz Internet verbunden ist, und klicken Sie dann auf **Umbenennen**.  
  
16. Geben Sie **Internet**ein, und drücken Sie die EINGABETASTE.  
  
17. Klicken Sie mit der rechten Maustaste auf **Internet**, und klicken Sie dann auf **Eigenschaften**.  
  
18. Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
19. Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie in **IP-Adresse** **131.107.0.8**ein. Geben Sie **255.255.255.0**in **Subnetzmaske**ein.  
  
20. Klicken Sie auf die Registerkarte **DNS**  
  
21. Geben Sie unter **DNS-Suffix für diese Verbindung** **ISP.example.com**ein, und klicken Sie dann zweimal auf **OK** , und klicken Sie dann auf **Schließen**.  
  
22. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
23. Zum Überprüfen der Netzwerkkommunikation zwischen EDGE2 und DC1 klicken Sie auf **Start**, geben Sie **cmd**ein, und drücken Sie dann die EINGABETASTE.  
  
24. Geben Sie im Eingabe Aufforderungs Fenster **ping dc1.Corp.contoso.com** ein, und drücken Sie die EINGABETASTE. Vergewissern Sie sich, dass vier Antworten von 10.0.0.1 oder der IPv6-Adresse 2001: db8:1:: 1 vorhanden sind.  
  
25. Schließen Sie das Eingabeaufforderungsfenster.  
  
## <a name="rename-edge2-and-join-it-to-the-domain"></a><a name="rename"></a>EDGE2 umbenennen und der Domäne beitreten  
  
1.  Klicken Sie in der Server-Manager Konsole unter **lokaler Server**im Bereich **Eigenschaften** neben **Computer Name**auf den Link.  
  
2.  Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
3.  Geben Sie im Dialogfeld **Computername/Domänen Änderungen** im Feld **Computername** den Namen **EDGE2**ein. Klicken Sie im Bereich **Mitglied von** auf **Domäne**, geben Sie im Textfeld **Corp.contoso.com**ein, und klicken Sie dann auf **OK**.  
  
4.  Geben Sie, wenn Sie zur Angabe eines Benutzernamens und eines Kennworts aufgefordert werden, **User1** und das zugehörige Kennwort ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie, wenn das Begrüßungsdialogfeld für die Domäne %%amp;quot;corp.contoso.com%%amp;quot; angezeigt wird, auf **OK**.  
  
6.  Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
7.  Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
8.  Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
9. Melden Sie sich nach dem Neustart als corp\user1 an.  
  
## <a name="install-the-ip-https-certificate"></a><a name="IPHTTPSCert"></a>Installieren des IP-HTTPS-Zertifikats  
  
1.  Geben Sie auf dem **Start** Bildschirm**MMC. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen bzw. entfernen** auf **Zertifikate**, klicken Sie auf **Hinzufügen**, klicken Sie auf **Computer Konto**, klicken Sie auf **weiter**, klicken Sie auf **Fertig**stellen und dann auf **OK**.  
  
4.  Navigieren Sie im linken Bereich der Konsole zu **Zertifikate (lokaler Computer) \personal\zertifikate**. Klicken Sie mit der rechten Maustaste auf den Knoten **Zertifikate** , zeigen Sie auf **Alle Tasks**, und klicken Sie dann auf **Neues Zertifikat anfordern**  
  
5.  Klicken Sie im Assistenten für die Zertifikat Registrierung zweimal auf **weiter** .  
  
6.  Aktivieren Sie auf der Seite **Zertifikate anfordern** das Kontrollkästchen **Webserver** , und klicken Sie dann auf **Weitere Informationen sind erforderlich, um sich für dieses Zertifikat anzumelden**.  
  
7.  Klicken Sie im Dialogfeld **Zertifikat Eigenschaften** **auf der Register** Karte Antragsteller im Bereich Antragsteller **Name** in der Liste **Typ** auf allgemeiner **Name**.  
  
8.  Geben Sie **Edge1.contoso.com**in **value**ein, und klicken Sie dann auf **Hinzufügen**.  
  
9. Klicken Sie im Bereich **alternativer Name** in der Liste **Typ** auf **DNS**.  
  
10. Geben Sie **Edge1.contoso.com**in **value**ein, und klicken Sie dann auf **Hinzufügen**.  
  
11. Geben Sie auf der Registerkarte **Allgemein** unter Anzeige **Name den Namen** **IP-HTTPS-Zertifikat**ein.  
  
12. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
13. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, ob ein neues Zertifikat mit dem Namen Edge1.contoso.com mit dem vorgesehenen Zweck der Server Authentifizierung registriert wurde.  
  
14. Schließen Sie das Konsolenfenster. Wenn Sie zum Speichern der Einstellungen aufgefordert werden, klicken Sie auf **Nein**.  
  
## <a name="install-the-remote-access-role-on-edge2"></a><a name="InstallDA"></a>Installieren der Remote Zugriffs Rolle auf EDGE2  
  
1.  Klicken Sie in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der**Serverrollen auswählen**die Option**RAS**klicken Sie auf**Features hinzufügen**und klicken Sie dann auf**Weiter**.  
  
4.  Klicken Sie fünfmal auf **Weiter**.  
  
5.  Klicken Sie im Dialogfeld **Installationsauswahl bestätigen** auf **Installieren**.  
  
6.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  


