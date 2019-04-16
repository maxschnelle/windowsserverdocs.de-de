---
title: Konfigurieren der Serverinfrastruktur
description: In diesem Schritt installieren und Konfigurieren der serverseitigen Komponenten erforderlich, um die VPN-Unterstützung. Die serverseitige Komponenten umfassen konfigurieren PKI, um die vom Benutzer, der VPN-Server und dem Netzwerkrichtlinienserver verwendeten Zertifikate zu verteilen.
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067407"
---
# Schritt 2. Konfigurieren der Serverinfrastruktur

>Gilt für: WindowsServer (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Vorherigen:** Schritt 1. Planen der Always On VPN-Bereitstellung](always-on-vpn-deploy-planning.md)<br>
& #187;  [ **Weiter:** Schritt 3. Konfigurieren Sie den RAS-Server für immer auf VPN](vpn-deploy-ras.md)


In diesem Schritt installieren und Konfigurieren der serverseitigen Komponenten erforderlich, um die VPN-Unterstützung. Die serverseitige Komponenten umfassen konfigurieren PKI, um die vom Benutzer, der VPN-Server und dem Netzwerkrichtlinienserver verwendeten Zertifikate zu verteilen.  Außerdem konfigurieren Sie RRAS zur Unterstützung von IKEv2 Verbindungen und dem Netzwerkrichtlinienserver für die Autorisierung für die VPN-Verbindungen.

## Konfigurieren Sie die automatische Registrierung von Zertifikaten in "Gruppenrichtlinie"
In diesem Verfahren konfigurieren Sie Gruppenrichtlinien auf dem Domänencontroller so, dass Domänenmitglieder automatisch Benutzer- und Zertifikate anfordern. Auf diese Weise können VPN-Benutzer anfordern und Abrufen von Benutzerzertifikate, die VPN-Verbindungen automatisch zu authentifizieren. Ebenso kann diese Richtlinie NPS Server Server anfordern Authentifizierungszertifikate automatisch. 

Sie registrieren manuell Zertifikate auf VPN-Servern.

