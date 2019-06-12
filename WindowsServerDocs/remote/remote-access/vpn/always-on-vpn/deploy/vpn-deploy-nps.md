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
ms.openlocfilehash: ca52aeeed8c4872e4d9a433c55bddc65a74d9dc0
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749620"
---
# <a name="step-4-install-and-configure-the-network-policy-server-nps"></a>Schritt 4 Installieren Sie und konfigurieren Sie (Network Policy Server, NPS)

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, Windows 10

- [**nächster:** Schritt 3 Konfigurieren des RAS-Servers für Always On VPN](vpn-deploy-ras.md)
- [**nächster:** Schritt 5 Konfigurieren von DNS und Firewalleinstellungen](vpn-deploy-dns-firewall.md)

In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) für die Verarbeitung von Anforderungen von Verbindungen, die von der VPN-Server gesendet werden:

- Führen Sie die Autorisierung, um sicherzustellen, dass der Benutzer die Berechtigung zur verbindungsherstellung verfügt.
- Ausführen der Authentifizierung, um die Identität des Benutzers zu überprüfen.
- Ausführen von Buchhaltung, um die Aspekte der Anforderung der Verbindung melden Sie sich, dass Sie ausgewählt haben, wenn Sie die RADIUS-Kontoführung auf dem Netzwerkrichtlinienserver konfiguriert.

Die Schritte in diesem Abschnitt ermöglichen Sie Folgendes ausführen:

1. Auf dem Computer oder virtuellen Computer, der für den NPS-Server geplant und auf Ihre Organisation oder Ihr Unternehmensnetzwerk installiert wird, können Sie NPS installieren.

   >[!TIP]
   >Wenn Sie bereits über einen oder mehrere NPS-Server in Ihrem Netzwerk verfügen, Sie müssen sich nicht um NPS-Server-Installation durchzuführen – stattdessen können Sie in diesem Thema verwenden, beim Aktualisieren der Konfiguration eines vorhandenen NPS-Servers.

> [!NOTE]
> Sie können die NPS-Dienst nicht unter Windows Server Core installieren.

2. Auf der Organisation/Unternehmenskonten NPS-Server können Sie NPS als RADIUS-Server ausführen, die von der VPN-Server empfangen verbindungsanforderungen verarbeitet konfigurieren.

## <a name="install-network-policy-server"></a>Installieren des Netzwerkrichtlinienservers

In diesem Verfahren installieren Sie NPS mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten aus. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

>[!TIP]
>Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Bei der Installation von NPS, und die Windows-Firewall mit erweiterter Sicherheit aktivieren, für IPv4 und IPv6-Verkehr automatisch Firewallausnahmen für diese Ports erstellt. Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere diese Standardwerte Ports konfiguriert sind, entfernen Sie die Ausnahmen, die in der Windows-Firewall mit erweiterter Sicherheit während der NPS-Installation erstellt, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Verkehr.

**Verfahren für Windows PowerShell:**

Führen Sie dieses Verfahren mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, geben das folgende Cmdlet aus:

```powershell
Install-WindowsFeature NPAS -IncludeManagementTools
```

**Verfahren für Server-Manager:**

1.  Wählen Sie im Server-Manager **verwalten**, und wählen Sie dann **Hinzufügen von Rollen und Features**.
        Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Bevor Sie beginnen, wählen Sie **Weiter**.

    >[!NOTE] 
    >Die **Vorbemerkungen** des Hinzufügen von Rollen und Features-Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **auf dieser Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistenten ausgeführt haben.

3.  Installationstyp auswählen, stellen sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und wählen **Weiter**.

4.  Zielserver auswählen, stellen sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist.

5.  Server befinden, stellen Sie sicher, dass der lokale Computer auswählen und Option ist **Weiter**.

6.  Wählen Sie in Server-Rollen in **Rollen**Option **Netzwerkrichtlinien- und Zugriffsdienste**. Ein Dialogfeld wird geöffnet, gefragt, ob es für Netzwerkrichtlinien- und Zugriffsdienste erforderlichen Features hinzufügen sollten.

