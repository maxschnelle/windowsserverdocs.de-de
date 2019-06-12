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
ms.openlocfilehash: 8a07d84427b770da465b8712d71eb846a7c9cf8d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749603"
---
# <a name="step-2-configure-the-server-infrastructure"></a>Schritt 2 Konfigurieren der Serverinfrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorherige:** Schritt 1 Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md)
- [**nächster:** Schritt 3 Konfigurieren des RAS-Servers für Always On VPN](vpn-deploy-ras.md)

In diesem Schritt haben Sie installieren und konfigurieren Sie die serverseitigen Komponenten erforderlich, um das VPN zu unterstützen. Die serverseitigen Komponenten ist die Konfiguration von PKI zum Verteilen der von dem Benutzer, dem VPN-Server und dem NPS-Server verwendeten Zertifikate umfassen.  Außerdem konfigurieren Sie RRAS, um IKEv2-Verbindungen und der NPS-Server für die Autorisierung für die VPN-Verbindungen zu unterstützen.

## <a name="configure-certificate-autoenrollment-in-group-policy"></a>Konfigurieren der automatischen Registrierung von Zertifikaten in der Gruppenrichtlinie
In diesem Verfahren konfigurieren Sie die Gruppenrichtlinie auf dem Domänencontroller, damit Mitglieder der Domäne automatisch Zertifikate für Benutzer und Computer anfordern. Auf diese Weise können VPN-Benutzer anfordern und Abrufen von Benutzerzertifikaten, die VPN-Verbindungen automatisch authentifizieren. Ebenso kann diese Richtlinie NPS-Servern zum Server anfordern Authentifizierungszertifikate automatisch. 

Manuelles Registrieren Sie Zertifikate für VPN-Server.

