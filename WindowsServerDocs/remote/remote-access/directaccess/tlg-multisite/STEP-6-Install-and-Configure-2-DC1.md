---
title: 'Schritt 6: Installieren und Konfigurieren von 2-DC1'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 3d66901a-c40b-474c-9948-f989f399cfea
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 21591de4527cc33857e215d9521f2f1458c1f3c6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861563"
---
# <a name="step-6-install-and-configure-2-dc1"></a>Schritt 6: Installieren und Konfigurieren von 2-DC1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

2 DC1 stellt die folgenden Dienste bereit:  
  
-   Ein Domänen Controller für die Domäne corp2.Corp.contoso.com Active Directory Domain Services (AD DS).  
  
-   Einen DNS-Server für die DNS-Domäne corp2.Corp.contoso.com.  
  
2: die DC1-Konfiguration besteht aus folgendem:  
  
- Installieren des Betriebssystems auf 2-DC1
  
- Konfigurieren von TCP/IP-Eigenschaften

- Konfigurieren von 2 DC1 als Domänen Controller und DNS-Server

- Geben Sie Gruppenrichtlinie Berechtigungen für corp\user1 an.
  
- CORP2 Computern das Abrufen von Computer Zertifikaten gestatten
  
- Erzwingen der Replikation zwischen DC1 und 2-DC1
  
## <a name="install-the-operating-system-on-2-dc1"></a>Installieren des Betriebssystems auf 2-DC1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
### <a name="to-install-the-operating-system-on-2-dc1"></a>So installieren Sie das Betriebssystem auf 2-DC1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Befolgen Sie die Anweisungen, um die Installation abzuschließen, indem Sie Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administrator Konto angeben. Melden Sie sich mit dem lokalen Administratorkonto an.  
  
3.  Verbinden Sie 2 DC1 mit einem Netzwerk, das über Internet Zugriff verfügt, und führen Sie Windows Update aus, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 zu installieren, und trennen Sie dann die Verbindung mit dem Internet.  
  
4.  Verbinden Sie 2 DC1 mit dem Subnetz 2-Corpnet.  
  
## <a name="configure-tcpip-properties"></a>Konfigurieren von TCP/IP-Eigenschaften  
Konfigurieren Sie das TCP/IP-Protokoll mit statischen IP-Adressen.  
  
### <a name="to-configure-tcpip-on-2-dc1"></a>So konfigurieren Sie TCP/IP auf 2 DC1  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie unter **Netzwerkverbindungen** mit der rechten Maustaste auf **Verkabelte Ethernetverbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. Geben Sie unter **IP-Adresse**den Namen **10.2.0.1 bis**ein. Geben Sie im Feld **Subnetzmaske** den Wert **255.255.255.0** ein. Geben Sie unter **Standard Gateway**den Namen **10.2.0.254**ein. Klicken Sie auf **folgende DNS-Serveradressen verwenden**, geben Sie unter **Bevorzugter DNS-Server**den Namen **10.2.0.1 bis**ein, und geben Sie in **Alternativer DNS-Server** **10.0.0.1**ein.  
  
5.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
6.  Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
7.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
8.  Klicken Sie auf **folgende IPv6-Adresse verwenden**. Geben Sie in der **IPv6-Adresse** **2001: db8:2:: 1 ein**. Geben Sie unter **Subnetzpräfix-Länge**den Wert **64**ein. Geben Sie unter **Standard Gateway**den Wert **2001: db8:2:: FE**ein. Klicken Sie auf **folgende DNS-Serveradressen verwenden**, geben Sie unter **Bevorzugter DNS-Server**den Namen **2001: db8:2:: 1 ein**, und geben Sie im **alternativen DNS-Server** **2001: db8:1:: 1**ein.  
  
9. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
10. Geben Sie unter **DNS-Suffix für diese Verbindung** **corp2.Corp.contoso.com**ein, und klicken Sie dann zweimal auf **OK** .  
  
11. Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Schließen**.  
  
12. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
13. Klicken Sie in der Server-Manager Konsole unter **lokaler Server**im Bereich **Eigenschaften** neben **Computer Name**auf den Link.  
  
14. Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
15. Geben Sie im Dialogfeld **Computername/Domänen Änderungen** unter **Computername den Namen** **2-DC1**ein, und klicken Sie dann auf **OK**.  
  
16. Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
17. Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
18. Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
19. Melden Sie sich nach dem Neustart mit dem lokalen Administrator Konto an.  
  
## <a name="configure-2-dc1-as-a-domain-controller-and-dns-server"></a>Konfigurieren von 2 DC1 als Domänen Controller und DNS-Server  
Konfigurieren Sie 2 DC1 als Domänen Controller für die corp2.Corp.contoso.com-Domäne und als DNS-Server für die corp2.Corp.contoso.com DNS-Domäne.  
  
### <a name="to-configure-2-dc1-as-a-domain-controller-and-dns-server"></a>So konfigurieren Sie 2 DC1 als Domänen Controller und DNS-Server  
  