7.  Wählen Sie **Features hinzufügen**, und wählen Sie dann **weiter**

8.  Wählen Sie in Funktionen auswählen **Weiter**, in die Netzwerkrichtlinien- und Zugriffsdienste, lesen Sie die Informationen, und wählen Sie **Weiter**.

9.  Wählen Sie in der Option Rollendienste **Netzwerkrichtlinienserver**.

10. Wählen Sie für den Network Policy Server erforderlichen Features, **Features hinzufügen**, und wählen Sie dann **Weiter**.

11. Wählen Sie in der Installationsauswahl, **automatisch neu starten die Zielserver bei Bedarf**.

12. Wählen Sie **Ja** ausgewählten zu bestätigen, und wählen Sie dann **installieren**.
    
    Seite für den Installationsfortschritt zeigt den Status während des Installationsvorgangs an. Wenn der Prozess abgeschlossen ist, die Meldung "Installation erfolgreich auf *ComputerName*" angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem Netzwerkrichtlinienserver installiert.

13. Wählen Sie **Schließen**.

## <a name="configure-nps"></a>Konfigurieren von NPS

Nach der Installation von NPS, konfigurieren Sie NPS, um alle Authentifizierung, Autorisierung, verarbeiten und Kontoführung Aufgaben für die Verbindung Herausgabe der Kundendaten erhält von der VPN-Server.

### <a name="register-the-nps-server-in-active-directory"></a>Registrieren Sie den NPS-Server in Active Directory.

In diesem Verfahren registrieren Sie den Server in Active Directory, damit sie die Berechtigung zum Zugriff auf Kontoinformationen für Benutzer während der Verarbeitung von Anforderungen von Verbindungen aufweist.

**Vorgehensweise:**

1.  Wählen Sie im Server-Manager **Tools**, und wählen Sie dann **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2.  In der NPS-Konsole mit der Maustaste **NPS (lokal)** , und wählen Sie dann **Server in Active Directory registrieren**.
   
     Der Netzwerkrichtlinienserver-Dialogfeld wird geöffnet.

3.  Wählen Sie in das Dialogfeld des Netzwerkrichtlinienservers **OK** zweimal.

Alternative Methoden zur Registrierung von NPS, finden Sie unter [registrieren Sie einen NPS-Server in einer Active Directory-Domäne](../../../../../networking/technologies/nps/nps-manage-register.md).

### <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

Konfigurieren Sie in diesem Verfahren Netzwerk-Richtlinie Server Kontoführung mithilfe einer der folgenden Typen für die Protokollierung aus:

- **Protokollierung von Komponentenereignissen**. Verwendet in erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen. Sie können NPS-ereignisprotokollierung durch Abrufen der Eigenschaften des NPS-Server in der NPS-Konsole konfigurieren.

- **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in einer lokalen Datei**. In erster Linie für verbindungszwecke für Analyse und die Abrechnung verwendet. Auch verwendet als ein Sicherheitstool für die Untersuchung, da er eine Methode zum Nachverfolgen der Aktivität von einem böswilligen Benutzer nach einem Angriff enthält. Sie können lokale dateiprotokollierung mithilfe des Assistenten Ressourcenerfassung konfigurieren.

- **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in eine Microsoft SQL Server-XML-kompatiblen Datenbank**. Wird verwendet, um mehrere Server mit NPS, damit eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server-Protokollierung konfigurieren, mit der Buchhaltung Konfigurations-Assistent.

Um Network Policy Server Ressourcenerfassung zu konfigurieren, finden Sie unter [konfigurieren Network Policy Server Accounting](../../../../../networking/technologies/nps/nps-accounting-configure.md).

### <a name="add-the-vpn-server-as-a-radius-client"></a>Fügen Sie dem VPN-Server als RADIUS-Client hinzu.

