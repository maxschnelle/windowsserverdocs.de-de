---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: 'Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bd21f2d6e8dcb167aa2c614d096807305a7728d6
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188887"
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen




## <a name="about-this-guide"></a>Informationen zum Handbuch
Diese exemplarische Vorgehensweise enthält Anweisungen zum Konfigurieren von Multi-Factor Authentication (MFA) in Active Directory Federation Services (AD FS) in Windows Server 2012 R2-basierten auf Gruppenmitgliedschaftsdaten des Benutzers.

Weitere Informationen zur MFA und Authentifizierungsmechanismen in AD FS finden Sie unter [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).

Die exemplarische Vorgehensweise enthält die folgenden Abschnitte:

-   [Schritt 1: Einrichten der testumgebung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Schritt 2: Überprüfen des Standardmechanismus für AD FS-Authentifizierung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [Schritt 3: Konfigurieren der mehrstufigen Authentifizierung auf dem Verbundserver](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [Schritt 4: Überprüfen des MFA-Mechanismus](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="BKMK_1"></a>Schritt 1: Einrichten der Testumgebung
Damit die exemplarische Vorgehensweise abgeschlossen werden kann, benötigen Sie eine Umgebung mit den folgenden Komponenten:

-   Active Directory-Domäne mit einem Testbenutzer und testgruppenkonten unter Windows Server 2012 R2 oder Active Directory-Domäne unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 mit einem Schema, das ein Upgrade auf Windows Server 2012 R2

-   Verbundserver unter Windows Server 2012 R2

-   Webserver, auf dem die Beispielanwendung gehostet wird

-   Clientcomputer, über den Sie auf die Beispielanwendung zugreifen können

> [!WARNING]
> Es wird (sowohl in Produktions- als auch in Testumgebungen) dringend empfohlen, nicht denselben Computer für den Verbundserver und den Webserver zu verwenden.

In dieser Umgebung gibt der Verbundserver die erforderlichen Ansprüche aus, sodass Benutzer auf die Beispielanwendung zugreifen können. Auf dem Webserver wird eine Beispielanwendung gehostet, die den Benutzern vertraut, die die vom Verbundserver ausgestellten Ansprüche vorweisen.

Anweisungen zum Einrichten dieser Umgebung finden Sie [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

## <a name="BKMK_2"></a>Schritt 2: Überprüfen des Standardmechanismus für die AD FS-Authentifizierung
In diesem Schritt überprüfen Sie den Standardmechanismus für die AD FS-Zugriffssteuerung (**Formularauthentifizierung** für das Extranet und **Windows-Authentifizierung** für das Intranet), bei dem der Benutzer auf die AD FS-Anmeldeseite umgeleitet wird, gültige Anmeldeinformationen eingibt und Zugriff auf die Anwendung erhält. Können Sie die **Robert Hatley** AD-Konto und die **Claimapp** beispielanwendung, die Sie in konfiguriert [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Mit dieser Aktion wird die Anforderung automatisch an den Verbundserver umgeleitet, und Sie werden zur Anmeldung mit einem Benutzernamen und einem Kennwort aufgefordert.

2.  Geben Sie die Anmeldeinformationen der **Robert Hatley** AD-Konto, das Sie in erstellt [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Ihnen wird der Zugriff auf die Anwendung gewährt.

## <a name="BKMK_3"></a>Schritt 3: Konfigurieren der mehrstufigen Authentifizierung auf dem Verbundserver
Es gibt zwei Teile, die Konfiguration der MFA in AD FS unter Windows Server 2012 R2:

-   [Eine zusätzliche Authentifizierungsmethode auswählen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [Einrichten der MFA-Richtlinie](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="BKMK_5"></a>Eine zusätzliche Authentifizierungsmethode auswählen
Zum Einrichten der MFA muss eine zusätzliche Authentifizierungsmethode ausgewählt werden. In dieser exemplarischen Vorgehensweise können Sie zwischen den folgenden Optionen wählen:

-   Wählen Sie [Zertifikatauthentifizierung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7) Methode, die in AD FS unter Windows Server 2012 R2 standardmäßig verfügbar ist.

-   Konfigurieren und Aktivieren von [Windows Azure Multi-Factor Authentication](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8)

#### <a name="BKMK_7"></a>Zertifikatauthentifizierung
Führen Sie eine der folgenden Verfahren aus, um die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode auszuwählen:

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>So konfigurieren Sie die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode über die AD FS-Verwaltungskonsole

1.  Navigieren Sie auf dem Verbundserver in der AD FS-Verwaltungskonsole zum Knoten **Authentifizierungsrichtlinien** , und klicken Sie im Abschnitt **Mehrstufige Authentifizierung** neben dem Unterabschnitt **Globale Einstellungen** auf den Link **Bearbeiten** .

2.  Wählen Sie im Fenster **Globale Authentifizierungsrichtlinie bearbeiten** als zusätzliche Authentifizierungsmethode **Zertifikatauthentifizierung** aus, und klicken Sie dann auf **OK**.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>So konfigurieren Sie die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode über Windows PowerShell

1.  Öffnen Sie auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > Mit dem Befehl `Get-AdfsGlobalAuthenticationPolicy` können Sie überprüfen, ob der oben angegebene Befehl erfolgreich ausgeführt wurde.

#### <a name="BKMK_8"></a>Windows Azure Multi-Factor Authentication
Führen Sie die folgenden Vorgehensweisen aus, um **Windows Azure Multi-Factor Authentication** herunterzuladen, zu konfigurieren und zur zusätzlichen Authentifizierung auf Ihrem Verbundserver auszuwählen:

1.  [Erstellen Sie einen Multi-Factor Authentication-Anbieter über das Windows Azure-Portal](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Herunterladen der Windows Azure Multi-Factor Authentication-Server](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [Installieren Sie Windows Azure Multi-Factor Authentication-Server, auf dem Verbundserver](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [Konfigurieren von Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="BKMK_a"></a>Erstellen Sie einen Multi-Factor Authentication-Anbieter über das Windows Azure-Portal

1.  Melden Sie sich beim Windows Azure-Portal als Administrator an.

2.  Wählen Sie links %%amp;quot;Active Directory%%amp;quot; aus.

3.  Wählen Sie auf der Active Directory-Seite oben **Anbieter für mehrstufige Authentifizierung**aus.  Klicken Sie anschließend unten auf **Neu**.

4.  Wählen Sie unter **App-Dienste->Active Directory** die Option **Anbieter für mehrstufige Authentifizierung** und anschließend **Schnellerfassung** aus.

5.  Wählen Sie unter **App-Dienste**die Option **Active Auth Providers**(Aktive Authentifizierungsanbieter) und anschließend **Schnellerfassung**aus.

6.  Füllen Sie die folgenden Felder aus, und wählen Sie **Erstellen** aus.

    1.  **Namen** -der Name des der Multi-Factor Authentication-Anbieter.

    2.  **Nutzungsmodell** : das Nutzungsmodell des Multi-Factor Authentication-Anbieters.

        -   **Pro Authentifizierung** -kaufmodell, die Gebühren pro Authentifizierung erhoben. Dieses Modell wird in der Regel für Szenarien mit Windows Azure Multi-Factor Authentication in einer kundenorientierten Anwendung verwendet.

        -   **Pro aktiviertem Benutzer** -kaufmodell, die pro aktiviertem Benutzer abgerechnet.  Dieses Modell wird in der Regel für mitarbeiterorientierte Szenarien wie Office 365 verwendet.

        Weitere Informationen zu Nutzungsmodellen finden Sie unter [Windows Azure-Preisdetails](http://www.windowsazure.com/pricing/details/active-directory/).

    3.  **Directory** – der Windows Azure Active Directory-Mandanten, der den Multi-Factor Authentication-Anbieter zugeordnet ist. Dies ist optional, da der Anbieter beim Sichern lokaler Anwendungen nicht mit Windows Azure Active Directory verknüpft sein muss.

7.  Nach dem Klicken auf „Erstellen“ wird der Anbieter für die mehrstufige Authentifizierung erstellt. Normalerweise wird folgende Meldung angezeigt:  Der Anbieter für Multi-Factor Authentication wurde erstellt.  Klicken Sie auf **OK**.

Im nächsten Schritt muss der Windows Azure Multi-Factor Authentication-Server heruntergeladen werden. Hierzu können Sie das Portal für Windows Azure Multi-Factor Authentication über das Windows Azure-Portal starten.

##### <a name="BKMK_b"></a>Herunterladen der Windows Azure Multi-Factor Authentication-Server

1.  Melden Sie sich beim Windows Azure-Portal als Administrator an, und klicken Sie auf den im vorherigen Verfahren erstellten Anbieter für die mehrstufige Authentifizierung. Klicken Sie anschließend auf die Schaltfläche **Verwalten** .

    Dadurch wird das Portal **Windows Azure Multi-Factor Authentication** geöffnet.

2.  Klicken Sie im Portal **Windows Azure Multi-Factor Authentication** auf **Downloads**und anschließend auf **Herunterladen** , um eine Kopie des Windows Azure Multi-Factor Authentication-Servers herunterzuladen.

Nach dem Herunterladen der ausführbaren Datei für den Windows Azure Multi-Factor Authentication-Server muss er auf dem Verbundserver installiert werden.

##### <a name="BKMK_c"></a>Installieren Sie Windows Azure Multi-Factor Authentication-Server, auf dem Verbundserver

1.  Laden Sie die ausführbare Datei für den Windows Azure Multi-Factor Authentication-Server herunter, und doppelklicken Sie darauf.  Dadurch wird die Installation gestartet.

2.  Lesen Sie auf dem Bildschirm mit der Lizenzvereinbarung die Vereinbarung, wählen Sie **Ich stimme zu** aus, und klicken Sie dann auf **Weiter**.

3.  Stellen Sie sicher, dass der Zielordner richtig ist, und klicken Sie dann auf **Weiter**.

4.  Wenn die Installation abgeschlossen ist, klicken Sie auf **Fertig stellen**.

Sie können nun den auf Ihrem Verbundserver installierten Windows Azure Multi-Factor Authentication-Server starten und ihn als zusätzliche Authentifizierungsmethode konfigurieren.

##### <a name="BKMK_d"></a>Konfigurieren von Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode

1.  Starten Sie **Windows Azure Multi-Factor Authentication** vom Speicherort auf dem Verbundserver, aktivieren Sie auf der Willkommensseite das Kontrollkästchen **Verwendung des Authentifizierungskonfigurations-Assistenten überspringen** , und klicken Sie dann auf **Weiter**.

2.  Wechseln Sie zum Aktivieren des Multi-Factor Authentication-Servers zurück auf die Seite im Multi-Factor Authentication-Verwaltungsportal, auf der Sie den Multi-Factor Authentication-Server heruntergeladen haben, und klicken Sie auf die Schaltfläche **Anmeldeinformationen für Aktivierung generieren** . Geben Sie auf der Benutzeroberfläche des Multi-Factor Authentication-Servers die generierten Anmeldeinformationen ein, und klicken Sie auf **Aktivieren**.

3.  Auf der Benutzeroberfläche von **Multi-Factor Authentication-Server** werden Sie zum Ausführen des **Multiserverkonfigurations-Assistenten** aufgefordert.  Klicken Sie auf **Nein**.

    > [!IMPORTANT]
    > Da zum Abschließen dieser exemplarischen Vorgehensweise eine Testumgebung mit nur einem Verbundserver verwendet wird, können Sie die Ausführung des **Multiserverkonfigurations-Assistenten** überspringen. Wenn Ihre Umgebung jedoch mehrere Verbundserver enthält, müssen Sie den Multi-Factor Authentication-Server installieren und den **Multiserverkonfigurations-Assistenten** auf jedem Verbundserver ausführen, um die Replikation zwischen den auf den Verbundservern ausgeführten Multi-Factor-Servern zu ermöglichen.

4.  Wählen Sie auf der Benutzeroberfläche **Multi-Factor Authentication-Server** das Symbol **Benutzer** aus, klicken Sie auf **Aus Active Directory importieren**, wählen Sie das Konto **Robert Hatley** für die Bereitstellung in Windows Azure Multi-Factor Authentication aus, und klicken Sie anschließend auf **Importieren**.

5.  Wählen Sie in der Liste **Benutzer** das Konto **Robert Hatley** aus, klicken Sie auf **Bearbeiten**, und geben Sie im Fenster **Benutzer bearbeiten** eine Mobiltelefonnummer ein. Vergewissern Sie sich, dass das Kontrollkästchen **Aktiviert** markiert ist, und klicken Sie anschließend auf **Anwenden**.

6.  Wählen Sie in der Liste **Benutzer** das Konto **Robert Hatley** aus, und klicken Sie auf **Testen**. Geben Sie im Fenster **Benutzer testen** die Anmeldeinformationen für das Konto **Robert Hatley** ein. Wenn das Mobiltelefon klingelt, drücken Sie '#', um die kontoüberprüfung abzuschließen.

7.  Wählen Sie auf der Benutzeroberfläche **Multi-Factor Authentication-Server** das Symbol **AD FS** aus, und vergewissern Sie sich, dass die Kontrollkästchen **Benutzerregistrierung zulassen**, **Methodenauswahl durch Benutzer zulassen** (einschließlich **Telefonanruf** und **SMS**), **Sicherheitsfragen für Alternative verwenden** und **Protokollierung aktivieren** aktiviert sind. Klicken Sie auf **AD FS-Adapter installieren**, und führen Sie den Installations-Assistenten für **Multi-Factor Authentication AD FS Adapter** (Multi-Factor Authentication-AD FS-Adapter) aus.

    > [!NOTE]
    > Vom Installations-Assistenten für **Multi-Factor Authentication AD FS Adapter** (Multi-Factor Authentication-AD FS-Adapter) wird in Ihrem Active Directory eine Sicherheitsgruppe namens **PhoneFactor Admins** erstellt. Anschließend wird das AD FS-Dienstkonto Ihres Verbunddiensts dieser Gruppe hinzugefügt.
    > 
    > Überprüfen Sie für den Domänencontroller, ob die Gruppe **PhoneFactor Admins** tatsächlich erstellt wurde und das AD FS-Dienstkonto ein Mitglied dieser Gruppe ist.
    > 
    > Fügen Sie ggf. das AD FS-Dienstkonto manuell zur Gruppe **PhoneFactor Admins** auf dem Domänencontroller hinzu.

    Klicken Sie im Multi-Factor Authentication-Server in der Ecke oben rechts auf den Hilfelink, um zusätzliche Informationen zum Installieren des AD FS-Adapters zu erhalten.

8.  Starten Sie zum Registrieren des Adapters im Verbunddienst auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus: `\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`. Der Adapter ist nun als **WindowsAzureMultiFactorAuthentication** registriert.  Der AD FS-Dienst muss neu gestartet werden, damit die Registrierung wirksam wird.

9. Navigieren Sie zum Konfigurieren von Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode in der AD FS-Verwaltungskonsole zum Knoten **Authentifizierungsrichtlinien**, und klicken Sie im Abschnitt **Mehrstufige Authentifizierung** neben dem Unterabschnitt **Globale Einstellungen** auf den Link **Bearbeiten**. Wählen Sie im Fenster **Globale Authentifizierungsrichtlinie bearbeiten** als zusätzliche Authentifizierungsmethode **Mehrstufige Authentifizierung** aus, und klicken Sie dann auf **OK**.

    > [!NOTE]
    > Sie können den Namen und die Beschreibung der Windows Azure Multi-Factor Authentication-Methode sowie jeder anderen konfigurierten Authentifizierungsmethode von Drittanbietern auf der AD FS-Benutzeroberfläche mithilfe des **Set-AdfsAuthenticationProviderWebContent**-Cmdlets anpassen. Weitere Informationen finden Sie unter [https://technet.microsoft.com/library/dn479401.aspx](https://technet.microsoft.com/library/dn479401.aspx)

### <a name="BKMK_6"></a>Einrichten der MFA-Richtlinie
Zum Aktivieren der MFA muss die MFA-Richtlinie auf dem Verbundserver eingerichtet werden. In dieser exemplarischen Vorgehensweise gemäß unserer MFA-Richtlinie **Robert Hatley** Konto ist erforderlich, um die MFA durchlaufen, da er gehört die **Finance** Gruppe, die Sie in einrichten [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Sie können die MFA-Richtlinie entweder über die AD FS-Verwaltungskonsole oder mithilfe von Windows PowerShell einrichten.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>So konfigurieren Sie die MFA-Richtlinie, die Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für claimapp 'Bearbeiten' über die AD FS-Verwaltungskonsole

1.  Navigieren Sie auf dem Verbundserver in der AD FS-Verwaltungskonsole zum Knoten **Authentifizierungsrichtlinien**\\**Pro Vertrauensstellung der vertrauenden Seite** , und wählen Sie die Vertrauensstellung der vertrauenden Seite aus, die Ihre Beispielanwendung (**claimapp**) darstellt.

2.  Wählen Sie entweder auf der Seite **Aktionen** oder durch Rechtsklick auf **claimapp**die Option **Benutzerdefinierte mehrstufige Authentifizierung bearbeiten**aus.

3.  Klicken Sie im Fenster **Vertrauensstellung der vertrauenden Seite für claimapp bearbeiten** neben der Liste **Benutzer/Gruppen** auf **Hinzufügen** . Geben Sie in **Finance** für den Namen der AD-Gruppe, die Sie in erstellt [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md), und klicken Sie auf **Namen überprüfen**, und wenn der Name ist Klicken Sie mit der aufgelöst, auf **OK**.

4.  Klicken Sie im Fenster **Vertrauensstellung der vertrauenden Seite für claimapp bearbeiten** auf **OK**.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>So konfigurieren Sie die MFA-Richtlinie, die Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für claimapp 'Bearbeiten' über Windows PowerShell

1.  Öffnen Sie auf dem Verbundserver das Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl aus:

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  Führen Sie im selben Windows PowerShell-Befehlsfenster den folgenden Befehl aus:

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > Achten Sie darauf, <group_SID> durch den Wert der SID der AD-Gruppe **Finance** zu ersetzen.

## <a name="BKMK_4"></a>Schritt 4: Überprüfen des MFA-Mechanismus
In diesem Schritt wird die im vorherigen Schritt eingerichtete MFA-Funktionalität überprüft. Mithilfe des folgenden Verfahrens können Sie überprüfen, ob der AD-Benutzer **Robert Hatley** auf Ihre Beispielanwendung zugreifen kann und dieses Mal die MFA durchlaufen muss, da er zur Gruppe **Finance** gehört.

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Mit dieser Aktion wird die Anforderung automatisch an den Verbundserver umgeleitet, und Sie werden zur Anmeldung mit einem Benutzernamen und einem Kennwort aufgefordert.

2.  Geben Sie die Anmeldeinformationen des AD-Kontos **Robert Hatley** ein.

    Hier wird der Benutzer aufgrund der von Ihnen konfigurierten MFA-Richtlinie zur zusätzlichen Authentifizierung aufgefordert. Der Standardtext der Meldung lautet **Aus Sicherheitsgründen sind weitere Informationen erforderlich, um Ihr Konto zu überprüfen** . Dieser Text kann jedoch vollständig angepasst werden. Weitere Informationen zum Anpassen der Anmeldeseiten finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).

    Wenn Sie die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode konfiguriert haben, wird der Standardtext der Meldung **wählen Sie ein Zertifikat, das Sie für die Authentifizierung verwenden möchten. Wenn Sie den Vorgang abbrechen, Bitte schließen Sie Ihren Browser, und versuchen Sie es erneut.**

    Wenn Sie Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode konfiguriert haben, lautet der Standardtext der Meldung **Ihr Telefon wird angerufen, um Ihre Authentifizierung abzuschließen.** Weitere Informationen zum Anmelden mit Windows Azure Multi-Factor Authentication und mithilfe der verschiedenen Optionen für die bevorzugte Methode der Überprüfung finden Sie unter [Windows Azure Multi-Factor Authentication Overview](https://technet.microsoft.com/library/dn249479.aspx).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



