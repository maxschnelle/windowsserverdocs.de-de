---
title: Installieren und Konfigurieren von NPS-Servers
description: Die NPS-Server Verarbeitung von Verbindungsanforderungen, die vom VPN-Server gesendet werden, überprüft, ob der Benutzer über die Berechtigung zum Herstellen einer Verbindung und die Identität des Benutzers verfügt, und protokolliert die Aspekte der Verbindungsanforderung, die Sie beim Konfigurieren der RADIUS-Kontoführung in NPS ausgewählt haben.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 08/30/2018
ms.openlocfilehash: d286f44e198aa13204b884da3fdf729f18b7553b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860453"
---
# <a name="step-4-install-and-configure-the-network-policy-server-nps"></a>Schritt 4 Installieren und Konfigurieren des Netzwerk Richtlinien Servers (NPS)

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Weiter:** Schritt 3. Konfigurieren des Remote Zugriffs Servers für die Always on-VPN](vpn-deploy-ras.md)
- [**Weiter:** Schritt 5: Konfigurieren von DNS-und Firewalleinstellungen](vpn-deploy-dns-firewall.md)

In diesem Schritt installieren Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) für die Verarbeitung von Verbindungsanforderungen, die vom VPN-Server gesendet werden:

- Führen Sie eine Autorisierung aus, um zu überprüfen, ob der Benutzer über die Berechtigung
- Authentifizierung wird durchgeführt, um die Identität des Benutzers zu überprüfen.
- Durchführen der Buchhaltung zum Protokollieren der Aspekte der Verbindungsanforderung, die Sie beim Konfigurieren der RADIUS-Kontoführung in NPS ausgewählt haben.

Mit den Schritten in diesem Abschnitt können Sie die folgenden Elemente ausführen:

1. Auf dem Computer oder virtuellen Computer, der für den NPS-Server geplant und in Ihrer Organisation oder im Unternehmensnetzwerk installiert ist, können Sie NPS installieren.

   >[!TIP]
   >Wenn Sie bereits über einen oder mehrere NPS-Server in Ihrem Netzwerk verfügen, müssen Sie die NPS-Server Installation nicht ausführen. stattdessen können Sie dieses Thema verwenden, um die Konfiguration eines vorhandenen NPS-Servers zu aktualisieren.

> [!NOTE]
> Der Netzwerk Richtlinien Server-Dienst kann nicht unter Windows Server Core installiert werden.

2. Auf dem NPS-Server "Organization/Corporate" können Sie NPS so konfigurieren, dass er als RADIUS-Server verwendet wird, der die vom VPN-Server empfangenen Verbindungsanforderungen verarbeitet.

## <a name="install-network-policy-server"></a>Installieren des Netzwerkrichtlinienservers

In diesem Verfahren installieren Sie NPS mithilfe von Windows PowerShell oder dem Server-Manager Assistenten zum Hinzufügen von Rollen und Features. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

>[!TIP]
>Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn Sie NPS installieren und die Windows-Firewall mit erweiterter Sicherheit aktivieren, werden Firewallausnahmen für diese Ports automatisch sowohl für IPv4-als auch für IPv6-Datenverkehr erstellt. Wenn Ihre Netzwerk Zugriffs Server für das Senden von RADIUS-Datenverkehr über andere Ports als diese Standardeinstellungen konfiguriert sind, entfernen Sie die Ausnahmen, die bei der NPS-Installation unter Windows-Firewall mit erweiterter Sicherheit erstellt wurden, und erstellen Sie Ausnahmen für die Ports, die Sie für RADIUS-Datenverkehr.

**Vorgehensweise für Windows PowerShell:**

Wenn Sie dieses Verfahren mithilfe von Windows PowerShell ausführen möchten, führen Sie Windows PowerShell als Administrator aus, und geben Sie das folgende Cmdlet ein:

```powershell
Install-WindowsFeature NPAS -IncludeManagementTools
```

**Prozedur für Server-Manager:**

1.  Klicken Sie in Server-Manager auf **Verwalten**, und wählen Sie dann **Rollen und Features hinzufügen**aus.
        Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Wählen Sie unter Vorbereitung die Option **weiter**aus.

    >[!NOTE] 
    >Die Seite **Vorbemerkungen** des Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie zuvor die Option Diese Seite beim Ausführen des Assistenten zum Hinzufügen von Rollen und Features **standardmäßig überspringen** ausgewählt haben.