>[!TIP]
>Nicht domained verbundene Computer finden Sie unter folgenden [Zertifizierungsstellenkonfiguration für keiner Domäne eingebundene Computer](#ca-configuration-for-non-domain-joined-computers) . Seit der RRAS-Server nicht Domäne beigetreten ist, kann nicht automatische Registrierung verwendet werden, um das VPN-Gateway-Zertifikat zu registrieren.  Verwenden Sie daher ein Verfahren offline Zertifikats Anforderung. 


1.  Öffnen Sie auf einem Domänencontroller die Gruppenrichtlinien-Verwaltungskonsole.

2.  Klicken Sie im Navigationsbereich mit der rechten Maustaste Ihrer Domäne (z. B. corp.contoso.com), und klicken Sie auf**ein Gruppenrichtlinienobjekt in dieser Domäne erstellen und verknüpfen Sie es hier**.

3.  Klicken Sie im Dialogfeld Neues Gruppenrichtlinienobjekt Geben Sie **Die automatische Registrierung Policy**, und klicken Sie auf **OK**.

4.  Klicken Sie im Navigationsbereich mit der rechten Maustaste **Mit der Richtlinie**, und klicken Sie auf **Bearbeiten**.

5.  Führen Sie in den Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte aus, um Computerzertifikaten zu konfigurieren:

    1.  Klicken Sie im Navigationsbereich auf **Configuration\\Policies\\Windows Settings\\Security Settings\\Public Schlüssel Computerrichtlinien**.

    2.  Klicken Sie im Detailbereich mit der rechten Maustaste**Services Client – automatische Registrierung von Zertifikaten**, und klicken Sie auf **Eigenschaften**.

    3.  Klicken Sie auf die Zertifikatdienstclient – automatische Registrierung Eigenschaften im Dialogfeld **Konfigurationsmodell** **aktiviert**.

    4.  Wählen Sie**Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**, und**Aktualisieren Sie Zertifikate, die Zertifikatvorlagen verwenden**.

    5.  Klicken Sie auf**OK**.

6.  Führen Sie in den Gruppenrichtlinienverwaltungs-Editor, die folgenden Schritte zum Konfigurieren Benutzer zur automatischen Registrierung:

    1.  Klicken Sie im Navigationsbereich auf **Configuration\\Policies\\Windows Settings\\Security Settings\\Public Schlüssel Benutzerrichtlinien**.

    2.  Klicken Sie im Detailbereich mit der rechten Maustaste**Services Client – automatische Registrierung von Zertifikaten**, und klicken Sie auf **Eigenschaften**.

    3.  Klicken Sie auf die Zertifikatdienstclient – automatische Registrierung Eigenschaften im Dialogfeld **Konfigurationsmodell** **aktiviert**.

    4.  Wählen Sie**Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen**, und**Aktualisieren Sie Zertifikate, die Zertifikatvorlagen verwenden**.

    5.  Klicken Sie auf**OK**.

    6.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

7.  Schließen Group Policy Management.

### Zertifizierungsstellenkonfiguration für keiner Domäne verbundene Computer

Seit der RRAS-Server nicht Domäne beigetreten ist, kann nicht automatische Registrierung verwendet werden, um das VPN-Gateway-Zertifikat zu registrieren.  Verwenden Sie daher ein Verfahren offline Zertifikats Anforderung. 

1. Auf dem RRAS-Server generiert eine Datei namens **VPNGateway.inf** basierend auf der Beispiel-Zertifikat-Richtlinie anfordern in Anhang (Abschnitt 0) bereitgestellt und passen die folgenden Einträge: 

   - Ersetzen Sie im Abschnitt [NewRequest] vpn.contoso.com für den Antragstellernamen mit dem ausgewählten [_Kunden_] VPN-Endpunkt FQDN verwendet.

   - Ersetzen Sie im Abschnitt [Extensions] vpn.contoso.com für den alternativen Antragstellernamen mit dem ausgewählten [_Kunden_] VPN-Endpunkt FQDN verwendet.

2. Speichern Sie oder kopieren Sie die Datei **VPNGateway.inf** an einem ausgewählten Speicherort.

3. Ein Eingabeaufforderungsfenster mit erhöhten Rechten navigieren Sie zu dem Ordner, der die **VPNGateway.inf** Datei- und Typ enthält:

   ```
   certreq -new VPNGateway.inf VPNGateway.req
   ```

4. Kopieren Sie die neu erstellte **VPNGateway.req** Ausgabedatei in eine Zertifizierungsstelle Server oder privilegierten Zugriff Workstation (KRALLE). 

5. Speichern Sie oder kopieren Sie die Datei **VPNGateway.req** an einem ausgewählten Speicherort auf dem Zertifizierungsstelle Server oder privilegierten Zugriff Workstation (KRALLE).

6. Ein Eingabeaufforderungsfenster mit erhöhten Rechten navigieren Sie zu dem Ordner, der die im vorherigen Schritt und Typ erstellte VPNGateway.req-Datei enthält: 

   ```
   certreq -attrib “CertificateTemplate:[Customer]VPNGateway” -submit VPNgateway.req VPNgateway.cer
   ```

7. Wählen Sie ggf. vom Fenster Liste der entsprechenden Enterprise-Zertifizierungsstelle das Zertifikat-Anforderung.

8. Kopieren Sie die neu erstellte **VPNGateway.cer** Ausgabedatei zum RRAS-Server. 

9. Speichern Sie oder kopieren Sie die Datei **VPNGateway.cer** an einem ausgewählten Speicherort auf dem RRAS-Server.

10. Ein Eingabeaufforderungsfenster mit erhöhten Rechten navigieren Sie zu dem Ordner, der die im vorherigen Schritt und Typ erstellte VPNGateway.cer-Datei enthält:
   
   ```
   certreq -accept VPNGateway.cer
   ```

11. Führen Sie das Zertifikat-MMC-Snap-in, als beschriebenen [hier](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in) **Computerkonto** mit der Option.

12. Stellen Sie sicher, dass ein gültiges Zertifikat für den RRAS-Server mit den folgenden Eigenschaften vorhanden ist:

   - **Beabsichtigte Zwecke:** Server-Authentifizierung, IP-Sicherheit IKE intermediate 

   - **Zertifikaten Vorlage:** [_Kunden_] VPN-Server

#### Beispiel: VPNGateway.inf Skript

Hier sehen Sie ein Beispielskript einer Zertifikat-Anforderung-Richtlinie verwendet, um ein VPN-Gateway-Zertifikat mit einer Out-of-Band-Prozess anfordern.

>[!TIP]
>Eine Kopie des Skripts VPNGateway.inf finden Sie im VPN-Angebot IP-Kit im Ordner "" Zertifikat anfordern Richtlinien. Aktualisieren Sie nur die "Betreff" und "\_continue\_" mit Kunden bestimmte Werte.

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

## Erstellen der VPN-Benutzer, VPN-Servern und NPS-Servers-Gruppen

In diesem Verfahren können Sie eine neue Gruppe von Active Directory (AD) hinzufügen, die der Benutzer das VPN für die Verbindung mit dem Netzwerk Ihrer Organisation verwenden dürfen enthält.

Diese Gruppe dient zwei Zwecken:

-   Es definiert, automatisch registrieren für die Benutzerzertifikate berechtigten Benutzer, die das VPN erforderlich sind.

-   Es definiert, welche Benutzer die NPS für VPN-Zugriff autorisiert.

Verwenden Sie eine benutzerdefinierte Gruppe, wenn Sie ein Benutzer VPN-Zugriff, widerrufen möchten können Sie diesen Benutzer aus der Gruppe entfernen.

Fügen Sie auch eine Gruppe mit VPN-Server und eine andere Gruppe mit NPS-Servern. Verwenden Sie diese Gruppen, um zertifikatanforderungen für ihre Mitglieder zu beschränken.

>[!NOTE] 
>Wir empfehlen-VPN-Server, auf denen in der DMA/Perimeter befinden sich nicht Domäne. Jedoch, wenn Sie es vorziehen, haben die VPN-Server für eine bessere Verwaltbarkeit Domäne hinzufügen (Gruppenrichtlinien, Backup/Monitoring Agent, keine lokalen Benutzer verwalten und so weiter), dann eine AD-Gruppe für die VPN-Server-Zertifikatvorlage.

### Konfigurieren der VPN-Benutzergruppe

1.  Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und-Computer.

2.  Mit der rechten Maustaste ein Container oder die Organisationseinheit, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.

3.  **Gruppenname**Geben Sie **VPN-Benutzer**, und klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Benutzer**, und klicken Sie auf **Eigenschaften**.

5.  Klicken Sie auf der Registerkarte " **Mitglieder** " im Dialogfeld Eigenschaften von VPN-Benutzern auf **Hinzufügen**.

6.  Fügen Sie im Dialogfeld Benutzer auswählen aller Benutzer, die VPN benötigen Zugriff auf, und klicken Sie auf **OK**.

7.  Schließen Sie Active Directory-Benutzer und -Computer.

### Konfigurieren Sie die VPN-Server und Netzwerkrichtlinienserver Gruppen

1.  Öffnen Sie auf einem Domänencontroller Active Directory-Benutzer und-Computer.

2.  Mit der rechten Maustaste ein Container oder die Organisationseinheit, klicken Sie auf **neu** , und klicken Sie auf **Gruppe**.

3.  **Gruppenname**Geben Sie **VPN-Servern**, und klicken Sie auf **OK**.

4.  Mit der rechten Maustaste **VPN-Servern**, und klicken Sie auf **Eigenschaften**.

5.  Klicken Sie auf der Registerkarte " **Mitglieder** " im Dialogfeld Eigenschaften von VPN-Servern auf **Hinzufügen**.

6.  Klicken Sie auf **Objekttypen**, aktivieren Sie das Kontrollkästchen **Computer** , und klicken Sie auf **OK**.

7.  Klicken Sie im Feld **Geben Sie die zu verwendenden Objektnamen ein**Geben Sie die Namen Ihrer VPN-Server, und klicken Sie auf **OK**.

8.  Klicken Sie auf **OK** , um das Dialogfeld Eigenschaften von VPN-Servers zu schließen.

9.  Wiederholen Sie die vorherigen Schritten für die Gruppe NPS-Servern.

10. Schließen Sie Active Directory-Benutzer und -Computer.

## Erstellen Sie die Benutzerauthentifizierung-Vorlage

In diesem Verfahren konfigurieren Sie eine benutzerdefinierte Client / Server-Authentifizierung Vorlage. Diese Vorlage ist erforderlich, da das Zertifikat allgemeine Sicherheit verbessern, indem Sie aktualisierte Kompatibilität Ebenen werden soll und der Microsoft-Plattformkryptografieanbieter auswählen. Diese letzte Änderung können Sie das TPM auf den Clientcomputern verwenden, um das Zertifikat zu schützen. Eine Übersicht über das TPM finden Sie unter [Trusted Platform Module – Technologieübersicht](https://docs.microsoft.com/windows/device-security/tpm/trusted-platform-module-overview).

**Verfahren:**

1.  Öffnen Sie in der Zertifizierungsstelle Zertifizierungsstelle.

2.  Klicken Sie im Navigationsbereich mit der rechten Maustaste**Zertifikatvorlagen**, und klicken Sie auf**Verwalten**.

3.  In der Konsole Zertifikatvorlagen mit der rechten Maustaste**Benutzer**, und klicken Sie auf**Doppelte Vorlage**.

    >[!WARNING]
    >Klicken Sie zu einem beliebigen Zeitpunkt vor Schritt 10 nicht **Übernehmen** oder **OK** .  Wenn Sie diese Schaltflächen klicken, bevor Sie alle Parameter eingeben, werden viele Optionen fest und nicht mehr bearbeitet werden. Beispielsweise auf der Registerkarte " **Kryptografie** " _Legacy Kryptografieanbieter Speicher_ im Feld Anbieterkategorie zeigt es wird deaktiviert, verhindern, dass weitere ändern. Die einzige alternative ist die Vorlage zu löschen und neu erstellen.  

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage**Allgemeine**Registerkarte, führen Sie die folgenden Schritte aus:

    1.  Geben Sie im **Vorlagenanzeigename** **VPN-Authentifizierung**.

    2.  Deaktivieren Sie das Kontrollkästchen **Zertifikat in Active Directory veröffentlichen** .

5.  Auf die**Sicherheit**Registerkarte, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Auswählen von Benutzern, Computern, Dienstkonten oder Gruppen-Dialogfeld Geben Sie die **VPN-Benutzer**und klicken Sie auf **OK**.

    3.  **Gruppen-oder Benutzernamen**klicken Sie auf **VPN-Benutzer**.

    4.  Wählen Sie im **Berechtigungen für VPN-Benutzer**die **Registrieren** und **automatisch registrieren** Kontrollkästchen in der Spalte " **Zulassen** ".

       >[!TIP]
       >Stellen Sie sicher, dass das Lesen Kontrollkästchen aktiviert zu lassen. Anders ausgedrückt, benötigen Sie die Berechtigung zum Lesen, für die Registrierung. 

    5.  Klicken Sie in **Gruppen-oder Benutzernamen**auf **Domänenbenutzer**, und klicken Sie auf **Entfernen**.

6.  Führen Sie auf der Registerkarte " **Kompatibilität** " die folgenden Schritte aus:

    1.  Klicken Sie im **Zertifizierungsstellen**auf **Windows Server2012R2**.

    2.  Klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.

    3.  Klicken Sie im **Zertifikatempfänger**auf **Windows8.1/Windows Server2012R2**.

    4.  Klicken Sie im Dialogfeld **resultierende Änderungen** auf **OK**.

7.  Deaktivieren Sie auf der Registerkarte " **Anforderungsverarbeitung** " das Kontrollkästchen **Exportieren von privatem Schlüssel zulassen** .

8.  Führen Sie auf der Registerkarte " **Kryptografie** " die folgenden Schritte aus:

    1.  Klicken Sie in **Der Kategorie Provider**auf **Schlüsselspeicheranbieter**.

    2.  Klicken Sie auf **Anfragen müssen eine der folgenden Anbieter verwenden**.

    3.  Aktivieren Sie das Kontrollkästchen **Microsoft Plattformkryptografieanbieter** .

9.  Wenn Sie eine e-Mail-Adresse für alle Benutzerkonten besitzen, deaktivieren Sie auf der Registerkarte **Antragstellername** die Kontrollkästchen **Include e-Mail-Namen im Antragstellernamen** und **e-Mail-Namen** .

10. Klicken Sie auf**OK** , um die Zertifikatvorlage für die VPN-Authentifizierung zu speichern.

11. Schließen TheCertificate Vorlagen-Konsole.

12. Klicken Sie im Navigationsbereich des TheCertification Authoritysnap-in, mit der rechten Maustaste**Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf**Auszustellende Zertifikatvorlage**.

13. Klicken Sie auf**VPN-Benutzerauthentifizierung**, und klicken Sie auf**OK**.

14. Schließen Sie TheCertification Zertifizierungsstellen-Snap-in.

## Erstellen Sie die VPN-Serverauthentifizierung-Vorlage

In diesem Verfahren können Sie eine neue Vorlage für die Authentifizierung des Servers für den VPN-Server konfigurieren. Hinzufügen von, dass die IP-Sicherheit (IPsec) IKE Intermediate Anwendungsrichtlinie ermöglicht es dem Server zum Filtern von Zertifikaten, wenn mehr als ein Zertifikat für die Authentifizierung des Servers verfügbar ist, erweiterte Schlüsselverwendung.

>[!IMPORTANT] 
>Da VPN-Clients diese Server über das Internet zugreifen, sind die Betreff und alternative Namen anders als den internen Servernamen. Daher können Sie nicht automatisch registrieren dieses Zertifikat auf VPN-Servern.

**Voraussetzungen:**<p>
Domäne VPN-Servern

**Verfahren:** 

1.  Öffnen Sie in der Zertifizierungsstelle Zertifizierungsstelle.

2.  Klicken Sie im Navigationsbereich mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie auf**Verwalten**.

3.  In der Konsole Zertifikatvorlagen mit der rechten Maustaste**RAS- und IAS-Server**, und klicken Sie auf**Doppelte Vorlage**.

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage**Allgemeine**Registerkarte in **Vorlagenanzeigename**, geben Sie einen beschreibenden Namen für die VPN-Server, z. B. **VPN-Serverauthentifizierung** oder **RADIUS-Server**.

5.  Auf die**Erweiterungen**Registerkarte, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf**Anwendungsrichtlinien**, und klicken Sie auf**Bearbeiten**.

    2.  Das Dialogfeld **Anwendungsrichtlinien bearbeiten** klicken Sie auf**Hinzufügen**.

    3.  Klicken Sie im Dialogfeld **Anwendungsrichtlinie hinzufügen** auf **IP-Sicherheit IKE intermediate**, und klicken Sie auf **OK**.<p>Hinzufügen von IP-hilft Sicherheit IKE fortgeschrittene und der EKU in Szenarien, in denen mehrere Serverauthentifizierungszertifikat des VPN-Servers vorhanden ist. Wenn IP-Sicherheit IKE intermediate vorhanden ist, verwendet IPSec nur das Zertifikat mit beiden EKU-Optionen. Ohne diese fehlschlagen IKEv2 Authentifizierung mit Fehler 13801: IKE-Authentifizierungsinformationen werden nicht akzeptiert.

    4.  Klicken Sie auf **OK** , um die**Eigenschaften der neuen Vorlage**zurückzukehrenDialogfeld.

6.  Auf die**Sicherheit**Registerkarte, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Klicken Sie im Dialogfeld **Benutzer, Computer, Dienstkonten oder Gruppen** Geben Sie **VPN-Servern**, und klicken Sie auf **OK**.

    3.  **Gruppen-oder Benutzernamen**klicken Sie auf **VPN-Servern**.

    4.  **Berechtigungen für VPN-Servern**aktivieren Sie das Kontrollkästchen **Registrieren** , in der Spalte " **Zulassen** ".

    5.  Klicken Sie in **Gruppen-oder Benutzernamen**auf **RAS- und IAS-Server**, und klicken Sie auf **Entfernen**.

7.  Führen Sie auf der Registerkarte " **Antragstellername** " die folgenden Schritte aus:

    1.  Klicken Sie auf die **in der Anforderung angeben**.

    2.  Klicken Sie im Dialogfeld **Zertifikatvorlagen** Warnung klicken Sie auf **OK**.

8.  (Optional) *Wenn Sie bedingten Zugriff für VPN-Verbindung konfigurieren*, klicken Sie auf der Registerkarte " **Anforderungsverarbeitung** ", und klicken Sie auf **Exportieren von privatem Schlüssel zulassen** , um sie auszuwählen.

9.  Klicken Sie auf**OK** , um die Zertifikatvorlage für die VPN-Server zu speichern.

10. Schließen TheCertificate Vorlagen-Konsole.

11. Im Navigationsfenster die Zertifizierung Authoritysnap-in mit der rechten Maustaste**Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf**Auszustellende Zertifikatvorlage**.

12. Starten Sie die Zertifizierungsstelle Dienste neu.

13. Wählen Sie den Namen, die, den Sie oben in Schritt 4 ausgewählt haben, und klicken Sie auf**OK**.

14. Schließen Sie TheCertification Zertifizierungsstellen-Snap-in.

## Erstellen Sie die Vorlage NPS-Serverauthentifizierung

Die dritte und letzte Zertifikatvorlage erstellen ist die Serverauthentifizierung NPS-Vorlage. Die Serverauthentifizierung NPS-Vorlage ist eine einfache Kopie der Vorlage RAS- und IAS-Server geschützt, um die NPS-Server-Gruppe, die Sie zuvor in diesem Abschnitt erstellt haben. 

Konfigurieren Sie dieses Zertifikat für die automatische Registrierung.

**Verfahren:**

1.  Öffnen Sie in der Zertifizierungsstelle Zertifizierungsstelle.

2.  Klicken Sie im Navigationsbereich mit der rechten Maustaste **Zertifikatvorlagen**, und klicken Sie auf**Verwalten**.

3.  Klicken Sie in der Konsole Zertifikatvorlagen mit der rechten Maustaste**RAS- und IAS-Server**, und wählen Sie **Vorlage duplizieren**.

4.  Klicken Sie im Dialogfeld Eigenschaften der neuen Vorlage**Allgemeine**Registerkarte **Vorlagenanzeigename** **NPS-Serverauthentifizierung**geben.

5.  Auf die**Sicherheit**Registerkarte, führen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf **Hinzufügen**.

    2.  Klicken Sie im Dialogfeld **Benutzer, Computer, Dienstkonten oder Gruppen** Geben Sie **NPS-Servern**, und klicken Sie auf **OK**.

    3.  **Gruppen-oder Benutzernamen**klicken Sie auf **NPS-Servern**.

    4.  Wählen Sie im **Berechtigungen für NPS-Servern**die **Registrieren** und **automatisch registrieren** Kontrollkästchen in der Spalte " **Zulassen** ".

    5.  Klicken Sie in **Gruppen-oder Benutzernamen**auf **RAS- und IAS-Server**, und klicken Sie auf **Entfernen**.

6.  Klicken Sie auf**OK** , um die Zertifikatvorlage NPS-Servers zu speichern.

7.  Schließen TheCertificate Vorlagen-Konsole.

8.  Im Navigationsfenster die Zertifizierung Authoritysnap-in mit der rechten Maustaste**Zertifikatvorlagen**, klicken Sie auf **neu** , und klicken Sie dann auf**Auszustellende Zertifikatvorlage**.

9.  Klicken Sie auf**NPS-Serverauthentifizierung**, und klicken Sie auf**OK**.

10. Schließen Sie TheCertification Zertifizierungsstellen-Snap-in.

## Registrieren und das Zertifikat überprüfen

Da Sie die Gruppenrichtlinie, damit Benutzerzertifikate verwenden, müssen Sie nur die Richtlinie aktualisieren und Windows 10 wird automatisch das Benutzerkonto für das richtige Zertifikat registrieren. Sie können dann das Zertifikat in der Konsole Zertifikate zu überprüfen.

**Verfahren:**

1.  Melden Sie sich für einen Client Domäne als Mitglied der Gruppe **VPN-Benutzer** .

2.  Drücken Sie die Windows-Taste + R, **** Gpupdate/Force ein, und drücken Sie die EINGABETASTE.

3.  Das Menü "Start" Geben Sie **certmgr.msc ein**, und drücken Sie die EINGABETASTE.

4.  Klicken Sie im Zertifikate-Snap-in unter **Persönliche**, **Zertifikate**aus. Die Zertifikate werden im Detailbereich angezeigt.

5.  Mit der rechten Maustaste in des Zertifikats, das Ihre aktuellen Domänenbenutzername hat, und klicken Sie auf **Öffnen**.

6.  Auf der Registerkarte " **Allgemein** " Stellen Sie sicher, dass die aufgeführten unter **gültig ab** Datum heutige Datum ist. Wenn dies nicht der Fall ist, können Sie das falsche Zertifikat ausgewählt haben.

7.  Klicken Sie auf **OK**, und schließen Sie das Zertifikate-Snap-in.

## Registrieren Sie und überprüfen Sie die Server-Zertifikate

Im Gegensatz zu das Zertifikat müssen Sie der VPN-Server-Zertifikat manuell registrieren. Nachdem Sie es registriert haben, überprüfen sie mithilfe des gleichen Prozess, den Sie für das Zertifikat verwendet. Wie das Zertifikat registriert der Netzwerkrichtlinienserver automatisch seine-Authentifizierungszertifikat, daher ist alles, was Sie tun müssen sie überprüfen.

>[!NOTE] 
>Sie müssen möglicherweise neu starten der VPN- und NPS-Server, um ermöglicht es ihnen, ihre Gruppenmitgliedschaften zu aktualisieren, bevor Sie diese Schritte abgeschlossen werden können.

### Registrieren Sie und überprüfen Sie das VPN-Server-Zertifikat

1.  Der VPN-Server Menü "Start" Geben Sie **certlm.msc**, und drücken Sie die EINGABETASTE.

2.  Mit der rechten Maustaste **Persönliche**, klicken Sie auf **Alle Aufgaben** , und klicken Sie dann auf **Neues Zertifikat anfordern** , um den Zertifikat-Registrierungs-Assistenten zu starten.

3.  Klicken Sie auf der Seite Vorbereitung auf **Weiter**.

4.  Klicken Sie auf der Seite "Zertifikatregistrierungsrichtlinie auswählen" auf **Weiter**.

5.  Klicken Sie auf der Seite "Zertifikate anfordern" auf das Kontrollkästchen neben der VPN-Server, um es auszuwählen.

6.  Klicken Sie unter das Kontrollkästchen für den VPN-Server auf **Weitere Informationen erforderlich ist** , um das Dialogfeld Zertifikateigenschaften öffnen und schließen Sie die folgenden Schritte aus:

    1.  Klicken Sie auf der Registerkarte " **Betreff** ", klicken Sie auf **Allgemeiner Name** unter **Antragstellernamen**in **Typ**.

    2.  Geben Sie unter **Antragstellername** **Wert**den Namen der externen Domänenclients zum Verbinden mit dem VPN, z. B. vpn.contoso.com, und klicken Sie auf **Hinzufügen**.

    3.  Klicken Sie unter **Alternative Namen**, **Typ**auf **DNS**.

    4.  Geben Sie unter **Alternative Name** **Wert**, alle des Servers, mit denen Namen Clients für die Verbindung mit dem VPN, z. B. vpn.contoso.com, Vpn, 132.64.86.2 aus.

    5.  Klicken Sie nach der Eingabe jeder Name auf **Hinzufügen** .

    6.  Klicken Sie anschließend auf **OK**.

7.  Klicken Sie auf **Registrieren**.

8.  Klicken Sie auf **Fertig stellen**.

9.  Klicken Sie im Zertifikate-Snap-in unter **Persönliche**, **Zertifikate**aus.<p>Ihre aufgeführten Zertifikate werden im Detailbereich angezeigt.

10. Mit der rechten Maustaste in des Zertifikats, das der VPN-Server benannt sind, und klicken Sie auf **Öffnen**.

11. Auf der Registerkarte " **Allgemein** " Stellen Sie sicher, dass die aufgeführten unter **gültig ab** Datum heutige Datum ist. Falls nicht, können Sie das falsche Zertifikat ausgewählt haben.

12. Klicken Sie auf der Registerkarte " **Details** " auf **Erweiterte Schlüsselverwendung**, und stellen Sie sicher, dass die **IP-Sicherheit IKE intermediate** und **Server-Authentifizierung** in der Liste angezeigt.

13. Klicken Sie auf **OK** , um das Zertifikat zu schließen.

14. Schließen Sie das Zertifikate-Snap-in.

### Überprüfen der NPS-Serverzertifikats

1.  Neustarten des NPS-Servers.

2.  Der Netzwerkrichtlinienserver Menü "Start" Geben Sie **certlm.msc**, und drücken Sie die EINGABETASTE.

3.  Klicken Sie im Zertifikate-Snap-in unter **Persönliche**, **Zertifikate**aus.<p>Ihre aufgeführten Zertifikate werden im Detailbereich angezeigt.

4.  Mit der rechten Maustaste in des Zertifikats, das des Netzwerkrichtlinienservers benannt sind, und klicken Sie auf **Öffnen**.

5.  Auf der Registerkarte " **Allgemein** " Stellen Sie sicher, dass die aufgeführten unter **gültig ab** Datum heutige Datum ist. Falls nicht, können Sie das falsche Zertifikat ausgewählt haben.

6.  Klicken Sie auf **OK** , um das Zertifikat zu schließen.

7.  Schließen Sie das Zertifikate-Snap-in.

## Nächster Schritt
[Schritt 3. Konfigurieren des RAS-Servers für Always On VPN](vpn-deploy-ras.md): In diesem Schritt konfigurieren Sie Remote Access VPN für IKEv2-VPN-Verbindung zulassen, verweigern, die Verbindungen von anderen VPN-Protokolle und weisen Sie einen statischen IP-Adresspool für die Ausstellung von IP-Adressen zu verbinden autorisierte VPN-Clients.







---
