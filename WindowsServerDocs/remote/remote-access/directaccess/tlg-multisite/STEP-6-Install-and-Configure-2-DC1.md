---
title: Schritt 6 installieren und Konfigurieren von 2-DC1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d66901a-c40b-474c-9948-f989f399cfea
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8c3e12f9d64619ce00e578c7a8096c764e68ff7d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283159"
---
# <a name="step-6-install-and-configure-2-dc1"></a>Schritt 6 installieren und Konfigurieren von 2-DC1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

2-DC1 bietet die folgenden Dienste:  
  
-   Ein Domänencontroller für die Domäne des corp2.corp.contoso.com Active Directory Domain Services (AD DS).  
  
-   Ein DNS-Server für die corp2.corp.contoso.com DNS-Domäne.  
  
2-DC1-Konfiguration umfasst Folgendes:  
  
- Installieren des Betriebssystems auf 2-DC1
  
- Konfigurieren von TCP/IP-Eigenschaften

- Konfigurieren von 2-DC1 als Domänencontroller und DNS-server

- Gewähren von Gruppenrichtlinien-Berechtigungen für "corp\user1"
  
- Abrufen von Computerzertifikaten CORP2 auf Computern zulassen
  
- Erzwingen der Replikation zwischen DC1 und 2-DC1
  
## <a name="install-the-operating-system-on-2-dc1"></a>Installieren des Betriebssystems auf 2-DC1  
Installieren Sie zunächst Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
### <a name="to-install-the-operating-system-on-2-dc1"></a>So installieren Sie das Betriebssystem auf 2-DC1  
  
1.  Starten Sie die Installation von Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012.  
  
2.  Führen Sie die Anweisungen zum Abschließen der Installations und geben Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 (vollständige Installation) und ein sicheres Kennwort für das lokale Administratorkonto an. Melden Sie sich beim lokalen Administratorkonto an.  
  
3.  Verbinden von 2-DC1 mit einem Netzwerk, das über Internetzugriff verfügt, und führen Sie Windows Update, um die neuesten Updates für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 installieren, und klicken Sie dann aus dem Internet zu trennen.  
  
4.  Verbinden Sie 2-DC1, mit dem 2-Corpnet-Subnetz.  
  
## <a name="configure-tcpip-properties"></a>Konfigurieren von TCP/IP-Eigenschaften  
Konfigurieren Sie das TCP/IP-Protokoll mit statischen IP-Adressen.  
  
### <a name="to-configure-tcpip-on-2-dc1"></a>So konfigurieren Sie TCP/IP auf 2-DC1  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  Klicken Sie unter **Netzwerkverbindungen** mit der rechten Maustaste auf **Verkabelte Ethernetverbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf **Folgende IP-Adresse verwenden**. In **IP-Adresse**, Typ **10.2.0.1**. Geben Sie im Feld **Subnetzmaske**den Wert **255.255.255.0**ein. In **Standardgateway**, Typ **10.2.0.254**. Klicken Sie auf **verwenden Sie die folgenden DNS-Serveradressen**im **Bevorzugter DNS-Server**, Typ **10.2.0.1**, und klicken Sie in **alternativer DNS-Server**, Typ **10.0.0.1**.  
  
5.  Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
6.  In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK** zweimal.  
  
7.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
8.  Klicken Sie auf **verwenden Sie die folgende IPv6-Adresse**. In **IPv6-Adresse**, Typ **2001:db8:2::1**. In **Subnetzpräfixlänge**, Typ **64**. In **Standardgateway**, Typ **2001:db8:2::fe**. Klicken Sie auf **verwenden Sie die folgenden DNS-Serveradressen**im **Bevorzugter DNS-Server**, Typ **2001:db8:2::1**, und klicken Sie in **alternativer DNS-Server**, Typ **2001:db8:1::1**.  
  
9. Klicken Sie auf **Erweitert** und dann auf die Registerkarte **DNS**.  
  
