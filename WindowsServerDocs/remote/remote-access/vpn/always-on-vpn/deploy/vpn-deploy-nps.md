---
title: Installieren und Konfigurieren von NPS-Servers
description: Verarbeitung der NPS-Server der verbindungsanforderungen, die von der VPN-Server gesendet werden überprüft, ob der Benutzer verfügt über die Berechtigung, die Identität des Benutzers, eine Verbindung herstellen und protokolliert die Aspekte der Anforderung der Verbindung, die Sie ausgewählt haben, wenn Sie die RADIUS-Kontoführung auf dem Netzwerkrichtlinienserver konfiguriert.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: ca53ef28497a78f264c60ac1132f721fb6e01c15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890311"
---
# <a name="step-4-install-and-configure-the-network-policy-server-nps"></a>Schritt 4 Installieren Sie und konfigurieren Sie (Network Policy Server, NPS)

>   Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, Windows 10


&#171;  [**nächster:** Schritt 3 Konfigurieren der RAS-Server für Always On-VPN](vpn-deploy-ras.md)<br>
&#187;  [**Next:** Schritt 5 Konfigurieren von DNS und Firewall-Einstellungen](vpn-deploy-dns-firewall.md)


In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) für die Verarbeitung von Anforderungen von Verbindungen, die von der VPN-Server gesendet werden:

- Führen Sie die Autorisierung, um sicherzustellen, dass der Benutzer die Berechtigung zur verbindungsherstellung verfügt.
- Ausführen der Authentifizierung, um die Identität des Benutzers zu überprüfen.
- Ausführen von Buchhaltung, um die Aspekte der Anforderung der Verbindung melden Sie sich, dass Sie ausgewählt haben, wenn Sie die RADIUS-Kontoführung auf dem Netzwerkrichtlinienserver konfiguriert.

Die Schritte in diesem Abschnitt ermöglichen Sie Folgendes ausführen:

1.  Auf dem Computer oder virtuellen Computer, der für den NPS-Server geplant und auf Ihre Organisation oder Ihr Unternehmensnetzwerk installiert wird, können Sie NPS installieren.

   >[!TIP] 
   >Wenn Sie bereits über einen oder mehrere NPS-Server in Ihrem Netzwerk verfügen, Sie müssen sich nicht um NPS-Server-Installation durchzuführen – stattdessen können Sie in diesem Thema verwenden, beim Aktualisieren der Konfiguration eines vorhandenen NPS-Servers.

>[!NOTE]  
Sie können die NPS-Dienst nicht unter Windows Server Core installieren.

2.  Auf der Organisation/Unternehmenskonten NPS-Server können Sie NPS als RADIUS-Server ausführen, die von der VPN-Server empfangen verbindungsanforderungen verarbeitet konfigurieren.

## <a name="install-network-policy-server"></a>Installieren des Netzwerkrichtlinienservers

In diesem Verfahren installieren Sie NPS mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten aus. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

>[!TIP] 
>Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Bei der Installation von NPS, und die Windows-Firewall mit erweiterter Sicherheit aktivieren, für IPv4 und IPv6-Verkehr automatisch Firewallausnahmen für diese Ports erstellt. Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere diese Standardwerte Ports konfiguriert sind, entfernen Sie die Ausnahmen, die in der Windows-Firewall mit erweiterter Sicherheit während der NPS-Installation erstellt, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Verkehr.

**Verfahren für Windows PowerShell:**