3.  Vergewissern Sie sich, dass unter Installationstyp auswählen die Option **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie auf **weiter**.

4.  Stellen Sie sicher, dass unter Zielserver auswählen die Option **einen Server aus dem Server Pool auswählen** ausgewählt ist.

5.  Stellen Sie sicher, dass unter Server Pool die Option Lokaler Computer ausgewählt ist, und klicken Sie auf **weiter**.

6.  Wählen Sie unter Server Rollen auswählen unter **Rollen**die Option **Netzwerk Richtlinien-und Zugriffs Dienste**aus. Es wird ein Dialogfeld mit der Frage angezeigt, ob für Netzwerk Richtlinien-und Zugriffs Dienste erforderliche Features hinzugefügt werden sollen.

7.  Wählen Sie **Features hinzufügen**und dann **weiter** aus.

8.  Wählen Sie unter Features auswählen die Option **weiter**aus, und überprüfen Sie unter Netzwerk Richtlinien-und Zugriffs Dienste die angegebenen Informationen, und klicken Sie dann auf **weiter**.

9.  Wählen Sie unter Rollen Dienste auswählen die Option **Netzwerk Richtlinien Server**aus.

10. Klicken Sie für die für den Netzwerk Richtlinien Server erforderlichen Features auf **Features hinzufügen**, und wählen Sie **weiter**aus.

11. Wählen Sie unter Installations Auswahl bestätigen **die Option Zielserver bei Bedarf automatisch neu starten**aus.

12. Wählen Sie **Ja** aus, um die Auswahl zu bestätigen, und wählen Sie dann **Installieren**aus.
    
    Auf der Seite Installationsfortschritt wird der Status während des Installationsvorgangs angezeigt. Wenn der Vorgang abgeschlossen ist, wird die Meldung "Installation erfolgreich auf *Computername*" angezeigt, wobei *Computername* der Name des Computers ist, auf dem Sie den Netzwerk Richtlinien Server installiert haben.

13. Wählen Sie **Schließen** aus.

## <a name="configure-nps"></a>Konfigurieren von NPS

Nach der Installation von NPS konfigurieren Sie NPS so, dass alle Authentifizierungs-, Autorisierungs-und Buchhaltungsaufgaben für die Verbindungsanforderung, die Sie vom VPN-Server empfängt, verarbeitet werden.

### <a name="register-the-nps-server-in-active-directory"></a>Registrieren des NPS-Servers in Active Directory

In diesem Verfahren registrieren Sie den Server in Active Directory, damit er beim Verarbeiten von Verbindungsanforderungen über die Berechtigung zum Zugreifen auf Benutzerkontoinformationen verfügt.

**Dringlichkeit**

1.  Klicken Sie in Server-Manager auf **Extras, und wählen Sie dann** **Netzwerk Richtlinien Server**aus. Die NPS-Konsole wird geöffnet.

2.  Klicken Sie in der NPS-Konsole mit der rechten Maustaste auf **NPS (lokal)** , und wählen Sie dann **Server in Active Directory registrieren aus**.
   
     Das Dialogfeld Netzwerkrichtlinienserver wird geöffnet.

3.  Klicken Sie im Dialogfeld Netzwerk Richtlinien Server zweimal auf **OK** .

Alternative Methoden zum Registrieren von NPS finden Sie unter [Registrieren eines NPS-Servers in einem Active Directory-Domäne](../../../../../networking/technologies/nps/nps-manage-register.md).

### <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

In diesem Verfahren konfigurieren Sie die Netzwerk Richtlinien Server-Kontoführung mithilfe eines der folgenden Protokollierungs Typen:

- **Ereignisprotokollierung**. Wird hauptsächlich für die Überwachung und Problembehandlung von Verbindungs versuchen verwendet. Sie können die NPS-Ereignisprotokollierung konfigurieren, indem Sie die NPS-Server Eigenschaften in der NPS-Konsole abrufen.

- **Protokollieren von Benutzerauthentifizierung und Buchhaltungs Anforderungen in einer lokalen Datei**. Wird hauptsächlich für Verbindungs Analyse und Abrechnungszwecke verwendet. Wird auch als Sicherheitsuntersuchung verwendet, da Sie eine Methode zum Nachverfolgen der Aktivität eines böswilligen Benutzers nach einem Angriff bereitstellt. Sie können die lokale Datei Protokollierung mit dem Konfigurations-Assistenten für die Buchhaltung konfigurieren.