10. In **DNS-Suffix für diese Verbindung**, Typ **corp2.corp.contoso.com**, und klicken Sie dann auf **OK** zweimal.  
  
11. Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld klicken Sie auf **schließen**.  
  
12. Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
13. In der Server-Manager-Konsole in **lokalen Server**in die **Eigenschaften** Bereich, der neben **Computername**, klicken Sie auf den Link.  
  
14. Klicken Sie auf der Registerkarte **Computername** im Dialogfeld **Systemeigenschaften** auf **Ändern**.  
  
15. Auf der **Änderung des Computernamens bzw. der Domäne** Dialogfeld **Computername**, Typ **2-DC1**, und klicken Sie dann auf **OK**.  
  
16. Klicken Sie auf **OK**, wenn Sie zum Neustarten des Computers aufgefordert werden.  
  
17. Klicken Sie im Dialogfeld **Systemeigenschaften** auf **Schließen**.  
  
18. Klicken Sie auf **Jetzt neu starten**, wenn Sie aufgefordert werden, den Computer neu zu starten.  
  
19. Nach dem Neustart, melden Sie sich mit dem lokalen Administratorkonto an.  
  
## <a name="configure-2-dc1-as-a-domain-controller-and-dns-server"></a>Konfigurieren von 2-DC1 als Domänencontroller und DNS-server  
Konfigurieren von 2-DC1 als Domänencontroller für die Domäne corp2.corp.contoso.com und als DNS-Server für die corp2.corp.contoso.com DNS-Domäne.  
  
### <a name="to-configure-2-dc1-as-a-domain-controller-and-dns-server"></a>Zum Konfigurieren von 2-DC1 als Domänencontroller und DNS-server  
  
1.  In der Server-Manager-Konsole auf die **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie auf **Weiter** dreimal, um dem Auswahlbildschirm des Server-Rolle zu erhalten  
  
3.  Auf der **Serverrollen auswählen** Seite **Active Directory Domain Services**. Klicken Sie auf **Features hinzufügen** wenn dazu aufgefordert werden, und klicken Sie dann auf **Weiter** drei Mal.  
  
4.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
5.  Wenn die Installation erfolgreich abgeschlossen wurde, klicken Sie auf **Server zu einem Domänencontroller heraufstufen**.  
  
6.  Die Active Directory-Domäne Konfigurations-Assistenten auf die **Bereitstellungskonfiguration** auf **Hinzufügen einer neuen Domäne zu einer vorhandenen Gesamtstruktur**.  
  
7.  In **Name der übergeordneten Domäne**, Typ **"corp.contoso.com"** im **neuer Domänenname**, Typ **corp2**.  
  
8.  Klicken Sie unter **Geben Sie die Anmeldeinformationen zum Ausführen dieses Vorgangs**, klicken Sie auf **Änderung**. Auf der **Windows Security** Dialogfeld **Benutzernamen**, Typ **corp.contoso.com\Administrator**, und klicken Sie in **Kennwort**, geben Sie die Corp\ Administratorkennwort ein, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Domänencontrolleroptionen** Seite, stellen Sie sicher, dass die **Standortname** ist **Sekunde-Site**. Klicken Sie unter **Geben Sie das Verzeichnis Verzeichnisdienst-Wiederherstellungsmodus (DSRM) Kennwort**im **Kennwort** und **Bestätigungskennwort**, ein sicheres Kennwort zweimal eingeben, und klicken Sie dann auf  **Nächste** fünf Mal.  
  
10. Auf der **Voraussetzungsüberprüfung** Seite, nachdem die erforderlichen Komponenten überprüft wurden, klicken Sie auf **installieren**.  
  
11. Warten Sie, bis der Assistent die Konfiguration der Active Directory und DNS-Dienste abgeschlossen ist, und klicken Sie dann auf **schließen**.  
  
12. Melden Sie sich bei der CORP2-Domäne mit dem Administratorkonto an, nach dem Neustart des Computers.  
  