>[!TIP]
>Nicht-domained verknüpften Computern finden Sie unter [Zertifizierungsstellenkonfiguration für nicht in die Domäne eingebundenen Computern](#ca-configuration-for-non-domain-joined-computers). Da der RRAS-Server keine Domäne eingebunden ist, kann nicht automatische Registrierung verwendet werden, um das VPN-Gateway-Zertifikat zu registrieren.  Aus diesem Grund gehen Sie eine offline-Zertifikat-Anforderung.

1. Öffnen Sie auf einem Domänencontroller die Gruppenrichtlinienverwaltung.

2. Klicken Sie im Navigationsbereich mit der rechten Maustaste in der Domäne (z. B. "corp.contoso.com"), und wählen Sie dann **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.

3. Geben Sie auf das Dialogfeld Neues Gruppenrichtlinienobjekt, **Richtlinie für die automatische Registrierung**, und wählen Sie dann **OK**.

4. Klicken Sie im Navigationsbereich mit der Maustaste **Richtlinie für die automatische Registrierung**, und wählen Sie dann **bearbeiten**.

5. Führen Sie in der Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte aus, um die zertifikatregistrierung für Computer zu konfigurieren:

    1. Navigieren Sie im Navigationsbereich zu **Computerkonfiguration** > **Richtlinien** > **Windows-Einstellungen**  >   **Sicherheitseinstellungen** > **Richtlinien für öffentliche Schlüssel**.

    2. Klicken Sie im Detailbereich mit der Maustaste **Zertifikatdiensteclient – automatische Registrierung**, und wählen Sie dann **Eigenschaften**.

    3. Auf der Zertifikatdiensteclient – automatische Registrierung Eigenschaften Dialogfeld **Konfigurationsmodell**Option **aktiviert**.

    4. Wählen Sie **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren** aus.

    5. Wählen Sie **OK**.

6. Führen Sie in der Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte aus, um die Benutzer-zertifikatregistrierung konfigurieren:

    1. Navigieren Sie im Navigationsbereich zu **Benutzerkonfiguration** > **Richtlinien** > **Windows-Einstellungen**  >   **Sicherheitseinstellungen** > **Richtlinien für öffentliche Schlüssel**.

    2. Klicken Sie im Detailbereich mit der rechten Maustaste auf **Zertifikatdienstclient - Automatische Registrierung**, und wählen Sie **Eigenschaften** aus.

    3. Auf der Zertifikatdiensteclient – automatische Registrierung Eigenschaften Dialogfeld **Konfigurationsmodell**Option **aktiviert**.

    4. Wählen Sie **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren** aus.

    5. Wählen Sie **OK**.

    6. Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

7. Schließen Sie die Gruppenrichtlinienverwaltung.

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
>Eine Kopie des Skripts VPNGateway.inf finden Sie im VPN-Angebot IP-Kit unter dem Ordner Zertifikatsrichtlinien anfordern. Aktualisiert nur die "Subject" und "\_weiterhin\_" kundenspezifische Werte.

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

- Sie definiert, welche Benutzer zur automatischen Registrierung für Benutzerzertifikate zulässig sind, die das VPN erforderlich sind.

- Es definiert, welche Benutzer der NPS für VPN-Zugriff autorisiert.

Verwenden Sie eine benutzerdefinierte Gruppe, wenn Sie VPN-Zugriff des Benutzers widerrufen möchten können Sie diesen Benutzer aus der Gruppe entfernen.

Sie fügen auch eine Gruppe, die VPN-Server und eine andere Gruppe, die mit der NPS-Server hinzu. Sie können diese Gruppen verwenden, um zertifikatanforderungen an ihre Member zu beschränken.

>[!NOTE]
>Es wird empfohlen, VPN-Server, die im DMA/Umkreisnetzwerk befinden sich nicht mit domänenverknüpfung. Jedoch wenn Sie die VPN-Server mit domänenverknüpfung zur Verbesserung der Verwaltbarkeit möchten hinzufügen (Gruppenrichtlinien, Sicherung/Überwachungsagent keine lokalen Benutzer verwalten und so weiter), klicken Sie dann eine AD-Gruppe mit der Zertifikatvorlage für VPN-Server.

### <a name="configure-the-vpn-users-group"></a>Konfigurieren Sie die VPN-Benutzer-Gruppe

1. Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und Computer aus.

2. Mit der rechten Maustaste einen Container oder die Organisationseinheit, Option **neu**, und wählen Sie dann **Gruppe**.

3. In **Gruppenname**, geben Sie **VPN-Benutzer**, und wählen Sie dann **OK**.

4. Mit der rechten Maustaste **VPN-Benutzer** , und wählen Sie **Eigenschaften**.

5. Auf der **Mitglieder** die Eigenschaften der VPN-Benutzer wählen Sie im Dialogfeld auf der Registerkarte **hinzufügen**.

6. Fügen Sie auf das Dialogfeld Auswahl von Benutzern, alle Benutzer, die VPN-Zugriff, und wählen **OK**.

7. Schließen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.

### <a name="configure-the-vpn-servers-and-nps-servers-groups"></a>Konfigurieren Sie die VPN-Server und NPS-Server-Gruppen

1. Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und Computer aus.

2. Mit der rechten Maustaste einen Container oder die Organisationseinheit, Option **neu**, und wählen Sie dann **Gruppe**.

3. In **Gruppenname**, geben Sie **VPN-Server**, und wählen Sie dann **OK**.

4. Mit der rechten Maustaste **VPN-Server** , und wählen Sie **Eigenschaften**.

5. Auf der **Mitglieder** die Eigenschaften der VPN-Server wählen Sie im Dialogfeld auf der Registerkarte **hinzufügen**.

6. Wählen Sie **Objekttypen**, wählen die **Computer** Kontrollkästchen aus, und wählen Sie dann **OK**.

7. In **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Namen Ihrer VPN-Server, und wählen Sie dann **OK**.

8. Wählen Sie **OK** um das Dialogfeld Eigenschaften von VPN-Servers zu schließen.

9. Wiederholen Sie die vorherigen Schritte für die NPS-Server-Gruppe ein.

10. Schließen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.

## <a name="create-the-user-authentication-template"></a>Erstellen Sie die Vorlage für die Benutzerauthentifizierung

In diesem Verfahren konfigurieren Sie eine benutzerdefinierten Client / Server-Authentifizierung-Vorlage. Diese Vorlage ist erforderlich, da Sie die allgemeine Sicherheit des Zertifikats zu verbessern, indem Sie die aktualisierten Kompatibilitätsgrade möchten und wählen den Kryptografieanbieter für Microsoft-Plattform. Dieser letzten Änderung können Sie das TPM auf den Clientcomputern zu verwenden, um das Zertifikat zu sichern. Eine Übersicht über das TPM, finden Sie unter [Trusted Platform Module – Technologieübersicht](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview).

**Vorgehensweise:**

1. Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2. Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen** , und wählen Sie **verwalten**.

3. In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **Benutzer** , und wählen Sie **Doppelte Vorlage**.

   >[!WARNING]
   >Aktivieren Sie nicht **übernehmen** oder **OK** jederzeit vor dem Schritt 10 fort.  Wenn Sie diese Schaltflächen auswählen, bevor Sie alle Parameter eingeben, werden viele Möglichkeiten, festen und nicht mehr bearbeitet werden. Z. B. auf die **Kryptografie** bei Registerkarte _Legacy-Speicher Kryptografieanbieter_ zeigt in den Anbieterkategorie, er wird deaktiviert, verhindern, dass keine weiteren Änderungen. Die einzige alternative ist die Vorlage löschen und neu erstellen.  

4. Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte, die folgenden Schritte ausführen:

   1. In **Vorlagenanzeigename**, Typ **VPN-Benutzerauthentifizierung**.

   2. Deaktivieren der **Zertifikat in Active Directory veröffentlichen** Kontrollkästchen.

5. Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

   1. Wählen Sie **hinzufügen**.

   2. Geben Sie auf die Auswahl von Benutzern, Computer, Dienstkonten oder Gruppen (Dialogfeld), **VPN-Benutzer**, und wählen Sie dann **OK**.

   3. In **Gruppen-oder Benutzernamen**Option **VPN-Benutzer**.

   4. In **Berechtigungen für die VPN-Benutzer**, wählen die **registrieren** und **automatisch registrieren** Kontrollkästchen in der **zulassen** Spalte.

      >[!TIP]
      >Stellen Sie sicher, dass das Kontrollkästchen "Lesen" aktiviert bleiben. Das heißt, benötigen Sie die Berechtigungen zum Lesen, für die Registrierung. 

   5. In **Gruppen-oder Benutzernamen**Option **Domänenbenutzer**, und wählen Sie dann **entfernen**.

6. Auf der **Kompatibilität** Registerkarte, die folgenden Schritte ausführen:

   1. In **Zertifizierungsstelle**Option **Windows Server 2012 R2**.

   2. Auf der **resultierende Änderungen** wählen Sie im Dialogfeld **OK**.

   3. In **Zertifikatsempfänger**Option **Windows 8.1 / Windows Server 2012 R2**.

   4. Auf der **resultierende Änderungen** wählen Sie im Dialogfeld **OK**.

7. Auf der **Anforderungsverarbeitung** Registerkarte die **privatem Schlüssel zulassen zu exportierenden** Kontrollkästchen.

8. Auf der **Kryptografie** Registerkarte, die folgenden Schritte ausführen:

   1. In **Anbieterkategorie**Option **Schlüsselspeicheranbieter**.

   2. Wählen Sie **Anforderungen müssen eine der folgenden Anbieter verwenden**.

   3. Wählen Sie die **Kryptografieanbieter für Microsoft-Plattform** Kontrollkästchen.

9. Auf der **Antragstellername** Registerkarte, wenn Ihnen eine e-Mail-Adresse, die auf alle Benutzerkonten aufgelistet sind, Löschen keine der **-e-Mail-Name im Antragstellernamen einschließen** und **e-Mail-Name** Kontrollkästchen.

10. Wählen Sie **OK** zum Speichern der Benutzerauthentifizierung für die VPN-Zertifikat-Vorlage.

11. Schließen Sie die Zertifikatvorlagenkonsole.

12. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**Option **neu** und wählen Sie dann **Auszustellende Zertifikatvorlage**.

13. Wählen Sie **VPN-Benutzerauthentifizierung**, und wählen Sie dann **OK**.

14. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="create-the-vpn-server-authentication-template"></a>Erstellen Sie die Vorlage für VPN-Server-Authentifizierung

In diesem Verfahren können Sie eine neue Vorlage für den Server-Authentifizierung für Ihre VPN-Server konfigurieren. Hinzufügen, dass die IP-Sicherheit (IPsec) IKE Intermediate-Anwendungsrichtlinie kann der Server zum Filtern von Zertifikaten aus, wenn mehr als ein Zertifikat mit dem Server-Authentifizierung verfügbar ist, erweiterte Schlüsselverwendung.

>[!IMPORTANT]
>Da VPN-Clients auf diesem Server über das öffentliche Internet zugreifen, unterscheiden sich die Antragsteller und alternativen Namen als Namen des internen Servers. Daher können Sie nicht automatisch registrieren dieses Zertifikat auf VPN-Servern.

**Voraussetzungen:**

VPN-Server mit domänenverknüpfung

**Vorgehensweise:**

1. Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2. Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen** , und wählen Sie **verwalten**.

3. In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **RAS- und IAS-Server** , und wählen Sie **Doppelte Vorlage**.

4. Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte **Vorlagenanzeigename**, geben Sie einen beschreibenden Namen für die VPN-Server, z. B. **VPN-Server-Authentifizierung** oder **RADIUS-Server**.

5. Auf der **Erweiterungen** Registerkarte, die folgenden Schritte ausführen:

    1. Wählen Sie **Anwendungsrichtlinien**, und wählen Sie dann **bearbeiten**.

    2. In der **Anwendungsrichtlinienerweiterung** wählen Sie im Dialogfeld **hinzufügen**.

    3. Auf der **Anwendungsrichtlinie hinzufügen** wählen Sie im Dialogfeld **IP-Sicherheits-IKE, dazwischenliegend**, und wählen Sie dann **OK**.
   
        Hinzufügen von IP-hilft Sicherheits-IKE, dazwischenliegend EKU in Szenarien, in denen mehrere CMG-Serverauthentifizierungszertifikat auf dem VPN-Server vorhanden ist. Wenn IP-Sicherheits-IKE, dazwischenliegend vorhanden ist, verwendet IPSec nur das Zertifikat mit EKU. Ohne diesen Schritt tritt Fehler 13801 IKEv2-Authentifizierung konnte: IKE-Authentifizierungsinformationen sind nicht akzeptabel.

    4. Wählen Sie **OK** zum Zurückgeben der **Eigenschaften der neuen Vorlage** Dialogfeld.

6. Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

    1. Wählen Sie **hinzufügen**.

    2. Auf der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** Dialogfeld Geben Sie **VPN-Server**, und wählen Sie dann **OK**.

    3. In **Gruppen-oder Benutzernamen**Option **VPN-Server**.

    4. In **Berechtigungen für die VPN-Server**, wählen die **registrieren** Kontrollkästchen in der **zulassen** Spalte.

    5. In **Gruppen-oder Benutzernamen**Option **RAS- und IAS-Server**, und wählen Sie dann **entfernen**.

7. Auf der **Antragstellername** Registerkarte, die folgenden Schritte ausführen:

    1. Wählen Sie **Geben Sie in der Anforderung**.

    2. Auf der **Zertifikatvorlagen** Warnung wählen Sie im Dialogfeld **OK**.

8. (Optional) Wenn Sie bedingten Zugriff für VPN-Verbindungen konfigurieren, wählen Sie die **Anforderungsverarbeitung** Registerkarte aus, und wählen Sie dann **privatem Schlüssel zulassen zu exportierenden**.

9. Wählen Sie **OK** um die Zertifikatvorlage für die VPN-Server zu speichern.

10. Schließen Sie die Zertifikatvorlagenkonsole.

11. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**Option **neu** und wählen Sie dann **Auszustellende Zertifikatvorlage**.

12. Wählen Sie den Namen, die Sie in Schritt 4 ausgewählt haben, und klicken Sie auf **OK**.

13. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="create-the-nps-server-authentication-template"></a>Erstellen Sie die Vorlage für die NPS-Server-Authentifizierung

Die dritte und letzte Zertifikatvorlage erstellen wird die Vorlage für die NPS-Server-Authentifizierung. Die Vorlage für die NPS-Server-Authentifizierung ist eine einfache Kopie der Vorlage RAS- und IAS-Server geschützt werden, um die NPS-Server-Gruppe, die Sie zuvor in diesem Abschnitt erstellt haben.

Konfigurieren Sie dieses Zertifikat für die automatische Registrierung.

**Vorgehensweise:**

1. Öffnen Sie auf der Zertifizierungsstelle Zertifizierungsstelle ein.

2. Klicken Sie im Navigationsbereich mit der Maustaste **Zertifikatvorlagen** , und wählen Sie **verwalten**.

3. In der Verwaltungskonsole Zertifikatvorlagen mit der Maustaste **RAS- und IAS-Server**, und wählen Sie **Doppelte Vorlage**.

4. Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage für die **allgemeine** Registerkarte **Vorlagenanzeigename**, Typ **NPS-Server-Authentifizierung**.

5. Auf der **Sicherheit** Registerkarte, die folgenden Schritte ausführen:

    1. Wählen Sie **hinzufügen**.

    2. Auf der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** Dialogfeld Geben Sie **NPS-Server**, und wählen Sie dann **OK**.

    3. In **Gruppen-oder Benutzernamen**Option **NPS-Server**.

    4. In **Berechtigungen für die NPS-Server**, wählen die **registrieren** und **automatisch registrieren** Kontrollkästchen in der **zulassen** Spalte.

    5. In **Gruppen-oder Benutzernamen**Option **RAS- und IAS-Server**, und wählen Sie dann **entfernen**.

6. Wählen Sie **OK** um die NPS-Server-Zertifikatvorlage zu speichern.

7. Schließen Sie die Zertifikatvorlagenkonsole.

8. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-in der Maustaste **Zertifikatvorlagen**Option **neu** und wählen Sie dann **Auszustellende Zertifikatvorlage**.

9. Wählen Sie **NPS-Server-Authentifizierung**, und wählen Sie **OK**.

10. Schließen Sie das Zertifizierungsstelle-Snap-in.

## <a name="enroll-and-validate-the-user-certificate"></a>Registrieren Sie und überprüfen Sie das Benutzerzertifikat

Da Sie die Gruppenrichtlinie, damit Benutzerzertifikate verwenden, müssen Sie nur die Richtlinie aktualisieren und Windows 10 wird automatisch das Benutzerkonto für das richtige Zertifikat registrieren. Sie können dann das Zertifikat in der Zertifikatkonsole überprüfen.

**Vorgehensweise:**

1. Melden Sie sich bei einer Domäne eingebundenen Client-Computer als Mitglied der **VPN-Benutzer** Gruppe.

2. Drücken Sie die Windows-Taste + R, Typ **Gpupdate/force**, und drücken Sie EINGABETASTE.

3. Geben Sie im Menü Start **"Certmgr.msc"** , und drücken Sie EINGABETASTE.

4. Klicken Sie in das Zertifikate-Snap-in unter **persönliche**Option **Zertifikate**. Die Zertifikate werden im Detailbereich angezeigt.

5. Mit der rechten Maustaste in des Zertifikats mit Ihrer aktuellen Domäne Benutzername ein, und wählen Sie dann **öffnen**.

6. Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Wenn sie nicht der Fall ist, haben Sie möglicherweise das falsche Zertifikat ausgewählt.

7. Wählen Sie **OK**, und schließen Sie das Zertifikate-Snap-in.

## <a name="enroll-and-validate-the-server-certificates"></a>Registrieren Sie und überprüfen Sie die Serverzertifikate

Im Gegensatz zu das Zertifikat müssen Sie das VPN-Zertifikat des Servers manuell registrieren. Nachdem sie registriert haben, überprüfen Sie sie durch die gleiche Weise wie für das Benutzerzertifikat. Wie das Benutzerzertifikat registriert der NPS-Server automatisch ein Clientauthentifizierungszertifikat, also alles, was Sie tun müssen sie überprüfen.

>[!NOTE]
>Sie müssen möglicherweise neu starten der VPN- und NPS-Server können sie Gruppenmitgliedschaften zu aktualisieren, bevor Sie diese Schritte ausführen können.

### <a name="enroll-and-validate-the-vpn-server-certificate"></a>Registrieren Sie und überprüfen Sie des VPN-Server-Zertifikats

1. Geben Sie auf das Menü "Start" die VPN-Server, **"certlm.msc"** , und drücken Sie EINGABETASTE.

2. Mit der rechten Maustaste **persönliche**Option **alle Aufgaben** und wählen Sie dann **neues Zertifikat anfordern** der Zertifikatregistrierungs-Assistent gestartet.

3. Wählen Sie auf der Seite Vorbemerkungen **Weiter**.

4. Wählen Sie auf der Seite Zertifikatregistrierungsrichtlinie auswählen **Weiter**.

5. Wählen Sie das Kontrollkästchen neben dem VPN-Server, um es auszuwählen, auf der Seite Zertifikate anfordern.

6. Wählen Sie das Kontrollkästchen VPN-Server **ist erforderlich, Weitere Informationen** zum Öffnen des Dialogfelds Eigenschaften des Zertifikats, und führen die folgenden Schritte aus:

    1. Wählen Sie die **Betreff** Registerkarte **allgemeiner Name** unter **Antragstellername**im **Typ**.

    2. Klicken Sie unter **Antragstellername**im **Wert**, geben Sie den Namen der externen Domänenclients verwendet, um die Verbindung zum VPN, z. B. vpn.contoso.com, und wählen Sie dann **hinzufügen**.

    3. Klicken Sie unter **alternativen Antragstellernamen**im **Typ**Option **DNS**.

    4. Klicken Sie unter **alternativen Antragstellernamen**im **Wert**, geben Sie alle Servernamen, die Clients verwenden, um mit dem VPN, z. B. eine Verbindung herstellen, vpn.contoso.com, Vpn, 132.64.86.2.

    5. Wählen Sie **hinzufügen** nach dem Eingeben der Namen der einzelnen.

    6. Wählen Sie **OK** Abschluss.

7. Wählen Sie **registrieren**.

8. Wählen Sie **Fertig stellen**.

9. Klicken Sie in das Zertifikate-Snap-in unter **persönliche**Option **Zertifikate**.
    
    Die aufgeführten Zertifikate werden im Detailbereich angezeigt.

10. Mit der rechten Maustaste in des Zertifikats mit der VPN-Server den Namen, und wählen Sie dann **öffnen**.

11. Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Falls nicht, können Sie nicht das richtige Zertifikat ausgewählt haben.

12. Auf der **Details** Registerkarte **Enhanced Key Usage**, und überprüfen Sie, ob **IP-Sicherheits-IKE, dazwischenliegend** und **Serverauthentifizierung** in der Liste angezeigt.

13. Wählen Sie **OK** um das Zertifikat zu schließen.

14. Schließen Sie das Zertifikate-Snap-in.

### <a name="validate-the-nps-server-certificate"></a>Überprüfen Sie die NPS-Serverzertifikats

1. Starten Sie den NPS-Server neu.

2. Geben Sie auf dem NPS-Server im Menü Start **"certlm.msc"** , und drücken Sie EINGABETASTE.

3. Klicken Sie in das Zertifikate-Snap-in unter **persönliche**Option **Zertifikate**.

    Die aufgeführten Zertifikate werden im Detailbereich angezeigt.

4. Mit der rechten Maustaste in des Zertifikats mit dem NPS-Server Namen, und wählen Sie dann **öffnen**.

5. Auf der **allgemeine** Registerkarte, zu bestätigen, dass das Datum unter aufgeführt **gültig ab** ist das aktuelle Datum. Falls nicht, können Sie nicht das richtige Zertifikat ausgewählt haben.

6. Wählen Sie **OK** um das Zertifikat zu schließen.

7. Schließen Sie das Zertifikate-Snap-in.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 3: Konfigurieren Sie die RAS-Server für Always On-VPN-](vpn-deploy-ras.md): In diesem Schritt konfigurieren Sie RAS-VPN IKEv2-VPN-Verbindungen zulassen, verweigern Verbindungen von anderen VPN-Protokolle und zuweisen einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zum Herstellen einer Verbindung autorisierte VPN-Clients.