- **Protokollieren von Benutzer Authentifizierungs-und Buchhaltungs Anforderungen in einer Microsoft SQL Server XML-kompatiblen Datenbank**. Wird verwendet, um mehreren Servern, auf denen NPS ausgeführt wird, eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server Protokollierung mit dem Konfigurations-Assistenten für die Buchhaltung konfigurieren.

Informationen zum Konfigurieren der Erfassung von Netzwerk Richtlinien Servern finden Sie unter [Konfigurieren der Netzwerk Richtlinien Server](../../../../../networking/technologies/nps/nps-accounting-configure.md)-Kontoführung

### <a name="add-the-vpn-server-as-a-radius-client"></a>Hinzufügen des VPN-Servers als RADIUS-Client

Im Abschnitt [configure the Remote Access Server for Always on VPN](vpn-deploy-ras.md) haben Sie den VPN-Server installiert und konfiguriert. Während der VPN-Serverkonfiguration haben Sie auf dem VPN-Server einen gemeinsamen RADIUS-Schlüssel hinzugefügt.

In diesem Verfahren verwenden Sie die gleiche gemeinsame geheime Text Zeichenfolge, um den VPN-Server als RADIUS-Client in NPS zu konfigurieren. Verwenden Sie dieselbe Text Zeichenfolge, die Sie auf dem VPN-Server verwendet haben, oder die Kommunikation zwischen dem NPS-Server und dem VPN-Server schlägt fehl

>[!IMPORTANT] 
>Wenn Sie einen neuen Netzwerk Zugriffs Server (VPN-Server, drahtlosen Zugriffspunkt, authentifizier enden Switch oder DFÜ-Server) in Ihrem Netzwerk hinzufügen, müssen Sie den Server als RADIUS-Client in NPS hinzufügen, damit NPS die Verbindung mit dem Netzwerk Zugriffs Server kennt und mit ihm kommunizieren kann.

**Dringlichkeit**

1. Doppelklicken Sie auf dem NPS-Server in der NPS-Konsole auf **RADIUS-Clients und-Server**.

2. Klicken Sie mit der rechten Maustaste auf **RADIUS-Clients** und wählen Sie **neu** Das Dialogfeld Neuer RADIUS-Client wird geöffnet.

3. Vergewissern Sie sich, dass das Kontrollkästchen **diesen RADIUS-Client aktivieren aktiviert** ist.

4. Geben Sie unter Anzeige **Name**einen anzeigen Amen für den VPN-Server ein.

5. Geben Sie unter **Adresse (IP oder DNS)** die NAS-IP-Adresse oder den voll qualifizierten Namen ein.
     
     Wenn Sie den FQDN eingeben, wählen Sie **überprüfen** aus, um zu überprüfen, ob der Name richtig ist und einer gültigen IP-Adresse zugeordnet ist.

6. Unter **gemeinsamer geheimer**Schlüssel:

    1. Stellen Sie sicher, dass **manuell** ausgewählt ist.

    2. Geben Sie die starke Text Zeichenfolge ein, die auch auf dem VPN-Server eingegeben wurde.

    3. Geben Sie den gemeinsamen geheimen Schlüssel in Confirm Shared Secret wieder ein.

7. Wählen Sie **OK**. Der VPN-Server wird in der Liste der auf dem NPS-Server konfigurierten RADIUS-Clients angezeigt.

## <a name="configure-nps-as-a-radius-for-vpn-connections"></a>Konfigurieren von NPS als RADIUS für VPN-Verbindungen

In diesem Verfahren konfigurieren Sie NPS als RADIUS-Server in Ihrem Organisations Netzwerk. Auf dem NPS müssen Sie eine Richtlinie definieren, die nur Benutzern in einer bestimmten Gruppe den Zugriff auf die Organisation/das Unternehmensnetzwerk über den VPN-Server ermöglicht. Dies gilt nur, wenn Sie ein gültiges Benutzerzertifikat in einer Anforderung für die Peer-Authentifizierung verwenden.

**Dringlichkeit**

1. Stellen Sie in der NPS-Konsole unter Standard Konfiguration sicher, dass **RADIUS-Server für DFÜ-oder VPN-Verbindungen** ausgewählt ist.

2. Wählen Sie **VPN oder Einwahl konfigurieren**aus.
        
    Der Assistent zum Konfigurieren von VPN oder DFÜ wird geöffnet.

