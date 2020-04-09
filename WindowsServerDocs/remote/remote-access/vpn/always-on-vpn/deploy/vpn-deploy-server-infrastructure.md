---
title: Konfigurieren der Server Infrastruktur
description: In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten, die zur Unterstützung des VPN erforderlich sind. Zu den serverseitigen Komponenten gehört das Konfigurieren der PKI für die Verteilung der Zertifikate, die von Benutzern, dem VPN-Server und dem NPS-Server verwendet werden.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 7c09ae7a792030152780ce4eb0029cea3ca234d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818923"
---
# <a name="step-2-configure-the-server-infrastructure"></a>Schritt 2 Konfigurieren der Serverinfrastruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorheriges:** Schritt 1: Planen der Always on VPN-Bereitstellung](always-on-vpn-deploy-planning.md)
- [**Weiter:** Schritt 3. Konfigurieren des Remote Zugriffs Servers für die Always on-VPN](vpn-deploy-ras.md)

In diesem Schritt installieren und konfigurieren Sie die serverseitigen Komponenten, die zur Unterstützung des VPN erforderlich sind. Zu den serverseitigen Komponenten gehört das Konfigurieren der PKI für die Verteilung der Zertifikate, die von Benutzern, dem VPN-Server und dem NPS-Server verwendet werden.  Außerdem konfigurieren Sie RRAS für die Unterstützung von IKEv2-Verbindungen und den NPS-Server zum Ausführen der Autorisierung für die VPN-Verbindungen.

## <a name="configure-certificate-autoenrollment-in-group-policy"></a>Konfigurieren der automatischen Zertifikat Registrierung in Gruppenrichtlinie
In diesem Verfahren konfigurieren Sie Gruppenrichtlinie auf dem Domänen Controller, damit Domänen Mitglieder automatisch Benutzer-und Computer Zertifikate anfordern. Auf diese Weise können VPN-Benutzer Benutzerzertifikate anfordern und abrufen, die VPN-Verbindungen automatisch authentifizieren. Ebenso ermöglicht diese Richtlinie NPS-Servern das automatische anfordern von Server Authentifizierungs Zertifikaten. 

Sie registrieren Zertifikate manuell auf VPN-Servern.