In der [Konfigurieren der RAS-Server für Always On-VPN-](vpn-deploy-ras.md) Abschnitt Sie installiert und den VPN-Server konfiguriert. Während der Konfiguration des VPN-Server haben Sie einen RADIUS-gemeinsamen geheimen Schlüssel auf dem VPN-Server hinzugefügt.

In diesem Verfahren verwenden Sie die gleiche freigegebene geheime Textzeichenfolge so konfigurieren Sie den VPN-Server als RADIUS-Client auf dem Netzwerkrichtlinienserver. Verwenden Sie die gleiche Textzeichenfolge, die Sie auf dem VPN-Server verwendet haben, oder die Kommunikation zwischen dem NPS-Server und VPN-Server ein Fehler auftritt.

>[!IMPORTANT] 
>Wenn Sie einem neuen Netzwerkzugriffsserver (VPN-Server, drahtlosen Zugriffspunkt, authentifizierenden Switch oder DFÜ-Server) mit dem Netzwerk hinzufügen, müssen Sie den Server als RADIUS-Client auf dem Netzwerkrichtlinienserver hinzufügen, sodass NPS bekannt ist, und klicken Sie mit Network Access Server kommunizieren kann.

**Vorgehensweise:**

1. Doppelklicken Sie auf dem NPS-Server in der NPS-Konsole auf **RADIUS-Clients und Servern**.

2. Mit der rechten Maustaste **RADIUS-Clients** , und wählen Sie **neu**. Das Dialogfeld Neuer RADIUS-Client wird geöffnet.

3. Überprüfen Sie, ob die **aktivieren Sie dieses RADIUS-Clients** das Kontrollkästchen aktiviert ist.

4. In **Anzeigenamen**, geben Sie einen Anzeigenamen für die VPN-Server.

5. In **Adresse (IP oder DNS)** , geben Sie den NAS IP-Adresse oder FQDN.
     
     Wenn Sie den FQDN eingegeben haben, wählen Sie **überprüfen** sollten Sie überprüfen, ob der Name richtig ist und eine gültige IP-Adresse zugeordnet.

6. In **gemeinsamer geheimer Schlüssel**, sind:

    1. Sicherstellen, dass **manuelle** ausgewählt ist.

    2. Geben Sie die fett formatierter Text-Zeichenfolge, die Sie auch auf dem VPN-Server eingegeben haben.

    3. Geben Sie den gemeinsamen geheimen Schlüssel in den gemeinsamen geheimen Schlüssel bestätigen.

7. Wählen Sie **OK**. Der VPN-Server wird angezeigt, in der Liste der RADIUS-Clients, die auf dem NPS-Server konfiguriert.

## <a name="configure-nps-as-a-radius-for-vpn-connections"></a>Konfigurieren von NPS als einen RADIUS für VPN-Verbindungen

In diesem Verfahren konfigurieren Sie NPS als RADIUS-Server im Netzwerk Ihrer Organisation. Für den NPS verwenden, müssen Sie eine Richtlinie, die nur Benutzer in der Organisation/Unternehmensnetzwerk über VPN-Server - Zugriff auf eine bestimmte Gruppe ermöglicht definieren und dann nur, wenn ein gültiger Benutzer-Zertifikat in einer Anforderung der PEAP-Authentifizierung verwenden.

**Vorgehensweise:**

1. Stellen Sie sicher, die in der Konsole "NPS" unter Standardkonfiguration **RADIUS-Server für DFÜ- oder VPN-Verbindungen** ausgewählt ist.

2. Wählen Sie **konfigurieren VPN- oder DFÜ-** .
        
    Das Konfigurieren von VPN- oder DFÜ-Assistent wird geöffnet.

3. Wählen Sie **virtuelles privates Netzwerk (VPN) Verbindungen**, und wählen Sie **Weiter**.

4. Wählen Sie im geben DFÜ- oder VPN-Server in der RADIUS-Clients den Namen des VPN-Server, die Sie im vorherigen Schritt hinzugefügt. Wählen Sie beispielsweise, wenn Ihre VPN-Server-NetBIOS-Namen RAS1 ist, **RAS1**.