## <a name="provide-group-policy-permissions-to-corpuser1"></a>Gewähren von Gruppenrichtlinien-Berechtigungen für "corp\user1"  
Geben Sie die "corp\user1" Benutzer mit vollen Berechtigungen zum Erstellen und Ändern von Gruppenrichtlinienobjekten corp2 mithilfe dieses Verfahrens.  
  
### <a name="to-provide-group-policy-permissions"></a>Berechtigungen für die Gruppenrichtlinie bereitstellen  
  
1.  Auf der **starten** geben**gpmc.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Gruppenrichtlinien-Verwaltungskonsole, **Gesamtstruktur: corp.contoso.com/Domains/corp2.corp.contoso.com**.  
  
3.  Klicken Sie im Detailbereich auf die **Delegierung** Registerkarte. In der **Berechtigung** Dropdown-Liste, klicken Sie auf **Verknüpfen von Gruppenrichtlinienobjekten**.  
  
4.  Klicken Sie auf **hinzufügen**, und klicken Sie auf dem neuen **Select User, Computer oder Gruppe** Dialogfeld klicken Sie auf **Speicherorte**.  
  
5.  Auf der **Speicherorte** Dialogfeld die **Speicherort** Struktur, klicken Sie auf **"corp.contoso.com"** , und klicken Sie auf **OK**.  
  
6.  In **Geben Sie den zu verwendenden Objektnamen** Typ **"user1"** , klicken Sie auf **OK**, und klicken Sie auf die **Benutzer oder Gruppe hinzufügen** Dialogfeld klicken Sie auf **OK** .  
  
7.  Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole, in der Struktur auf **Group Policy Objects**, und klicken Sie in die Details im Bereich auf die **Delegierung** Registerkarte.  
  
8.  Klicken Sie auf **hinzufügen**, und klicken Sie auf dem neuen **Select User, Computer oder Gruppe** Dialogfeld klicken Sie auf **Speicherorte**.  
  
9. Auf der **Speicherorte** Dialogfeld die **Speicherort** Struktur, klicken Sie auf **"corp.contoso.com"** , und klicken Sie auf **OK**.  
  
10. In **Geben Sie den zu verwendenden Objektnamen** Typ **"user1"** , klicken Sie auf **OK**.  
  
11. Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole, in der Struktur auf **WMI-Filter**, und klicken Sie in die Details im Bereich auf die **Delegierung** Registerkarte.  
  
12. Klicken Sie auf **hinzufügen**, und klicken Sie auf dem neuen **Select User, Computer oder Gruppe** Dialogfeld klicken Sie auf **Speicherorte**.  
  
13. Auf der **Speicherorte** Dialogfeld die **Speicherort** Struktur, klicken Sie auf **"corp.contoso.com"** , und klicken Sie auf **OK**.  
  
14. In **Geben Sie den zu verwendenden Objektnamen** Typ **"user1"** , klicken Sie auf **OK**. Auf der **Benutzer oder Gruppe hinzufügen** Dialogfeld Feld, stellen Sie sicher, dass **Berechtigungen** festgelegt **Vollzugriff**, und klicken Sie dann auf **OK**.  
  
15. Schließen Sie die Gruppenrichtlinien-Verwaltungskonsole.  
  
## <a name="allow-corp2-computers-to-obtain-computer-certificates"></a>Abrufen von Computerzertifikaten CORP2 auf Computern zulassen 

Computer in der Domäne CORP2 müssen Computerzertifikate von der Zertifizierungsstelle auf dem Computer APP1 beziehen. Verfahren Sie dieses auf dem Computer APP1 aus.  
  
### <a name="to-allow-corp2-computers-to-automatically-obtain-computer-certificates"></a>Gestattet CORP2 Computern um Computerzertifikate automatisch zu erhalten.  
  