>[!TIP]
>Informationen zu nicht in Domänen eingebundenen Computern finden Sie unter Zertifizierungsstellen [Konfiguration für Computer, die keiner Domäne beigetreten](#ca-configuration-for-non-domain-joined-computers)sind. Da der RRAS-Server keiner Domäne beigetreten ist, kann die automatische Registrierung nicht zum Registrieren des VPN Gateway-Zertifikats verwendet werden.  Verwenden Sie daher eine Offline-Zertifikat Anforderungs Prozedur.

1. Öffnen Sie auf einem Domänen Controller Gruppenrichtlinie-Verwaltung.

2. Klicken Sie im Navigationsbereich mit der rechten Maustaste auf Ihre Domäne (z. b. Corp.contoso.com), und wählen Sie dann Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen aus**.

3. Geben Sie im Dialogfeld Neues Gruppenrichtlinien Objekt die **Richtlinie**für die automatische Registrierung ein, und klicken Sie dann auf **OK**.

4. Klicken Sie im Navigationsbereich mit der rechten Maustaste auf **Richtlinie**für die automatische Registrierung, und wählen Sie dann **Bearbeiten**aus.

5. Führen Sie im Gruppenrichtlinienverwaltungs-Editor die folgenden Schritte aus, um die automatische Registrierung von Computer Zertifikaten zu konfigurieren:

    1. Navigieren Sie im Navigationsbereich zu **Computer Konfiguration** > **Richtlinien** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Richtlinien für öffentliche Schlüssel**.

    2. Klicken Sie im Detailfenster mit der rechten Maustaste auf **Zertifikat Dienst Client – automatische**Registrierung, und wählen Sie dann **Eigenschaften**aus.

    3. Wählen Sie im Dialogfeld Zertifikat Dienst Client – Eigenschaften für automatische Registrierung unter **Konfigurations Modell**die **Option aktiviert**aus.

    4. Wählen Sie **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren** aus.

    5. Wählen Sie **OK**.

6. Führen Sie im Gruppenrichtlinienverwaltungs-Editor die folgenden Schritte aus, um die automatische Registrierung von Benutzer Zertifikaten zu konfigurieren:

    1. Navigieren Sie im Navigationsbereich zu **Benutzerkonfiguration** > **Richtlinien** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Richtlinien für öffentliche Schlüssel**.

    2. Klicken Sie im Detailbereich mit der rechten Maustaste auf **Zertifikatdienstclient - Automatische Registrierung**, und wählen Sie **Eigenschaften** aus.

    3. Wählen Sie im Dialogfeld Zertifikat Dienst Client – Eigenschaften für automatische Registrierung unter **Konfigurations Modell**die **Option aktiviert**aus.

    4. Wählen Sie **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** und **Zertifikate, die Zertifikatvorlagen verwenden, aktualisieren** aus.

    5. Wählen Sie **OK**.

    6. Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

7. Schließen Sie Gruppenrichtlinienverwaltung.

### <a name="ca-configuration-for-non-domain-joined-computers"></a>Zertifizierungsstellen Konfiguration für Computer, die keiner Domäne beigetreten sind

Da der RRAS-Server keiner Domäne beigetreten ist, kann die automatische Registrierung nicht zum Registrieren des VPN Gateway-Zertifikats verwendet werden.  Verwenden Sie daher eine Offline-Zertifikat Anforderungs Prozedur.

1. Generieren Sie auf dem RRAS-Server eine Datei mit dem Namen **vpngateway. inf** , die auf der in Anhang a (Abschnitt 0) bereitgestellten Beispiel Zertifikat Richtlinien Anforderung basiert, und passen Sie die folgenden Einträge an:

   - Ersetzen Sie im Abschnitt [newrequest] VPN.contoso.com, der für den Antragsteller Namen verwendet wird, durch den ausgewählten [_Customer_] VPN Endpoint-voll qualifizierten Namen.

   - Ersetzen Sie im Abschnitt [Extensions] VPN.contoso.com, das für den alternativen Antragsteller Namen verwendet wird, durch den ausgewählten [_Customer_] VPN Endpoint-voll qualifizierten Namen.

2. Speichern oder kopieren Sie die Datei " **vpngateway. inf** " an einen ausgewählten Speicherort.

3. Navigieren Sie an einer Eingabeaufforderung mit erhöhten Rechten zu dem Ordner, der die Datei " **vpngateway. inf** " enthält, und geben Sie Folgendes ein:

   ```
   certreq -new VPNGateway.inf VPNGateway.req
   ```

4. Kopieren Sie die neu erstellte **vpngateway. req** -Ausgabedatei auf einen Zertifizierungsstellen Server oder eine Arbeitsstation mit privilegiertem Zugriff (PW).

5. Speichern oder kopieren Sie die Datei " **vpngateway. req** " an einen ausgewählten Speicherort auf dem Zertifizierungsstellen Server oder auf der Arbeitsstation mit privilegiertem Zugriff (PW).

6. Navigieren Sie an einer Eingabeaufforderung mit erhöhten Rechten zu dem Ordner, der die im vorherigen Schritt erstellte vpngateway. req-Datei enthält, und geben Sie Folgendes ein:

   ```
   certreq -attrib "CertificateTemplate:[Customer]VPNGateway" -submit VPNgateway.req VPNgateway.cer
   ```

7. Wenn Sie im Fenster "Zertifizierungsstellen Liste" aufgefordert werden, wählen Sie die entsprechende Unternehmens Zertifizierungsstelle für die Zertifikat Anforderung aus.

8. Kopieren Sie die neu erstellte **vpngateway. CER** -Ausgabedatei auf den RRAS-Server. 

9. Speichern oder kopieren Sie die Datei " **vpngateway. CER** " an einen ausgewählten Speicherort auf dem RRAS-Server.

10. Navigieren Sie an einer Eingabeaufforderung mit erhöhten Rechten zu dem Ordner, der die im vorherigen Schritt erstellte vpngateway. CER-Datei enthält, und geben Sie Folgendes ein:

    ```
    certreq -accept VPNGateway.cer
    ```

11. Führen Sie das MMC-Snap-in "Zertifikate" aus, wie [hier](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in) beschrieben: Auswählen der Option **Computer Konto** .

12. Stellen Sie sicher, dass für den RRAS-Server ein gültiges Zertifikat mit den folgenden Eigenschaften vorhanden ist:

    - **Beabsichtigte Zwecke:** Server Authentifizierung, IP-Sicherheits-IKE-zwischen 

    - **Zertifikat Vorlage:** [_Customer_] VPN-Server

#### <a name="example-vpngatewayinf-script"></a>Beispiel: vpngateway. inf-Skript

Hier sehen Sie ein Beispielskript für eine Richtlinie für Zertifikat Anforderungen, die verwendet wird, um ein VPN-Gatewayzertifikat mithilfe eines Out-of-Band-Prozesses anzufordern.

>[!TIP]
>Eine Kopie des Skripts vpngateway. inf finden Sie im IP-Kit für VPN-Angebote unter dem Ordner Zertifikat Anforderungs Richtlinien. Aktualisieren Sie nur "Subject" und "\_Continue\_" mit kundenspezifischen Werten.

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

## <a name="create-the-vpn-users-vpn-servers-and-nps-servers-groups"></a>Erstellen der Gruppen VPN-Benutzer, VPN-Server und NPS-Server

In diesem Verfahren können Sie eine neue Active Directory (AD)-Gruppe hinzufügen, die die Benutzer enthält, die das VPN verwenden dürfen, um eine Verbindung mit Ihrem Organisations Netzwerk herzustellen.

Diese Gruppe dient zwei Zwecken:

- Es definiert, welche Benutzer die automatische Registrierung für die für das VPN erforderlichen Benutzerzertifikate durchführen dürfen.

- Es definiert, welche Benutzer der NPS für den VPN-Zugriff autorisiert.

Wenn Sie mit einer benutzerdefinierten Gruppe den VPN-Zugriff eines Benutzers widerrufen möchten, können Sie diesen Benutzer aus der Gruppe entfernen.

Außerdem fügen Sie eine Gruppe hinzu, die VPN-Server und eine andere Gruppe mit NPS-Servern enthält. Sie verwenden diese Gruppen, um Zertifikat Anforderungen auf ihre Mitglieder einzuschränken.

>[!NOTE]
>Wir empfehlen, dass VPN-Server, die sich im DMA/Umkreis befinden, nicht in die Domäne aufgenommen werden. Wenn Sie jedoch bevorzugen, dass die VPN-Server der Domäne beitreten, um eine bessere Verwaltbarkeit zu erzielen (Gruppenrichtlinien, Sicherungs-/Überwachungs-Agent, keine lokalen Benutzer zu verwalten usw.), fügen Sie der VPN-Serverzertifikat Vorlage eine Ad-Gruppe hinzu.

### <a name="configure-the-vpn-users-group"></a>Konfigurieren der Gruppe "VPN-Benutzer"

1. Öffnen Sie auf einem Domänen Controller Active Directory Benutzer und Computer.

2. Klicken Sie mit der rechten Maustaste auf einen Container oder eine Organisationseinheit, und wählen Sie **neu**und dann **Gruppe**aus.

3. Geben Sie unter **Gruppenname den Namen** **VPN-Benutzer**ein, und klicken Sie auf **OK**.

4. Klicken Sie mit der rechten Maustaste auf **VPN-Benutzer** und wählen Sie **Eigenschaften**

5. Wählen Sie im Dialogfeld Eigenschaften von VPN-Benutzer auf der Registerkarte **Mitglieder** die Option **Hinzufügen**aus.

6. Fügen Sie im Dialogfeld Benutzer auswählen alle Benutzer hinzu, die VPN-Zugriff benötigen, und wählen Sie **OK**aus.

7. Schließen Sie Active Directory-Benutzer und -Computer.

### <a name="configure-the-vpn-servers-and-nps-servers-groups"></a>Konfigurieren der VPN-Server und NPS-Server Gruppen

1. Öffnen Sie auf einem Domänen Controller Active Directory Benutzer und Computer.

2. Klicken Sie mit der rechten Maustaste auf einen Container oder eine Organisationseinheit, und wählen Sie **neu**und dann **Gruppe**aus.

3. Geben Sie unter **Gruppenname den Namen** **VPN-Server**ein, und klicken Sie auf **OK**.

4. Klicken Sie mit der rechten Maustaste auf **VPN-Server** und wählen Sie **Eigenschaften**

5. Wählen Sie im Dialogfeld Eigenschaften von VPN-Server auf der Registerkarte **Mitglieder** die Option **Hinzufügen**aus.

6. Wählen Sie **Objekttypen**aus, aktivieren Sie das Kontrollkästchen **Computer** , und klicken Sie dann auf **OK**.

7. Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein die Namen Ihrer VPN-Server ein, und klicken Sie dann auf **OK**.

8. Wählen Sie **OK** aus, um das Dialogfeld VPN-Server Eigenschaften zu schließen.

9. Wiederholen Sie die vorherigen Schritte für die NPS-Server Gruppe.

10. Schließen Sie Active Directory-Benutzer und -Computer.

## <a name="create-the-user-authentication-template"></a>Erstellen der Benutzer Authentifizierungs Vorlage

In diesem Verfahren konfigurieren Sie eine benutzerdefinierte Client-Server-Authentifizierungs Vorlage. Diese Vorlage ist erforderlich, da Sie die Gesamtsicherheit des Zertifikats verbessern möchten, indem Sie aktualisierte Kompatibilitäts Grade auswählen und den Kryptografieanbieter der Microsoft-Plattform auswählen. Mit dieser letzten Änderung können Sie das TPM auf den Client Computern zum Sichern des Zertifikats verwenden. Eine Übersicht über das TPM finden Sie unter [Übersicht](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview)über die Trusted Platform Module-Technologie.

>[!IMPORTANT] 
>Der Kryptografieanbieter für Microsoft-Plattformen erfordert einen TPM-Chip, falls Sie einen virtuellen Computer ausführen, und Sie erhalten die folgende Fehlermeldung: "Es wurde kein gültiger CSP auf dem lokalen Computer gefunden". Wenn Sie versuchen, das Zertifikat manuell zu registrieren, müssen Sie "Microsoft Software Key Storage" prüfen. Anbieter "und nach" der Microsoft-Plattform-Kryptografieanbieter "auf der Registerkarte" Kryptografie "in den Zertifikat Eigenschaften.

**Dringlichkeit**

1. Öffnen Sie auf der Zertifizierungsstelle die Zertifizierungsstelle.

2. Klicken Sie im Navigationsbereich mit der rechten Maustaste auf **Zertifikat Vorlagen** , und wählen Sie **Verwalten**aus.

3. Klicken Sie in der Konsole Zertifikat Vorlagen mit der rechten Maustaste auf **Benutzer** , und wählen Sie **Doppelte Vorlage**aus.

   >[!WARNING]
   >Wählen Sie vor Schritt 10 nicht **anwenden** oder **OK** aus.  Wenn Sie diese Schaltflächen vor dem Eingeben aller Parameter auswählen, werden viele Optionen korrigiert und können nicht mehr bearbeitet werden. Wenn z. b. auf der Registerkarte **Cryptography** der _Legacy-Kryptografiespeicheranbieter_ im Feld Anbieter Kategorie angezeigt wird, wird dieser deaktiviert und verhindert weitere Änderungen. Die einzige Alternative besteht darin, die Vorlage zu löschen und neu zu erstellen.  

4. Führen Sie im Dialogfeld Eigenschaften der neuen Vorlage auf der Registerkarte **Allgemein** die folgenden Schritte aus:

   1. Geben Sie unter **Vorlagen Anzeige Name den Namen** **VPN-Benutzerauthentifizierung**ein.

   2. Deaktivieren Sie das Kontrollkästchen **Zertifikat in Active Directory veröffentlichen** .

5. Führen Sie auf der Registerkarte **Sicherheit** die folgenden Schritte aus:

   1. Wählen Sie **Hinzufügen**.

   2. Geben Sie im Dialogfeld Benutzer, Computer, Dienst Konten oder Gruppen auswählen die Option **VPN-Benutzer**ein, und klicken Sie dann auf **OK**.

   3. Wählen Sie unter **Gruppen-oder Benutzernamen**die Option **VPN-Benutzer**aus.

   4. Aktivieren Sie in **Berechtigungen für VPN-Benutzer**in der Spalte **zulassen** die Kontroll **Kästchen registrieren und** **automatisch registrieren** .

      >[!TIP]
      >Stellen Sie sicher, dass das Kontrollkästchen Lesen aktiviert ist. Anders ausgedrückt: Sie benötigen die Leseberechtigungen für die Registrierung. 

   5. Klicken Sie unter **Gruppen-oder Benutzernamen**auf **Domänen Benutzer**, und wählen Sie dann **Entfernen**aus.

6. Führen Sie auf der Registerkarte **Kompatibilität** die folgenden Schritte aus:

   1. Wählen Sie unter **Zertifizierungs**Stelle die Option **Windows Server 2012 R2**aus.

   2. Klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.

   3. Wählen Sie unter **Zertifikat Empfänger**den Eintrag **Windows 8.1/Windows Server 2012 R2**aus.

   4. Klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.

7. Deaktivieren Sie auf der Registerkarte **Anforderungs Verarbeitung** das Kontrollkästchen **Exportieren von privatem Schlüssel zulassen** .

8. Führen Sie auf der Registerkarte **Cryptography** die folgenden Schritte aus:

   1. Wählen Sie unter **Anbieter Kategorie**die Option **Schlüsselspeicher Anbieter**aus.

   2. Für SELECT- **Anforderungen muss einer der folgenden Anbieter verwendet**werden.

   3. Aktivieren Sie das Kontrollkästchen **Kryptografieanbieter für Microsoft-Plattform** .

9. Wenn Sie auf der Registerkarte Antragsteller **Name** keine e-Mail-Adresse für alle Benutzerkonten aufgelistet haben, deaktivieren Sie die Kontrollkästchen **e-Mail-Name in** Antragsteller Name und **e-Mail-Name** einschließen.

10. Wählen Sie **OK** aus, um die Zertifikat Vorlage VPN-Benutzerauthentifizierung zu speichern.

11. Schließen Sie die Zertifikatvorlagenkonsole.

12. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-Ins mit der rechten Maustaste auf **Zertifikat Vorlagen**, wählen Sie **neu** und dann auszustellende **Zertifikat Vorlage**aus.

13. Wählen Sie **VPN-Benutzerauthentifizierung**, und klicken Sie dann auf **OK**.

14. Schließen Sie das Snap-in "Zertifizierungsstelle".

## <a name="create-the-vpn-server-authentication-template"></a>Erstellen der Vorlage für die VPN-Server Authentifizierung

In diesem Verfahren können Sie eine neue Server Authentifizierungs Vorlage für den VPN-Server konfigurieren. Durch das Hinzufügen der IPSec-IKE-zwischen Anwendungs Richtlinie (IP Security, IPSec) kann der Server Zertifikate filtern, wenn mehr als ein Zertifikat mit der erweiterten Schlüssel Verwendung der Server Authentifizierung verfügbar ist.

>[!IMPORTANT]
>Da VPN-Clients über das öffentliche Internet auf diesen Server zugreifen, unterscheiden sich die Antragsteller Namen und alternativen Namen von dem internen Servernamen. Daher können Sie dieses Zertifikat nicht automatisch auf VPN-Servern registrieren.

**Voraussetzung**

In die Domäne eingebundenen VPN-Servern

**Dringlichkeit**

1. Öffnen Sie auf der Zertifizierungsstelle die Zertifizierungsstelle.

2. Klicken Sie im Navigationsbereich mit der rechten Maustaste auf **Zertifikat Vorlagen** , und wählen Sie **Verwalten**aus.

3. Klicken Sie in der Konsole Zertifikat Vorlagen mit der rechten Maustaste auf **RAS-und IAS-Server** , und wählen Sie **Doppelte Vorlage**.

4. Geben Sie im Dialogfeld Eigenschaften der neuen Vorlage auf der Registerkarte **Allgemein** unter **Vorlagen Anzeige Name**einen beschreibenden Namen für den VPN-Server ein, z. b. **VPN-Server Authentifizierung** oder **RADIUS-Server**.

5. Führen Sie auf der Registerkarte **Erweiterungen** die folgenden Schritte aus:

    1. Wählen Sie **Anwendungsrichtlinien**und dann **Bearbeiten**aus.

    2. Wählen Sie im Dialogfeld **Anwendungsrichtlinien Erweiterung bearbeiten** die Option **Hinzufügen**aus.

    3. Wählen Sie im Dialogfeld **Anwendungs Richtlinie hinzufügen** die Option **IP-Sicherheit IKE zwischen**aus, und klicken Sie dann auf **OK**.
   
        Das Hinzufügen der IP-Sicherheits-IKE Intermediate zur EKU unterstützt Szenarien, in denen mehrere Server Authentifizierungs Zertifikate auf dem VPN-Server vorhanden sind. Wenn IP-Sicherheits-IKE Intermediate vorhanden ist, verwendet IPSec nur das Zertifikat mit beiden EKU-Optionen. Andernfalls kann die IKEv2-Authentifizierung mit Fehler 13801 fehlschlagen: die Anmelde Informationen für die IKE-Authentifizierung sind nicht zulässig.

    4. Wählen Sie **OK** aus, um zum Dialogfeld **Eigenschaften der neuen Vorlage** zurückzukehren.

6. Führen Sie auf der Registerkarte **Sicherheit** die folgenden Schritte aus:

    1. Wählen Sie **Hinzufügen**.

    2. Geben Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** die Option **VPN-Server**ein, und klicken Sie dann auf **OK**.

    3. Wählen Sie unter **Gruppen-oder Benutzernamen**die Option **VPN-Server**aus.

    4. Aktivieren Sie in **Berechtigungen für VPN-Server**in der Spalte **zulassen** das Kontrollkästchen **registrieren** .

    5. Wählen Sie unter **Gruppen-oder Benutzernamen** **RAS-und IAS-Server**aus, und klicken Sie dann auf **Entfernen**.

7. Führen Sie auf der Registerkarte Antragsteller **Name** die folgenden Schritte aus:

    1. Wählen Sie **in der Anforderung bereitstellen aus**.

    2. Wählen Sie im Dialogfeld **Zertifikat Vorlagen** Warnung die Option **OK**aus.

8. Optionale Wenn Sie den bedingten Zugriff für VPN-Konnektivität konfigurieren, klicken Sie auf die Registerkarte **Anforderungs Verarbeitung** , und wählen Sie dann die Option **zum Exportieren von privatem Schlüssel zulassen**aus.

9. Wählen Sie **OK** aus, um die VPN-Server Zertifikat Vorlage zu speichern.

10. Schließen Sie die Zertifikatvorlagenkonsole.

11. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-Ins mit der rechten Maustaste auf **Zertifikat Vorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf Auszustellende **Zertifikat Vorlage**.

12. Starten Sie die Zertifizierungsstellen Dienste neu. (*)

13. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-Ins mit der rechten Maustaste auf **Zertifikat Vorlagen**, wählen Sie **neu** und dann auszustellende **Zertifikat Vorlage**aus.

14. Wählen Sie den Namen aus Schritt 4 oben aus, und klicken Sie auf **OK**.

15. Schließen Sie das Snap-in "Zertifizierungsstelle".

* **Sie können den Zertifizierungsstellen Dienst durch Ausführen des folgenden Befehls in cmd Abbrechen/starten:**

```
Net Stop "certsvc"
Net Start "certsvc"
```

## <a name="create-the-nps-server-authentication-template"></a>Erstellen der NPS-Server Authentifizierungs Vorlage

Die dritte und letzte zu Erstell Bare Zertifikat Vorlage ist die NPS-Server Authentifizierungs Vorlage. Die NPS-Server Authentifizierungs Vorlage ist eine einfache Kopie der RAS-und IAS-Server Vorlage, die für die NPS-Server Gruppe gesichert ist, die Sie zuvor in diesem Abschnitt erstellt haben.

Dieses Zertifikat wird für die automatische Registrierung konfiguriert.

**Dringlichkeit**

1. Öffnen Sie auf der Zertifizierungsstelle die Zertifizierungsstelle.

2. Klicken Sie im Navigationsbereich mit der rechten Maustaste auf **Zertifikat Vorlagen** , und wählen Sie **Verwalten**aus.

3. Klicken Sie in der Konsole Zertifikat Vorlagen mit der rechten Maustaste auf **RAS-und IAS-Server**, und wählen Sie **Doppelte Vorlage**aus.

4. Geben Sie im Dialogfeld Eigenschaften der neuen Vorlage auf der Registerkarte **Allgemein** unter **Vorlagen Anzeige Name**den Namen **NPS-Server Authentifizierung**ein.

5. Führen Sie auf der Registerkarte **Sicherheit** die folgenden Schritte aus:

    1. Wählen Sie **Hinzufügen**.

    2. Geben Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** die **NPS-Server**ein, und klicken Sie dann auf **OK**.

    3. Wählen Sie unter **Gruppen-oder Benutzernamen**die Option **NPS-Server**aus.

    4. Aktivieren Sie in **Berechtigungen für NPS-Server**in der Spalte **zulassen** die Kontroll **Kästchen registrieren und** **automatisch registrieren** .

    5. Wählen Sie unter **Gruppen-oder Benutzernamen** **RAS-und IAS-Server**aus, und klicken Sie dann auf **Entfernen**.

6. Wählen Sie **OK** aus, um die NPS-Server Zertifikat Vorlage zu speichern.

7. Schließen Sie die Zertifikatvorlagenkonsole.

8. Klicken Sie im Navigationsbereich des Zertifizierungsstellen-Snap-Ins mit der rechten Maustaste auf **Zertifikat Vorlagen**, wählen Sie **neu** und dann auszustellende **Zertifikat Vorlage**aus.

9. Wählen Sie **NPS-Server Authentifizierung**aus, und klicken Sie auf **OK**.

10. Schließen Sie das Snap-in "Zertifizierungsstelle".

## <a name="enroll-and-validate-the-user-certificate"></a>Registrieren und Validieren des Benutzer Zertifikats

Da Sie Gruppenrichtlinie für die automatische Registrierung von Benutzer Zertifikaten verwenden, müssen Sie die Richtlinie nur aktualisieren, und Windows 10 registriert automatisch das Benutzerkonto für das korrekte Zertifikat. Anschließend können Sie das Zertifikat in der Zertifikat Konsole überprüfen.

**Dringlichkeit**

1. Melden Sie sich bei einem in die Domäne eingebundenen Client Computer als Mitglied der Gruppe " **VPN-Benutzer** " an.

2. Drücken Sie Windows-Taste + R, geben Sie **gpupdate/force**ein, und drücken Sie die EINGABETASTE.

3. Geben Sie im Menü Start den Befehl **Certmgr. msc**ein, und drücken Sie die EINGABETASTE.

4. Wählen Sie im Zertifikate-Snap-in unter **persönlich**die Option **Zertifikate**aus. Die Zertifikate werden im Bereich Details angezeigt.

5. Klicken Sie mit der rechten Maustaste auf das Zertifikat mit Ihrem aktuellen Domänen Benutzernamen, und wählen Sie dann **Öffnen**aus.

6. Vergewissern Sie sich auf der Registerkarte **Allgemein** , dass das Datum unter **gültig ab** das heutige Datum ist. Wenn dies nicht der Fall ist, haben Sie möglicherweise das falsche Zertifikat ausgewählt.

7. Wählen Sie **OK**aus, und schließen Sie das Snap-in Zertifikate.

## <a name="enroll-and-validate-the-server-certificates"></a>Registrieren und Validieren der Server Zertifikate

Im Gegensatz zum Benutzerzertifikat müssen Sie das Zertifikat des VPN-Servers manuell registrieren. Nachdem Sie diese registriert haben, überprüfen Sie Sie mithilfe desselben Prozesses, den Sie für das Benutzerzertifikat verwendet haben. Ebenso wie das Benutzerzertifikat registriert der NPS-Server automatisch sein Authentifizierungszertifikat, sodass Sie es nur überprüfen müssen.

>[!NOTE]
>Möglicherweise müssen Sie die VPN-und NPS-Server neu starten, damit Sie Ihre Gruppenmitgliedschaften aktualisieren können, bevor Sie diese Schritte ausführen können.

### <a name="enroll-and-validate-the-vpn-server-certificate"></a>Registrieren und Validieren des VPN-Serverzertifikats

1. Geben Sie im Startmenü des VPN-Servers **certlm. msc**ein, und drücken Sie die EINGABETASTE.

2. Klicken Sie mit der rechten Maustaste auf **persönlich**, wählen Sie **alle Aufgaben** aus, und wählen Sie dann **Neues Zertifikat anfordern** , um den Zertifikatregistrierungs-Assistenten

3. Wählen Sie auf der Seite Vorbereitung die Option **weiter**aus.

4. Wählen Sie auf der Seite Zertifikat Registrierungs Richtlinie auswählen die Option **weiter**aus.

5. Aktivieren Sie auf der Seite Zertifikate anfordern das Kontrollkästchen neben dem VPN-Server, um es auszuwählen.

6. Wählen Sie unter dem Kontrollkästchen VPN-Server die Option **Weitere Informationen sind erforderlich** aus, um das Dialogfeld Zertifikat Eigenschaften zu öffnen, und führen Sie die folgenden Schritte aus:

    1. Wählen Sie die Registerkarte **Betreff** aus, und wählen Sie unter Antragsteller **Name**die Option allgemeiner **Name** in **Typ**.

    2. Geben Sie unter Antragsteller **Name**unter **Wert**den Namen der externen Domänen Clients ein, die für die Verbindung mit dem VPN verwendet werden, z. b. VPN.contoso.com, und klicken Sie dann auf **Hinzufügen**.

    3. Wählen Sie unter **alternativer Name**in **Typ**die Option **DNS**aus.

    4. Geben Sie unter **alternativer Name**unter **Wert**den Namen aller Servernamen ein, die von Clients zum Herstellen einer Verbindung mit dem VPN verwendet werden, z. b. VPN.contoso.com, VPN, 132.64.86.2.

    5. Wählen Sie nach Eingabe der einzelnen Namen **Hinzufügen** aus.

    6. Klicken Sie abschließend auf **OK** .

7. Wählen Sie **Anmelden**aus.

8. Wählen Sie **Fertig stellen** aus.

9. Wählen Sie im Zertifikate-Snap-in unter **persönlich**die Option **Zertifikate**aus.
    
    Die aufgelisteten Zertifikate werden im Bereich Details angezeigt.

10. Klicken Sie mit der rechten Maustaste auf das Zertifikat mit dem Namen des VPN-Servers, und wählen Sie dann **Öffnen**aus.

11. Vergewissern Sie sich auf der Registerkarte **Allgemein** , dass das Datum unter **gültig ab** das heutige Datum ist. Wenn dies nicht der Fall ist, haben Sie möglicherweise das falsche Zertifikat ausgewählt.

12. Wählen Sie auf der Registerkarte **Details** die Option **Erweiterte Schlüssel Verwendung**aus, und überprüfen Sie, ob **IP-Sicherheits-IKE zwischen** und **Server Authentifizierung** in der Liste angezeigt werden

13. Wählen Sie **OK** aus, um das Zertifikat zu schließen.

14. Schließen Sie das Snap-In Zertifikate.

### <a name="validate-the-nps-server-certificate"></a>Validieren des NPS-Serverzertifikats

1. Starten Sie den NPS-Server neu.

2. Geben Sie im Startmenü des NPS-Servers **certlm. msc**ein, und drücken Sie die EINGABETASTE.

3. Wählen Sie im Zertifikate-Snap-in unter **persönlich**die Option **Zertifikate**aus.

    Die aufgelisteten Zertifikate werden im Bereich Details angezeigt.

4. Klicken Sie mit der rechten Maustaste auf das Zertifikat mit dem Namen des NPS-Servers, und wählen Sie dann **Öffnen**aus.

5. Vergewissern Sie sich auf der Registerkarte **Allgemein** , dass das Datum unter **gültig ab** das heutige Datum ist. Wenn dies nicht der Fall ist, haben Sie möglicherweise das falsche Zertifikat ausgewählt.

6. Wählen Sie **OK** aus, um das Zertifikat zu schließen.

7. Schließen Sie das Snap-In Zertifikate.

## <a name="next-steps"></a>Nächste Schritte

[Schritt 3. Konfigurieren des RAS-Servers für Always on VPN](vpn-deploy-ras.md): in diesem Schritt konfigurieren Sie das RAS-VPN, um IKEv2-VPN-Verbindungen zuzulassen, Verbindungen von anderen VPN-Protokollen zu verweigern und einen statischen IP-Adresspool für die Ausstellung von IP-Adressen für die Verbindung mit autorisierten VPN-Clients zuzuweisen.