5. Wählen Sie **Weiter** aus.

6. Führen Sie in den Authentifizierungsmethoden zu konfigurieren die folgenden Schritte aus:

    1. Deaktivieren der **Microsoft-verschlüsselte Authentifizierung, Version 2 (MS-CHAPv2)** Kontrollkästchen.

    2. Wählen Sie die **Extensible Authentication Protocol** Kontrollkästchen, um es auszuwählen.

    3. Wählen Sie unter Typ (basierend auf die Methode von Zugriff und Netzwerkkonfiguration) **Microsoft: Geschütztes EAP (PEAP)** , und wählen Sie dann **konfigurieren**.
      
        Das Dialogfeld Eigenschaften für geschütztes EAP bearbeiten wird geöffnet.

    4. Wählen Sie **entfernen** sicheres Kennwort (EAP-MSCHAP v2) EAP-Typ entfernen.

    5. Wählen Sie **hinzufügen**. Das Dialogfeld "EAP hinzufügen" wird geöffnet.

    6. Wählen Sie **Smartcard- oder anderes Zertifikat**, und wählen Sie dann **OK**.

    7. Wählen Sie **OK** um Eigenschaften für geschütztes EAP bearbeiten zu schließen.

7. Wählen Sie **Weiter** aus.

8. Führen Sie in den Benutzergruppen angeben die folgenden Schritte aus:

    1. Wählen Sie **hinzufügen**. Das Dialogfeld zur Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen wird geöffnet.

    2. Geben Sie **VPN-Benutzer**, und wählen Sie dann **OK**.

    3. Wählen Sie **Weiter** aus.

9. Wählen Sie in der IP-Filter angeben, **Weiter**.

10. Wählen Sie in das Angeben von Verschlüsselungseinstellungen **Weiter**. Nehmen Sie keine Änderungen.

    Diese Einstellungen gelten nur für Microsoft Point-Encryption (MPPE)-Verbindungen, die in diesem Szenario nicht unterstützt.

11. Wählen Sie in der Bereichsname angeben, **Weiter**.

12. Wählen Sie **Fertig stellen** um den Assistenten zu schließen.

## <a name="autoenroll-the-nps-server-certificate"></a>Zertifikat nicht der NPS-Server registrieren

In diesem Verfahren aktualisieren Sie Gruppenrichtlinien auf dem lokalen NPS-Server manuell. Wenn automatisch registrierten gruppenrichtlinienaktualisierungen, wenn der automatischen Registrierung von Zertifikaten konfiguriert und ordnungsgemäß funktioniert, der lokale Computer ist ein Zertifikat von der Zertifizierungsstelle (CA).

>[!NOTE]  
>Die Gruppenrichtlinie wird automatisch aktualisiert, wenn Sie den Domänenmitgliedscomputer neu starten, oder wenn ein Benutzer auf einem Domänenmitgliedscomputer anmeldet. Darüber hinaus wird der Gruppenrichtlinie in regelmäßigen Abständen aktualisiert. Diese regelmäßige Aktualisierung geschieht standardmäßig alle 90 Minuten mit einem zufälligen Versatz von bis zu 30 Minuten.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

**Vorgehensweise:**

1. Öffnen Sie auf den NPS Windows PowerShell ein.

2. Geben Sie an der Windows PowerShell-Eingabeaufforderung **Gpupdate**, und drücken Sie dann die EINGABETASTE.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 5: Konfigurieren von DNS und Firewall-Einstellungen für Always On-VPN-](vpn-deploy-dns-firewall.md): In diesem Schritt installieren Sie Windows-Verwaltungsinstrumentation (Network Policy Server, NPS) mit Windows PowerShell oder die Rollen von Server-Manager hinzufügen und Features-Assistenten. Sie auch konfigurieren, NPS, um alle Authentifizierung, Autorisierung und Kontoführung von Aufgaben für die Verbindung verarbeitet Anforderungen, die von der VPN-Server empfangen.