1.  Klicken Sie in der Server-Manager-Konsole auf dem **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **weiter** , um zum Bildschirm für die Server Rollenauswahl zu gelangen.  
  
3.  Wählen Sie auf der Seite **Server Rollen auswählen** die Option **Active Directory Domain Services**aus. Klicken Sie bei entsprechender Aufforderung auf **Features hinzufügen** , und klicken Sie dann dreimal auf **weiter** .  
  
4.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
5.  Wenn die Installation erfolgreich abgeschlossen wurde, klicken Sie auf **Server zu einem Domänen Controller**herauf Stufen.  
  
6.  Klicken Sie im Konfigurations-Assistenten für Active Directory Domain Services auf der Seite **Bereitstellungs Konfiguration** auf **neue Domäne einer vorhandenen Gesamtstruktur hinzufügen**.  
  
7.  Geben Sie unter Name der über **geordneten Domäne** **Corp.contoso.com**ein, geben Sie unter **neuer Domänen Name den Namen** **corp2**ein.  
  
8.  Klicken Sie unter Geben Sie **die Anmelde Informationen an, um diesen Vorgang auszuführen**, auf **ändern**. Geben Sie im Dialogfeld **Windows-Sicherheit** unter **Benutzername den Namen**Corp. Configuration. **com\administrator**ein, und geben Sie im Feld **Kennwort**das Kennwort corp\administrator ein, klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.  
  
9. Vergewissern Sie sich auf der Seite **Domänen Controller Optionen** , dass der **Name des Standorts** auf der **zweiten**Seite liegt. Geben Sie unter **Kennwort** und **Kennwort bestätigen**ein Kennwort für **den Verzeichnisdienst-Wiederherstellungs Modus (DSRM**-Kennwort) ein, und klicken Sie dann zweimal auf **weiter** .  
  
10. Klicken Sie nach der Überprüfung der Voraussetzungen auf der Seite Voraussetzungs **Prüfung** auf **Installieren**.  
  
11. Warten Sie, bis der Assistent die Konfiguration von Active Directory und DNS-Diensten abgeschlossen hat, und klicken Sie dann auf **Schließen**.  
  
12. Nachdem der Computer neu gestartet wurde, melden Sie sich mit dem Administrator Konto bei der CORP2-Domäne an.  
  
## <a name="provide-group-policy-permissions-to-corpuser1"></a>Geben Sie Gruppenrichtlinie Berechtigungen für corp\user1 an.  
Verwenden Sie dieses Verfahren, um den Benutzer "corp\user1" mit vollen Berechtigungen zum Erstellen und Ändern von corp2-Gruppenrichtlinie Objekten bereitzustellen.  
  
### <a name="to-provide-group-policy-permissions"></a>So geben Sie Gruppenrichtlinie Berechtigungen an  
  
1.  Geben Sie auf dem **Start** Bildschirm**GPMC. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Gruppenrichtlinie-Verwaltungskonsole die Struktur " **Forest: Corp.contoso.com/Domains/corp2.Corp.contoso.com**".  
  
3.  Klicken Sie im Detailbereich auf die Registerkarte **Delegierung** . Klicken Sie in der Dropdown Liste **Berechtigung** auf Gruppenrichtlinien Objekte **Verknüpfen**.  
  
4.  Klicken Sie auf **Hinzufügen**, und klicken Sie im Dialogfeld Neuer **Benutzer, Computer oder Gruppe auswählen** auf Speicher **Orte**.  
  
5.  Klicken Sie im Dialogfeld Speicher **Orte** in der Struktur **Speicherort** auf **Corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
6.  Klicken Sie im Feld **Geben Sie den Namen des zu ausgewäfgenden Objekts** ein **User1**auf **OK**, und klicken Sie im Dialogfeld **Gruppe oder Benutzer hinzufügen** auf **OK**.  
  
7.  Klicken Sie in der Gruppenrichtlinie-Verwaltungskonsole in der Struktur auf **Objekte Gruppenrichtlinie**, und klicken Sie im Detailbereich auf die Registerkarte **Delegierung** .  
  
8.  Klicken Sie auf **Hinzufügen**, und klicken Sie im Dialogfeld Neuer **Benutzer, Computer oder Gruppe auswählen** auf Speicher **Orte**.  
  
9. Klicken Sie im Dialogfeld Speicher **Orte** in der Struktur **Speicherort** auf **Corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
10. Klicken Sie in **Geben Sie den Namen des zu ausgewäfartigen Objekts** ein **User1**auf **OK**.  
  
11. Klicken Sie in der Gruppenrichtlinie-Verwaltungskonsole in der Struktur auf **WMI-Filter**, und klicken Sie im Detailbereich auf die Registerkarte **Delegierung** .  
  
12. Klicken Sie auf **Hinzufügen**, und klicken Sie im Dialogfeld Neuer **Benutzer, Computer oder Gruppe auswählen** auf Speicher **Orte**.  
  
