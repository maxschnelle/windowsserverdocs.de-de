---
title: Konfigurieren der Serverinfrastruktur
description: In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten erforderlich, um das VPN zu unterstützen. Die serverseitigen Komponenten ist die Konfiguration von PKI zum Verteilen der von dem Benutzer, dem VPN-Server und dem NPS-Server verwendeten Zertifikate umfassen.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 21b494bea1990fb8424537205db483d977331465
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832931"
---
# <a name="step-2-configure-the-server-infrastructure"></a>Schritt 2 Konfigurieren der Serverinfrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**Vorherige:** Schritt 1 Planen der Always On-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)<br>
&#187;  [ **Next:** Schritt 3 Konfigurieren der RAS-Server für Always On-VPN](vpn-deploy-ras.md)


In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten erforderlich, um das VPN zu unterstützen. Die serverseitigen Komponenten ist die Konfiguration von PKI zum Verteilen der von dem Benutzer, dem VPN-Server und dem NPS-Server verwendeten Zertifikate umfassen.  Außerdem konfigurieren Sie RRAS, um IKEv2-Verbindungen und der NPS-Server für die Autorisierung für die VPN-Verbindungen zu unterstützen.

## <a name="configure-certificate-autoenrollment-in-group-policy"></a>Konfigurieren der automatischen Registrierung von Zertifikaten in der Gruppenrichtlinie
In diesem Verfahren konfigurieren Sie die Gruppenrichtlinie auf dem Domänencontroller, damit Mitglieder der Domäne automatisch Zertifikate für Benutzer und Computer anfordern. Auf diese Weise können VPN-Benutzer anfordern und Abrufen von Benutzerzertifikaten, die VPN-Verbindungen automatisch authentifizieren. Ebenso kann diese Richtlinie NPS-Servern zum Server anfordern Authentifizierungszertifikate automatisch. 

Manuelles Registrieren Sie Zertifikate für VPN-Server.