1.  Klicken Sie auf dem App1-Computer auf **starten**, Typ **certtmpl.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  In der **Vorlage Zertifikatkonsole**, doppelklicken Sie im mittleren Bereich auf **Client-/ Serverauthentifizierung**.  
  
3.  Auf der **Eigenschaften von Client / Server-Authentifizierung** Dialogfeld klicken Sie auf die **Sicherheit** Registerkarte.  
  
4.  Klicken Sie auf **hinzufügen**, und klicken Sie auf die **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** Dialogfeld klicken Sie auf **Speicherorte**.  
  
5.  Auf der **Speicherorte** Dialogfeld **Speicherort**, erweitern Sie **"corp.contoso.com"** , klicken Sie auf **corp2.corp.contoso.com**, und klicken Sie dann auf  **OK**.  
  
6.  In **Geben Sie die zu verwendenden Objektnamen**, Typ **Domänen-Admins; Domänencomputer** , und klicken Sie dann auf **OK**.  
  
7.  Auf der **Eigenschaften von Client / Server-Authentifizierung** Dialogfeld **Gruppen-oder Benutzernamen**, klicken Sie auf **Domänen-Admins (Administratoren CORP2\Domain)** , und klicken Sie in  **Berechtigungen für die Domänen-Admins**in die **zulassen** Spalte **schreiben** und **registrieren**.  
  
8.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **Domänencomputer (CORP2\Domain Computer)** , und klicken Sie in **Berechtigungen für Domänencomputer**in die **zulassen**Spalte **registrieren** und **automatisch registrieren**, und klicken Sie dann auf **OK**.  
  
9. Schließen Sie die Zertifikatvorlagenkonsole.  
  
## <a name="replication"></a>Erzwingen der Replikation zwischen DC1 und 2-DC1  
Bevor Sie Zertifikate auf 2-EDGE1 registrieren können, müssen Sie die Replikation der Einstellungen von DC1 auf 2-DC1 erzwingen. Dieser Vorgang sollte auf DC1 ausgeführt werden.  
  
### <a name="to-force-replication"></a>Die Replikation erzwingen  
  
1.  Klicken Sie auf DC1 auf **starten**, und klicken Sie dann auf **Active Directory-Standorte und-Dienste**.  
  
2.  Erweitern Sie in der Konsole Active Directory-Standorte und-Dienste in der Struktur der **standortübergreifende Transporte**, und klicken Sie dann auf **IP**.  
  
3.  Doppelklicken Sie im Detailbereich auf **DEFAULTIPSITELINK**.  
  
4.  Auf der **DEFAULTIPSITELINK Eigenschaften** Dialogfeld **Kosten**, Typ **1**im **Replizieren alle**, Typ **15**, und klicken Sie dann auf **OK**. Warten Sie 15 Minuten, bis die Replikation beendet ist.  
  
5.  Um die Replikation jetzt in der Konsolenstruktur zu erzwingen, erweitern Sie **%%amp;quot;sites\standardwebsite\adfs%%amp;quot;)-First-Site-name\Servers\DC1\NTDS Einstellungen**, im Detailbereich mit der Maustaste **<automatically generated>** , klicken Sie auf  **Jetzt replizieren**, und klicken Sie dann auf die **Jetzt replizieren** Dialogfeld klicken Sie auf **OK**.  
  
6.  Um sicherzustellen, dass Replikation erfolgreich abgeschlossen wurde gehen Sie folgendermaßen vor:  
  
    1.  Auf der **starten** geben**cmd.exe**, und drücken Sie dann die EINGABETASTE.  
  
    2.  Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
  
        ```  
        repadmin /syncall /e /A /P /d /q  
        ```  
  
    3.  Stellen Sie sicher, dass alle Partitionen ohne Fehler synchronisiert werden. Wenn dies nicht der Fall ist, klicken Sie dann den Befehl erneut ausführen, bis keine Fehler, bevor Sie fortfahren gemeldet werden.  
  
7.  Schließen Sie das Eingabeaufforderungsfenster.  
  