13. Klicken Sie im Dialogfeld Speicher **Orte** in der Struktur **Speicherort** auf **Corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
14. Klicken Sie in **Geben Sie den Namen des zu ausgewäfartigen Objekts** ein **User1**auf **OK**. Vergewissern Sie sich, dass im Dialogfeld **Gruppe oder Benutzer hinzufügen** die **Berechtigungen** auf **voll**Zugriff festgelegt sind, und klicken Sie dann auf **OK**.  
  
15. Schließen Sie die Gruppenrichtlinien-Verwaltungskonsole.  
  
## <a name="allow-corp2-computers-to-obtain-computer-certificates"></a>CORP2 Computern das Abrufen von Computer Zertifikaten gestatten 

Computer in der CORP2-Domäne müssen Computer Zertifikate von der Zertifizierungsstelle auf App1 abrufen. Führen Sie dieses Verfahren auf App1 aus.  
  
### <a name="to-allow-corp2-computers-to-automatically-obtain-computer-certificates"></a>So ermöglichen Sie CORP2-Computern das automatische Abrufen von Computer Zertifikaten  
  
1.  Klicken Sie auf App1 auf **Start**, geben Sie **certtmpl. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Doppelklicken Sie in der **Zertifikat Vorlagen Konsole**im mittleren Bereich auf **Client-Server-Authentifizierung**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften von Client-Server-Authentifizierung** auf die Registerkarte **Sicherheit** .  
  
4.  Klicken Sie auf **Hinzufügen**, und klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** auf Speicher **Orte**.  
  
5.  Erweitern Sie im Dialogfeld Speicher **Orte** unter **Speicherort**die Option **Corp.contoso.com**, klicken Sie auf **corp2.Corp.contoso.com**, und klicken Sie dann auf **OK**.  
  
6.  **Geben Sie unter Geben Sie die zu**entwerfbaren Objektnamen ein die Zeichen **Domäne Admins Domänen Computer** , und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Eigenschaften von Client-Server-Authentifizierung** unter **Gruppen-oder Benutzernamen**auf **Domänen-Admins (CORP2\Domain Admins)** , und wählen Sie in **Berechtigungen für Domänen Administratoren**in der Spalte **zulassen** die Option **Schreiben** und **Anmelden**aus.  
  
8.  Klicken Sie unter **Gruppen-oder Benutzernamen**auf **Domänen Computer (CORP2\Domain-Computer)** , und wählen Sie unter **Berechtigungen für Domänen Computer**in der Spalte **zulassen** die **Option registrieren und** **automatisch registrieren**aus, und klicken Sie dann auf **OK**.  
  
9. Schließen Sie die Zertifikatvorlagenkonsole.  
  
## <a name="force-replication-between-dc1-and-2-dc1"></a><a name="replication"></a>Erzwingen der Replikation zwischen DC1 und 2-DC1  
Bevor Sie sich für Zertifikate bei 2 Edge1 registrieren können, müssen Sie die Replikation von Einstellungen von DC1 zu 2-DC1 erzwingen. Dieser Vorgang sollte auf DC1 ausgeführt werden.  
  
### <a name="to-force-replication"></a>Erzwingen der Replikation  
  
1.  Klicken Sie auf DC1 auf **Start**, und klicken Sie dann auf **Active Directory Websites und Dienste**.  
  
2.  Erweitern Sie in der Konsole Active Directory Standorte und Dienste in der Struktur **standortübergreifende Transporte**, und klicken Sie dann auf **IP**.  
  
3.  Doppelklicken Sie im Detailbereich auf **DEFAULTIPSITELINK**.  
  
4.  Geben Sie im Dialogfeld **DEFAULTIPSITELINK-Eigenschaften** unter **Kosten**den Text **1 ein**, geben Sie in **Replizieren alle**den Typ **15**ein, und klicken Sie dann auf **OK**. Warten Sie 15 Minuten, bis die Replikation abgeschlossen ist.  
  
5.  Um die Replikation jetzt in der Konsolen Struktur zu erzwingen, erweitern Sie **Sites\Default-First-Site-name\servers\dc1\ntds Settings**, klicken Sie im Detailbereich mit der rechten Maustaste auf **<automatically generated>** , klicken Sie auf **Jetzt replizieren**, und klicken Sie dann im Dialogfeld **Jetzt replizieren** auf **OK**.  
  
6.  Gehen Sie folgendermaßen vor, um eine erfolgreiche Replikation sicherzustellen:  
  
    1.  Geben Sie auf dem **Start** Bildschirm**cmd. exe**ein, und drücken Sie dann die EINGABETASTE.  
  
    2.  Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
        ```  
        repadmin /syncall /e /A /P /d /q  
        ```  
  
    3.  Stellen Sie sicher, dass alle Partitionen ohne Fehler synchronisiert werden. Wenn nicht, führen Sie den Befehl erneut aus, bis keine Fehler gemeldet werden, bevor Sie den Vorgang fortsetzen.  
  
7.  Schließen Sie das Eingabeaufforderungsfenster.  
  