3. Wählen Sie **VPN-Verbindungen (virtuelles privates Netzwerk)** aus, und klicken Sie auf **weiter**.

4. Wählen Sie unter DFÜ-oder VPN-Server angeben in RADIUS-Clients den Namen des VPN-Servers aus, den Sie im vorherigen Schritt hinzugefügt haben. Wenn der NetBIOS-Name des VPN-Servers beispielsweise RAS1 lautet, wählen Sie **RAS1**aus.

5. Klicken Sie auf **Weiter**.

6. Führen Sie unter Konfigurieren von Authentifizierungsmethoden die folgenden Schritte aus:

    1. Deaktivieren Sie das Kontrollkästchen **Microsoft-verschlüsselte Authentifizierung, Version 2 (MS-CHAPv2)** .

    2. Aktivieren Sie das Kontrollkästchen **Extensible Authentication-Protokoll** , um es auszuwählen.

    3. Wählen Sie in Typ (basierend auf der Zugriffs-und Netzwerkkonfiguration) die Option **Microsoft: geschütztes EAP (PEAP)** , und klicken Sie dann auf **Konfigurieren**.
      
        Das Dialogfeld geschützte EAP-Eigenschaften bearbeiten wird geöffnet.

    4. Wählen Sie **Entfernen** aus, um den EAP-Typ des gesicherten Kennworts (EAP-MSCHAP v2) zu entfernen.

    5. Wählen Sie **Hinzufügen**. Das Dialogfeld EAP hinzufügen wird geöffnet.

    6. Wählen Sie **Smartcard oder anderes Zertifikat**aus, und klicken Sie dann auf **OK**.

    7. Wählen Sie **OK** aus, um geschützte EAP-Eigenschaften bearbeiten zu schließen.

7. Klicken Sie auf **Weiter**.

8. Führen Sie unter Benutzergruppen angeben die folgenden Schritte aus:

    1. Wählen Sie **Hinzufügen**. Das Dialogfeld Benutzer, Computer, Dienstkonten oder Gruppen auswählen wird geöffnet.

    2. Geben Sie **VPN-Benutzer**ein, und wählen Sie dann **OK**

    3. Klicken Sie auf **Weiter**.

9. Wählen Sie unter IP-Filter angeben die Option **weiter**aus.

10. Wählen Sie unter Verschlüsselungseinstellungen angeben die Option **weiter**aus. Nehmen Sie keine Änderungen vor.

    Diese Einstellungen gelten nur für MPPE-Verbindungen (Point-to-Point Encryption) von Microsoft, die in diesem Szenario nicht unterstützt werden.

11. Wählen Sie unter Bereichs Namen angeben die Option **weiter**aus.

12. Wählen Sie **Fertig** stellen aus, um den Assistenten zu schließen.

## <a name="autoenroll-the-nps-server-certificate"></a>Automatische Registrierung des NPS-Server Zertifikats

In diesem Verfahren aktualisieren Sie Gruppenrichtlinie auf dem lokalen NPS-Server manuell. Wenn die automatische Registrierung von Zertifikaten konfiguriert ist und ordnungsgemäß funktioniert, wird der lokale Computer von der Zertifizierungsstelle automatisch registriert, wenn Gruppenrichtlinie aktualisiert wird.

>[!NOTE]  
>Gruppenrichtlinie automatisch aktualisiert, wenn Sie den Domänen Mitglieds Computer neu starten oder wenn sich ein Benutzer an einem Domänen Mitglieds Computer anmeldet. Außerdem Gruppenrichtlinie in regelmäßigen Abständen aktualisiert. Standardmäßig erfolgt diese regelmäßige Aktualisierung alle 90 Minuten mit einem zufälligen Offset von bis zu 30 Minuten.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.

**Dringlichkeit**

1. Öffnen Sie Windows PowerShell auf dem NPS.

2. Geben Sie an der Windows PowerShell-Eingabeaufforderung **gpupdate**ein, und drücken Sie dann die EINGABETASTE.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 5: Konfigurieren von DNS-und Firewalleinstellungen für Always on-VPN](vpn-deploy-dns-firewall.md): in diesem Schritt installieren Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe von Windows PowerShell oder dem Assistenten zum Hinzufügen von Rollen und Features Server-Manager. Außerdem können Sie NPS so konfigurieren, dass alle Authentifizierungs-, Autorisierungs-und Buchhaltungsaufgaben für Verbindungsanforderungen verarbeitet werden, die vom VPN-Server empfangen werden.