>[!TIP]
>Nicht-domained verknüpften Computern finden Sie unter [Zertifizierungsstellenkonfiguration für nicht in die Domäne eingebundenen Computern](#ca-configuration-for-non-domain-joined-computers) unten. Da der RRAS-Server keine Domäne eingebunden ist, kann nicht automatische Registrierung verwendet werden, um das VPN-Gateway-Zertifikat zu registrieren.  Aus diesem Grund gehen Sie eine offline-Zertifikat-Anforderung. 


1.  Öffnen Sie auf einem Domänencontroller die Gruppenrichtlinienverwaltung.

2.  Klicken Sie im Navigationsbereich mit der Maustaste Ihrer Domäne (z. B. "corp.contoso.com"), und klicken Sie auf **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.

3.  Geben Sie auf das Dialogfeld Neues Gruppenrichtlinienobjekt, **Richtlinie für die automatische Registrierung**, und klicken Sie auf **OK**.

4.  Klicken Sie im Navigationsbereich mit der Maustaste **Richtlinie für die automatische Registrierung**, und klicken Sie auf **bearbeiten**.

5.  Führen Sie in der Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte aus, um die zertifikatregistrierung für Computer zu konfigurieren:

    1.  Klicken Sie im Navigationsbereich auf **Computerkonfiguration\\Richtlinien\\Windows-Einstellungen\\Sicherheitseinstellungen\\Richtlinien öffentlicher Schlüssel**.

    2.  Klicken Sie im Detailbereich mit der Maustaste **Zertifikatdiensteclient – automatische Registrierung**, und klicken Sie auf **Eigenschaften**.

    3.  Auf der Zertifikatdiensteclient – automatische Registrierung Eigenschaften Dialogfeld **Konfigurationsmodell**, klicken Sie auf **aktiviert**.

    4.  Wählen Sie **abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate aktualisieren, die Zertifikatvorlagen verwenden**.

    5.  Klicken Sie auf **OK**.

6.  Führen Sie in der Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte aus, um die Benutzer-zertifikatregistrierung konfigurieren:

    1.  Klicken Sie im Navigationsbereich auf **Benutzerkonfiguration\\Richtlinien\\Windows-Einstellungen\\Sicherheitseinstellungen\\Richtlinien öffentlicher Schlüssel**.

    2.  Klicken Sie im Detailbereich mit der Maustaste **Zertifikatdiensteclient – automatische Registrierung**, und klicken Sie auf **Eigenschaften**.

    3.  Auf der Zertifikatdiensteclient – automatische Registrierung Eigenschaften Dialogfeld **Konfigurationsmodell**, klicken Sie auf **aktiviert**.

    4.  Wählen Sie **abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate aktualisieren, die Zertifikatvorlagen verwenden**.

    5.  Klicken Sie auf **OK**.

    6.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

7.  Schließen Sie die Gruppenrichtlinienverwaltung.

### <a name="ca-configuration-for-non-domain-joined-computers"></a>Konfiguration der Zertifizierungsstelle für nicht in die Domäne eingebundenen Computer

Da der RRAS-Server keine Domäne eingebunden ist, kann nicht automatische Registrierung verwendet werden, um das VPN-Gateway-Zertifikat zu registrieren.  Aus diesem Grund gehen Sie eine offline-Zertifikat-Anforderung. 

1. Generieren Sie auf dem RRAS-Server, eine Datei namens **VPNGateway.inf** basierend auf der Beispiel-Richtlinie zertifikatanforderung im Anhang bereitgestellt, (Abschnitt 0), und passen Sie die folgenden Einträge: 

   - Ersetzen Sie im Abschnitt [NewRequest] verwendet, für den Antragstellernamen, mit der ausgewählten vpn.contoso.com [_Kunden_] VPN-Endpunkt FQDN.

   - Ersetzen Sie im Abschnitt [Extensions] verwendet, für den alternativen Antragstellernamen mit der ausgewählten vpn.contoso.com [_Kunden_] VPN-Endpunkt FQDN.

2. Speichern oder kopieren Sie die **VPNGateway.inf** Datei in einer ausgewählten Stelle ein.

3. Eine Eingabeaufforderung mit erhöhten Rechten, navigieren Sie zu dem Ordner mit den **VPNGateway.inf** Datei, und geben:

   ```
   certreq -new VPNGateway.inf VPNGateway.req
   ```

4. Kopieren Sie die neu erstellte **VPNGateway.req** Ausgabedatei auf einer Zertifizierungsstelle oder (Privileged Access Workstation, PAW). 

5. Speichern oder kopieren Sie die **VPNGateway.req** Datei an einem ausgewählten Speicherort auf dem Server der Zertifizierungsstelle, oder (Privileged Access Workstation, PAW).

6. Eine Eingabeaufforderung mit erhöhten Rechten navigieren Sie zu dem Ordner, der die in den vorherigen Schritt und den Typ erstellte VPNGateway.req-Datei enthält: 

   ```
   certreq -attrib “CertificateTemplate:[Customer]VPNGateway” -submit VPNgateway.req VPNgateway.cer
   ```

7. Wenn Sie dazu aufgefordert werden, indem Sie die Liste der Zertifizierungsstellen-Fenster, wählen Sie die entsprechende Enterprise-Zertifizierungsstelle die zertifikatanforderung zu verarbeiten.

8. Kopieren Sie die neu erstellte **VPNGateway.cer** Ausgabedatei auf dem RRAS-Server. 

9. Speichern oder kopieren Sie die **VPNGateway.cer** Datei an einem ausgewählten Speicherort auf dem RRAS-Server.

10. Eine Eingabeaufforderung mit erhöhten Rechten navigieren Sie zu dem Ordner, der die in den vorherigen Schritt und den Typ erstellte VPNGateway.cer-Datei enthält:
   
   ```
   certreq -accept VPNGateway.cer
   ```

11. Führen das Zertifikate-MMC-Snap-in, wie beschrieben [hier](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in) Auswählen der **Computerkonto** Option.

12. Stellen Sie sicher, dass ein gültiges Zertifikat für den RRAS-Server mit den folgenden Eigenschaften vorhanden ist:

   - **Beabsichtigte Zwecke:** Server-Authentifizierung, IP-Sicherheits-IKE, dazwischenliegend 

   - **Zertifikatvorlage:** [_Kunden_] VPN-Server

#### <a name="example-vpngatewayinf-script"></a>Beispiel: VPNGateway.inf script

Hier sehen Sie ein Beispielskript, der eine Zertifikatrichtlinie-Anforderung verwendet, um ein VPN-Gateway-Zertifikat mithilfe eines Out-of-Band-Prozesses anzufordern.

>[!TIP]
>Eine Kopie des Skripts VPNGateway.inf finden Sie im VPN-Angebot IP-Kit unter dem Ordner Zertifikatsrichtlinien anfordern. Aktualisiert nur die "Subject" und "\_weiterhin\_" mit bestimmten Werten von Kunden.

```
[Version] 

Signature="$Windows NT$"

[NewRequest]
Subject = "CN=vpn.contoso.com"
Exportable = FALSE   
KeyLength = 2048     
KeySpec = 1          
KeyUsage = 0xA0      
MachineKeySet = True
ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
RequestType = PKCS10 

[Extensions]
2.5.29.17 = "{text}"
_continue_ = "dns=vpn.contoso.com&"

```

## <a name="create-the-vpn-users-vpn-servers-and-nps-servers-groups"></a>Erstellen von VPN-Benutzer, VPN-Server und NPS-Server-Gruppen

In diesem Verfahren können Sie eine neue Active Directory (AD)-Gruppe hinzufügen, die der Benutzer auf das VPN verwenden, für die Verbindung mit dem Netzwerk Ihrer Organisation enthält.

Diese Gruppe dient zwei Zwecken:

-   Sie definiert, welche Benutzer zur automatischen Registrierung für Benutzerzertifikate zulässig sind, die das VPN erforderlich sind.

-   Es definiert, welche Benutzer der NPS für VPN-Zugriff autorisiert.

Verwenden Sie eine benutzerdefinierte Gruppe, wenn Sie VPN-Zugriff des Benutzers widerrufen möchten können Sie diesen Benutzer aus der Gruppe entfernen.

Sie fügen auch eine Gruppe, die VPN-Server und eine andere Gruppe, die mit der NPS-Server hinzu. Sie können diese Gruppen verwenden, um zertifikatanforderungen an ihre Member zu beschränken.

>[!NOTE] 
>Es wird empfohlen, VPN-Server, die im DMA/Umkreisnetzwerk befinden sich nicht mit domänenverknüpfung. Jedoch wenn Sie die VPN-Server mit domänenverknüpfung zur Verbesserung der Verwaltbarkeit möchten hinzufügen (Gruppenrichtlinien, Sicherung/Überwachungsagent keine lokalen Benutzer verwalten und so weiter), klicken Sie dann eine AD-Gruppe mit der Zertifikatvorlage für VPN-Server.

### <a name="configure-the-vpn-users-group"></a>Konfigurieren Sie die VPN-Benutzer-Gruppe

1.  Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und Computer aus.

2.  Ein Container oder die Organisationseinheit, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.

3.  In **Gruppenname**, Typ **VPN-Benutzer**, und klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Benutzer**, und klicken Sie auf **Eigenschaften**.

5.  Auf der **Mitglieder** Registerkarte im Dialogfeld Eigenschaften von VPN-Benutzer, klicken Sie auf **hinzufügen**.

6.  Fügen Sie auf das Dialogfeld Auswahl von Benutzern, alle Benutzer, die VPN-Zugriff, und klicken Sie auf **OK**.

7.  Schließen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.

### <a name="configure-the-vpn-servers-and-nps-servers-groups"></a>Konfigurieren Sie die VPN-Server und NPS-Server-Gruppen

1.  Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und Computer aus.

2.  Ein Container oder die Organisationseinheit, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.

3.  In **Gruppenname**, Typ **VPN-Server**, und klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Server**, und klicken Sie auf **Eigenschaften**.

5.  Auf der **Mitglieder** Registerkarte im Dialogfeld Eigenschaften von VPN-Servers, klicken Sie auf **hinzufügen**.

6.  Klicken Sie auf **Objekttypen**, wählen die **Computer** , und klicken Sie auf **OK**.

7.  In **Geben Sie die zu verwendenden Objektnamen**, geben Sie die Namen Ihrer VPN-Server, und klicken Sie auf **OK**.

8.  Klicken Sie auf **OK** um das Dialogfeld Eigenschaften von VPN-Servers zu schließen.

9.  Wiederholen Sie die vorherigen Schritte für die NPS-Server-Gruppe ein.

10. Schließen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.

## <a name="create-the-user-authentication-template"></a>Erstellen Sie die Vorlage für die Benutzerauthentifizierung

In diesem Verfahren konfigurieren Sie eine benutzerdefinierten Client / Server-Authentifizierung-Vorlage. Diese Vorlage ist erforderlich, da Sie die allgemeine Sicherheit des Zertifikats zu verbessern, indem Sie die aktualisierten Kompatibilitätsgrade möchten und wählen den Kryptografieanbieter für Microsoft-Plattform. Dieser letzten Änderung können Sie das TPM auf den Clientcomputern zu verwenden, um das Zertifikat zu sichern. Eine Übersicht über das TPM, finden Sie unter [Trusted Platform Module – Technologieübersicht](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview).

**Vorgehensweise:**

1.  Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2.  Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen**, und klicken Sie auf **verwalten**.

3.  In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **Benutzer**, und klicken Sie auf **Doppelte Vorlage**.

    >[!WARNING]
    >Klicken Sie nicht auf **übernehmen** oder **OK** jederzeit vor dem Schritt 10 fort.  Wenn Sie diese Schaltflächen klicken, bevor Sie alle Parameter eingeben, werden viele Möglichkeiten, festen und nicht mehr bearbeitet werden. Z. B. auf die **Kryptografie** bei Registerkarte _Legacy-Speicher Kryptografieanbieter_ zeigt in den Anbieterkategorie, er wird deaktiviert, verhindern, dass keine weiteren Änderungen. Die einzige alternative ist die Vorlage löschen und neu erstellen.  

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte, die folgenden Schritte ausführen:

    1.  In **Vorlagenanzeigename**, Typ **VPN-Benutzerauthentifizierung**.

    2.  Deaktivieren der **Zertifikat in Active Directory veröffentlichen** Kontrollkästchen.

5.  Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Geben Sie auf die Auswahl von Benutzern, Computer, Dienstkonten oder Gruppen (Dialogfeld), **VPN-Benutzer**, und klicken Sie auf **OK**.

    3.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **VPN-Benutzer**.

    4.  In **Berechtigungen für die VPN-Benutzer**, wählen die **registrieren** und **automatisch registrieren** Kontrollkästchen in der **zulassen** Spalte.

       >[!TIP]
       >Stellen Sie sicher, dass das Kontrollkästchen "Lesen" aktiviert bleiben. Das heißt, benötigen Sie die Berechtigungen zum Lesen, für die Registrierung. 

    5.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **Domänenbenutzer**, und klicken Sie auf **entfernen**.

6.  Auf der **Kompatibilität** Registerkarte, die folgenden Schritte ausführen:

    1.  In **Zertifizierungsstelle**, klicken Sie auf **Windows Server 2012 R2**.

    2.  Auf der **resultierende Änderungen** Dialogfeld klicken Sie auf **OK**.

    3.  In **Zertifikatsempfänger**, klicken Sie auf **Windows 8.1 / Windows Server 2012 R2**.

    4.  Auf der **resultierende Änderungen** Dialogfeld klicken Sie auf **OK**.

7.  Auf der **Anforderungsverarbeitung** Registerkarte die **privatem Schlüssel zulassen zu exportierenden** Kontrollkästchen.

8.  Auf der **Kryptografie** Registerkarte, die folgenden Schritte ausführen:

    1.  In **Anbieterkategorie**, klicken Sie auf **Schlüsselspeicheranbieter**.

    2.  Klicken Sie auf **Anforderungen müssen eine der folgenden Anbieter verwenden**.

    3.  Wählen Sie die **Kryptografieanbieter für Microsoft-Plattform** Kontrollkästchen.

9.  Auf der **Antragstellername** Registerkarte, wenn Ihnen eine e-Mail-Adresse, die auf alle Benutzerkonten aufgelistet sind, Löschen keine der **-e-Mail-Name im Antragstellernamen einschließen** und **e-Mail-Name** Kontrollkästchen.

10. Klicken Sie auf **OK** zum Speichern der Benutzerauthentifizierung für die VPN-Zertifikat-Vorlage.

11. Schließen Sie die Zertifikatvorlagenkonsole.

12. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf **Auszustellende Zertifikatvorlage**.

13. Klicken Sie auf **VPN-Benutzerauthentifizierung**, und klicken Sie auf **OK**.

14. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="create-the-vpn-server-authentication-template"></a>Erstellen Sie die Vorlage für VPN-Server-Authentifizierung

In diesem Verfahren können Sie eine neue Vorlage für den Server-Authentifizierung für Ihre VPN-Server konfigurieren. Hinzufügen, dass die IP-Sicherheit (IPsec) IKE Intermediate-Anwendungsrichtlinie kann der Server zum Filtern von Zertifikaten aus, wenn mehr als ein Zertifikat mit dem Server-Authentifizierung verfügbar ist, erweiterte Schlüsselverwendung.

>[!IMPORTANT] 
>Da VPN-Clients auf diesem Server über das öffentliche Internet zugreifen, unterscheiden sich die Antragsteller und alternativen Namen als Namen des internen Servers. Daher können Sie nicht automatisch registrieren dieses Zertifikat auf VPN-Servern.

**Voraussetzungen:**<p>
VPN-Server mit domänenverknüpfung

**Vorgehensweise:** 

1.  Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2.  Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen**, und klicken Sie auf **verwalten**.

3.  In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **RAS- und IAS-Server**, und klicken Sie auf **Doppelte Vorlage**.

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte **Vorlagenanzeigename**, geben Sie einen beschreibenden Namen für die VPN-Server, z. B. **VPN-Server Authentifizierung** oder **RADIUS-Server**.

5.  Auf der **Erweiterungen** Registerkarte, die folgenden Schritte ausführen:

    1.  Klicken Sie auf **Anwendungsrichtlinien**, und klicken Sie auf **bearbeiten**.

    2.  In der **Anwendungsrichtlinienerweiterung** Dialogfeld klicken Sie auf **hinzufügen**.

    3.  Auf der **Anwendungsrichtlinie hinzufügen** Dialogfeld klicken Sie auf **IP-Sicherheits-IKE, dazwischenliegend**, und klicken Sie auf **OK**.<p>Hinzufügen von IP-hilft Sicherheits-IKE, dazwischenliegend EKU in Szenarien, in denen mehrere CMG-Serverauthentifizierungszertifikat auf dem VPN-Server vorhanden ist. Wenn IP-Sicherheits-IKE, dazwischenliegend vorhanden ist, verwendet IPSec nur das Zertifikat mit EKU. Ohne diesen Schritt tritt Fehler 13801 IKEv2-Authentifizierung konnte: IKE-Authentifizierungsinformationen sind nicht akzeptabel.

    4.  Klicken Sie auf **OK** zum Zurückgeben der **Eigenschaften der neuen Vorlage** Dialogfeld.

6.  Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Auf der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** (Dialogfeld), Typ **VPN-Server**, und klicken Sie auf **OK**.

    3.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **VPN-Server**.

    4.  In **Berechtigungen für die VPN-Server**, wählen die **registrieren** Kontrollkästchen in der **zulassen** Spalte.

    5.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **RAS- und IAS-Server**, und klicken Sie auf **entfernen**.

7.  Auf der **Antragstellername** Registerkarte, die folgenden Schritte ausführen:

    1.  Klicken Sie auf **Geben Sie in der Anforderung**.

    2.  Auf der **Zertifikatvorlagen** klicken Sie im Dialogfeld Warnung **OK**.

8.  (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren*, klicken Sie auf die **Anforderungsverarbeitung** Registerkarte, und klicken Sie auf **privatem Schlüssel zulassen zu exportierenden** um es auszuwählen.

9.  Klicken Sie auf **OK** um die Zertifikatvorlage für die VPN-Server zu speichern.

10. Schließen Sie die Zertifikatvorlagenkonsole.

11. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf **Auszustellende Zertifikatvorlage**.

12. Starten Sie die Dienste für die Zertifizierungsstelle neu.

13. Wählen Sie den Namen, die Sie in Schritt 4 ausgewählt haben, und klicken Sie auf **OK**.

14. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="create-the-nps-server-authentication-template"></a>Erstellen Sie die Vorlage für die NPS-Server-Authentifizierung

Die dritte und letzte Zertifikatvorlage erstellen wird die Vorlage für die NPS-Server-Authentifizierung. Die Vorlage für die NPS-Server-Authentifizierung ist eine einfache Kopie der Vorlage RAS- und IAS-Server geschützt werden, um die NPS-Server-Gruppe, die Sie zuvor in diesem Abschnitt erstellt haben. 

Konfigurieren Sie dieses Zertifikat für die automatische Registrierung.

**Vorgehensweise:**

1.  Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2.  Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen**, und klicken Sie auf **verwalten**.

3.  In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **RAS- und IAS-Server**, und wählen Sie **Doppelte Vorlage**.

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte **Vorlagenanzeigename**, Typ **NPS-Server-Authentifizierung**.

5.  Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Auf der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** (Dialogfeld), Typ **NPS-Server**, und klicken Sie auf **OK**.

    3.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **NPS-Server**.

    4.  In **Berechtigungen für die NPS-Server**, wählen die **registrieren** und **automatisch registrieren** Kontrollkästchen in der **zulassen** Spalte.

    5.  In **Gruppen-oder Benutzernamen**, klicken Sie auf **RAS- und IAS-Server**, und klicken Sie auf **entfernen**.

6.  Klicken Sie auf **OK** um die NPS-Server-Zertifikatvorlage zu speichern.

7.  Schließen Sie die Zertifikatvorlagenkonsole.

8.  Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf **Auszustellende Zertifikatvorlage**.

9.  Klicken Sie auf **NPS-Server-Authentifizierung**, und klicken Sie auf **OK**.

10. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="enroll-and-validate-the-user-certificate"></a>Registrieren Sie und überprüfen Sie das Benutzerzertifikat

Da Sie die Gruppenrichtlinie, damit Benutzerzertifikate verwenden, müssen Sie nur die Richtlinie aktualisieren und Windows 10 wird automatisch das Benutzerkonto für das richtige Zertifikat registrieren. Sie können dann das Zertifikat in der Zertifikatkonsole überprüfen.

**Vorgehensweise:**

1.  Melden Sie sich bei einer Domäne eingebundenen Client-Computer als Mitglied der **VPN-Benutzer** Gruppe.

2.  Drücken Sie die Windows-Taste + R, Typ **Gpupdate/force**, und drücken Sie EINGABETASTE.

3.  Geben Sie im Menü Start **"Certmgr.msc"**, und drücken Sie EINGABETASTE.

4.  Klicken Sie in das Zertifikate-Snap-in unter **persönliche**, klicken Sie auf **Zertifikate**. Die Zertifikate werden im Detailbereich angezeigt.

5.  Mit der rechten Maustaste in des Zertifikats mit Ihrer aktuellen Domäne Benutzername ein, und klicken Sie dann auf **öffnen**.

6.  Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Wenn sie nicht der Fall ist, haben Sie möglicherweise das falsche Zertifikat ausgewählt.

7.  Klicken Sie auf **OK**, und schließen Sie das Zertifikate-Snap-in.

## <a name="enroll-and-validate-the-server-certificates"></a>Registrieren Sie und überprüfen Sie die Serverzertifikate

Im Gegensatz zu das Zertifikat müssen Sie das VPN-Zertifikat des Servers manuell registrieren. Nachdem sie registriert haben, überprüfen Sie sie durch die gleiche Weise wie für das Benutzerzertifikat. Wie das Benutzerzertifikat registriert der NPS-Server automatisch ein Clientauthentifizierungszertifikat, also alles, was Sie tun müssen sie überprüfen.

>[!NOTE] 
>Sie müssen möglicherweise neu starten der VPN- und NPS-Server können sie Gruppenmitgliedschaften zu aktualisieren, bevor Sie diese Schritte ausführen können.

### <a name="enroll-and-validate-the-vpn-server-certificate"></a>Registrieren Sie und überprüfen Sie des VPN-Server-Zertifikats

1.  Geben Sie auf das Menü "Start" die VPN-Server, **"certlm.msc"**, und drücken Sie EINGABETASTE.

2.  Mit der rechten Maustaste **persönliche**, klicken Sie auf **alle Aufgaben** , und klicken Sie dann auf **neues Zertifikat anfordern** der Zertifikatregistrierungs-Assistent gestartet.

3.  Klicken Sie auf der Seite Vorbemerkungen auf **Weiter**.

4.  Klicken Sie auf der Seite Zertifikatregistrierungsrichtlinie auswählen auf **Weiter**.

5.  Klicken Sie auf der Seite anfordern von Zertifikaten auf das Kontrollkästchen neben dem VPN-Server, um es auszuwählen.

6.  Klicken Sie das Kontrollkästchen VPN-Server unter auf **ist erforderlich, Weitere Informationen** Öffnet das Dialogfeld Zertifikateigenschaften (Dialogfeld), und führen Sie folgende Schritte:

    1.  Klicken Sie auf die **Betreff** auf **allgemeiner Name** unter **Antragstellername**im **Typ**.

    2.  Klicken Sie unter **Antragstellername**im **Wert**, geben Sie den Namen der externen Domänenclients verwendet, um die Verbindung zum VPN, z. B. vpn.contoso.com, und klicken Sie auf **hinzufügen**.

    3.  Klicken Sie unter **alternativen Antragstellernamen**im **Typ**, klicken Sie auf **DNS**.

    4.  Klicken Sie unter **alternativen Antragstellernamen**im **Wert**, geben Sie alle Servernamen, die Clients verwenden, um mit dem VPN, z. B. eine Verbindung herstellen, vpn.contoso.com, Vpn, 132.64.86.2.

    5.  Klicken Sie auf **hinzufügen** nach dem Eingeben der Namen der einzelnen.

    6.  Klicken Sie anschließend auf **OK**.

7.  Klicken Sie auf **Registrieren**.

8.  Klicken Sie auf **Fertig stellen**.

9.  Klicken Sie in das Zertifikate-Snap-in unter **persönliche**, klicken Sie auf **Zertifikate**.<p>Die aufgeführten Zertifikate werden im Detailbereich angezeigt.

10. Mit der rechten Maustaste in des Zertifikats mit der VPN-Server den Namen, und klicken Sie dann auf **öffnen**.

11. Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Falls nicht, können Sie nicht das richtige Zertifikat ausgewählt haben.

12. Auf der **Details** auf **Enhanced Key Usage**, und überprüfen Sie, ob **IP-Sicherheits-IKE, dazwischenliegend** und **Serverauthentifizierung** in der Liste angezeigt.

13. Klicken Sie auf **OK** um das Zertifikat zu schließen.

14. Schließen Sie das Zertifikate-Snap-in.

### <a name="validate-the-nps-server-certificate"></a>Überprüfen Sie die NPS-Serverzertifikats

1.  Starten Sie den NPS-Server neu.

2.  Geben Sie auf dem NPS-Server im Menü Start **"certlm.msc"**, und drücken Sie EINGABETASTE.

3.  Klicken Sie in das Zertifikate-Snap-in unter **persönliche**, klicken Sie auf **Zertifikate**.<p>Die aufgeführten Zertifikate werden im Detailbereich angezeigt.

4.  Mit der rechten Maustaste in des Zertifikats mit dem NPS-Server den Namen, und klicken Sie dann auf **öffnen**.

5.  Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Falls nicht, können Sie nicht das richtige Zertifikat ausgewählt haben.

6.  Klicken Sie auf **OK** um das Zertifikat zu schließen.

7.  Schließen Sie das Zertifikate-Snap-in.

## <a name="next-step"></a>Nächster Schritt
[Schritt 3. Konfigurieren Sie die RAS-Server für Always On-VPN-](vpn-deploy-ras.md): In diesem Schritt konfigurieren Sie RAS-VPN IKEv2-VPN-Verbindungen zulassen, verweigern Verbindungen von anderen VPN-Protokolle und zuweisen einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zum Herstellen einer Verbindung autorisierte VPN-Clients.







---