Geben Sie den folgenden Befehl zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature NPAS -IncludeManagementTools`

**Verfahren für Server-Manager:**

1.  Klicken Sie im Server-Manager **verwalten**, und klicken Sie auf **Hinzufügen von Rollen und Features**. <p>Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Bevor Sie beginnen, klicken Sie auf **Weiter**.

    >[!NOTE] 
    >Die **Vorbemerkungen** des Hinzufügen von Rollen und Features-Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **auf dieser Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistenten ausgeführt haben.

1.  Installationstyp auswählen, stellen sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie auf **Weiter**.

2.  Zielserver auswählen, stellen sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist.

3.  Server befinden, stellen Sie sicher, dass der lokale Computer ausgewählt ist, und klicken Sie auf **Weiter**.

4.  Wählen Sie in Server-Rollen in **Rollen**Option **Netzwerkrichtlinien- und Zugriffsdienste**. Ein Dialogfeld wird geöffnet, gefragt, ob es für Netzwerkrichtlinien- und Zugriffsdienste erforderlichen Features hinzufügen sollten.

5.  Klicken Sie auf **Features hinzufügen**, und klicken Sie auf **weiter**

6.  Features auswählen, klicken Sie auf **Weiter**, und klicken Sie in die Netzwerkrichtlinien- und Zugriffsdienste, lesen Sie die Informationen, und klicken Sie auf **Weiter**.

7.  Dienste für Rolle auswählen, klicken Sie auf **Netzwerkrichtlinienserver**.

8.  Für Funktionen, die für den Network Policy Server erforderlich sind, klicken Sie auf **Features hinzufügen** und klicken Sie auf **Weiter**.

9.  Installationsauswahl bestätigen, klicken Sie auf **automatisch neu starten die Zielserver bei Bedarf**.

10. Klicken Sie auf **Ja** , bestätigen Sie den ausgewählten, und klicken Sie dann auf **installieren**. <p>Seite für den Installationsfortschritt zeigt den Status während des Installationsvorgangs an. Wenn der Prozess abgeschlossen ist, die Meldung "Installation erfolgreich auf *ComputerName*" angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem Netzwerkrichtlinienserver installiert.

11. Klicken Sie auf **Schließen**.

## <a name="configure-nps"></a>Konfigurieren von NPS

Nach der Installation von NPS, konfigurieren Sie NPS, um alle Authentifizierung, Autorisierung, verarbeiten und Kontoführung Aufgaben für die Verbindung Herausgabe der Kundendaten erhält von der VPN-Server.

### <a name="register-the-nps-server-in-active-directory"></a>Registrieren Sie den NPS-Server in Active Directory.

In diesem Verfahren registrieren Sie den Server in Active Directory, damit sie die Berechtigung zum Zugriff auf Kontoinformationen für Benutzer während der Verarbeitung von Anforderungen von Verbindungen aufweist.

**Vorgehensweise:**

1.  Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2.  In der NPS-Konsole mit der Maustaste **NPS (lokal)**, und klicken Sie auf **Server in Active Directory registrieren** um es auszuwählen.<p>Der Netzwerkrichtlinienserver-Dialogfeld wird geöffnet.

3.  Klicken Sie in das Dialogfeld Network Policy Server, auf **OK** zweimal.

Alternative Methoden zur Registrierung von NPS, finden Sie unter [registrieren Sie einen NPS-Server in einer Active Directory-Domäne](../../../../../networking/technologies/nps/nps-manage-register.md).

### <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

Konfigurieren Sie in diesem Verfahren Netzwerk-Richtlinie Server Kontoführung mithilfe einer der folgenden Typen für die Protokollierung aus:

-   **Protokollierung von Komponentenereignissen**. Verwendet in erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen. Sie können NPS-ereignisprotokollierung durch Abrufen der Eigenschaften des NPS-Server in der NPS-Konsole konfigurieren.

-   **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in einer lokalen Datei**. In erster Linie für verbindungszwecke für Analyse und die Abrechnung verwendet. Auch verwendet als ein Sicherheitstool für die Untersuchung, da er eine Methode zum Nachverfolgen der Aktivität von einem böswilligen Benutzer nach einem Angriff enthält. Sie können lokale dateiprotokollierung mithilfe des Assistenten Ressourcenerfassung konfigurieren.

-   **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in eine Microsoft SQL Server-XML-kompatiblen Datenbank**. Wird verwendet, um mehrere Server mit NPS, damit eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server-Protokollierung konfigurieren, mit der Buchhaltung Konfigurations-Assistent.

Um Network Policy Server Ressourcenerfassung zu konfigurieren, finden Sie unter [konfigurieren Network Policy Server Accounting](../../../../../networking/technologies/nps/nps-accounting-configure.md).

### <a name="add-the-vpn-server-as-a-radius-client"></a>Fügen Sie dem VPN-Server als RADIUS-Client hinzu.

In der [Konfigurieren der RAS-Server für Always On-VPN-](vpn-deploy-ras.md) Abschnitt Sie installiert und den VPN-Server konfiguriert. Während der Konfiguration des VPN-Server haben Sie einen RADIUS-gemeinsamen geheimen Schlüssel auf dem VPN-Server hinzugefügt. 

In diesem Verfahren verwenden Sie die gleiche freigegebene geheime Textzeichenfolge so konfigurieren Sie den VPN-Server als RADIUS-Client auf dem Netzwerkrichtlinienserver. Verwenden Sie die gleiche Textzeichenfolge, die Sie auf dem VPN-Server verwendet haben, oder die Kommunikation zwischen dem NPS-Server und VPN-Server ein Fehler auftritt.

>[!IMPORTANT] 
>Wenn Sie einem neuen Netzwerkzugriffsserver (VPN-Server, drahtlosen Zugriffspunkt, authentifizierenden Switch oder DFÜ-Server) mit dem Netzwerk hinzufügen, müssen Sie den Server als RADIUS-Client auf dem Netzwerkrichtlinienserver hinzufügen, sodass NPS bekannt ist, und klicken Sie mit Network Access Server kommunizieren kann.

**Vorgehensweise:**

1.  Doppelklicken Sie auf dem NPS-Server in der NPS-Konsole auf **RADIUS-Clients und Servern**.

2.  Mit der rechten Maustaste **RADIUS-Clients** , und klicken Sie auf **neu**. Das Dialogfeld Neuer RADIUS-Client wird geöffnet.

3.  Überprüfen Sie, ob die **aktivieren Sie dieses RADIUS-Clients** das Kontrollkästchen aktiviert ist.

4.  In **Anzeigenamen**, geben Sie einen Anzeigenamen für die VPN-Server.

5.  In **Adresse (IP oder DNS)**, geben Sie den NAS IP-Adresse oder FQDN.<p>Wenn Sie den FQDN eingegeben haben, klicken Sie auf **überprüfen** sollten Sie überprüfen, ob der Name richtig ist und eine gültige IP-Adresse zugeordnet.

6.  In **gemeinsamer geheimer Schlüssel**, sind:

    1.  Sicherstellen, dass **manuelle** ausgewählt ist.

    2.  Geben Sie die fett formatierter Text-Zeichenfolge, die Sie auch auf dem VPN-Server eingegeben haben.

    3.  Geben Sie den gemeinsamen geheimen Schlüssel in den gemeinsamen geheimen Schlüssel bestätigen ein.

7.  Klicken Sie auf **OK**. Der VPN-Server wird angezeigt, in der Liste der RADIUS-Clients, die auf dem NPS-Server konfiguriert.

## <a name="configure-nps-as-a-radius-for-vpn-connections"></a>Konfigurieren von NPS als einen RADIUS für VPN-Verbindungen

In diesem Verfahren konfigurieren Sie NPS als RADIUS-Server im Netzwerk Ihrer Organisation. Für den NPS verwenden, müssen Sie eine Richtlinie, die nur Benutzer in der Organisation/Unternehmensnetzwerk über VPN-Server - Zugriff auf eine bestimmte Gruppe ermöglicht definieren und dann nur, wenn ein gültiger Benutzer-Zertifikat in einer Anforderung der PEAP-Authentifizierung verwenden.

**Vorgehensweise:**

1.  Stellen Sie sicher, die in der Konsole "NPS" unter Standardkonfiguration **RADIUS-Server für DFÜ- oder VPN-Verbindungen** ausgewählt ist.

2.  Klicken Sie auf **konfigurieren VPN- oder DFÜ-**.<p>Das Konfigurieren von VPN- oder DFÜ-Assistent wird geöffnet.

3.  Klicken Sie auf **virtuelles privates Netzwerk (VPN) Verbindungen**, und klicken Sie auf **Weiter**.

4.  Wählen Sie im geben DFÜ- oder VPN-Server in der RADIUS-Clients den Namen des VPN-Server, die Sie im vorherigen Schritt hinzugefügt.<p>Beispielsweise wenn Ihre VPN-Server-NetBIOS-Namen RAS1 ist, klicken Sie auf **RAS1**.

5.  Klicken Sie auf **Weiter**.

6.  Führen Sie in den Authentifizierungsmethoden zu konfigurieren die folgenden Schritte aus:

    1.  Deaktivieren der **Microsoft-verschlüsselte Authentifizierung, Version 2 (MS-CHAPv2)** Kontrollkästchen.

    2.  Klicken Sie auf die **Extensible Authentication Protocol** Kontrollkästchen, um es auszuwählen.

    3.  Typ (basierend auf die Methode von Zugriff und Netzwerkkonfiguration), klicken Sie auf **Microsoft: Geschütztes EAP (PEAP)**, und klicken Sie auf **konfigurieren**.<p>Das Dialogfeld Eigenschaften für geschütztes EAP bearbeiten wird geöffnet.

    4.  Klicken Sie auf **entfernen** sicheres Kennwort (EAP-MSCHAP v2) EAP-Typ entfernen.

    5.  Klicken Sie auf **Hinzufügen**. Das Dialogfeld "EAP hinzufügen" wird geöffnet.

    6.  Klicken Sie auf **Smartcard- oder anderes Zertifikat**, und klicken Sie auf **OK**.

    7.  Klicken Sie auf **OK** um Eigenschaften für geschütztes EAP bearbeiten zu schließen.

7.  Klicken Sie auf **Weiter**.

8.  Führen Sie in den Benutzergruppen angeben die folgenden Schritte aus:

    1.  Klicken Sie auf **Hinzufügen**. Das Dialogfeld zur Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen wird geöffnet.

    2.  Typ **VPN-Benutzer** , und klicken Sie auf **OK**.

    3.  Klicken Sie auf **Weiter**.

9.  Geben Sie IP-Filter, klicken Sie auf **Weiter**.

10. Angeben von Verschlüsselungseinstellungen, klicken Sie auf **Weiter**. Nehmen Sie keine Änderungen.<p>Diese Einstellungen gelten nur für Microsoft Point-Encryption (MPPE)-Verbindungen, die in diesem Szenario nicht unterstützt.

11. Geben Sie einen Bereich an, klicken Sie auf **Weiter**.

12. Klicken Sie auf **Fertig stellen**, und beenden Sie den Assistenten.

## <a name="autoenroll-the-nps-server-certificate"></a>Zertifikat nicht der NPS-Server registrieren

In diesem Verfahren aktualisieren Sie Gruppenrichtlinien auf dem lokalen NPS-Server manuell. Wenn automatisch registrierten gruppenrichtlinienaktualisierungen, wenn der automatischen Registrierung von Zertifikaten konfiguriert und ordnungsgemäß funktioniert, der lokale Computer ist ein Zertifikat von der Zertifizierungsstelle (CA).

>[!NOTE]  
>Die Gruppenrichtlinie wird automatisch aktualisiert, wenn Sie den Domänenmitgliedscomputer neu starten, oder wenn ein Benutzer auf einem Domänenmitgliedscomputer anmeldet. Darüber hinaus wird der Gruppenrichtlinie in regelmäßigen Abständen aktualisiert. Diese regelmäßige Aktualisierung geschieht standardmäßig alle 90 Minuten mit einem zufälligen Versatz von bis zu 30 Minuten.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

**Vorgehensweise:**

1.  Öffnen Sie auf den NPS Windows PowerShell ein.

2.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Gpupdate**, und drücken Sie dann die EINGABETASTE.

## <a name="next-step"></a>Nächster Schritt
[Schritt 5. Konfigurieren von DNS und Firewall-Einstellungen für Always On-VPN-](vpn-deploy-dns-firewall.md): In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten. Sie auch konfigurieren, NPS, um alle Authentifizierung, Autorisierung und Kontoführung von Aufgaben für die Verbindung verarbeitet Anforderungen, die von der VPN-Server empfangen.



---

