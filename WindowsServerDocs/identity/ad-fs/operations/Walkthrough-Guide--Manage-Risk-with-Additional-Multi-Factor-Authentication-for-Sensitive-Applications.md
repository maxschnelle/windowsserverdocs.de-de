---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: "Handbuch mit exemplarischer Vorgehensweise - Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 414f37e86f0072863e5fa2f107c39e5518e560ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen

>Gilt für: Windows Server 2012 R2


## <a name="about-this-guide"></a>Informationen zum Handbuch
Diese exemplarische Vorgehensweise enthält Anweisungen zum Konfigurieren der mehrstufigen Authentifizierung (MFA) in Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2 anhand von Gruppenmitgliedschaftsdaten des Benutzers.

Weitere Informationen zur MFA und Authentifizierungsmechanismen in AD FS finden Sie unter [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).

In dieser exemplarischen Vorgehensweise besteht aus den folgenden Abschnitten:

-   [Schritt 1: Einrichten der testumgebung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Schritt 2: Überprüfen des Standardmechanismus für AD FS-Authentifizierung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [Schritt 3: Konfigurieren der mehrstufigen Authentifizierung auf dem Verbundserver](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [Schritt 4: Überprüfen des MFA-Mechanismus](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="BKMK_1"></a>Schritt 1: Einrichten der testumgebung
Um diese exemplarische Vorgehensweise abzuschließen, benötigen Sie eine Umgebung, die die folgenden Komponenten:

-   Active Directory-Domäne mit einem Testbenutzer und testgruppenkonten unter Windows Server 2012 R2 oder Active Directory-Domäne unter Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 mit einem Upgrade auf Windows Server 2012 R2

-   Verbundserver unter Windows Server 2012 R2

-   Ein Webserver, der für Ihre beispielanwendung gehostet

-   Ein Clientcomputer, von dem Sie die beispielanwendung zugreifen können

> [!WARNING]
> Es wird (sowohl in einer produktionsumgebung und testumgebungen) dringend empfohlen, dass Sie nicht denselben Computer den Verbundserver und den Webserver zu verwenden.

In dieser Umgebung gibt der Verbundserver die Ansprüche, die erforderlich sind, damit Benutzer auf die beispielanwendung zugreifen können. Der Webserver hostet einer beispielanwendung, die den Benutzern vertraut wird, die die Ansprüche, die vorhanden vom Verbundserver ausgestellten.

Eine Anleitung zum Einrichten dieser Umgebung finden Sie unter [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

## <a name="BKMK_2"></a>Schritt 2: Überprüfen des Standardmechanismus für AD FS-Authentifizierung
In diesem Schritt überprüfen Sie den standardmäßigen AD FS-Mechanismus (**Formularauthentifizierung** für extranet und **Windows-Authentifizierung** für das Intranet), in denen der Benutzer auf die AD FS-Anmeldeseite weitergeleitet wird, gültige Anmeldeinformationen und erhält Zugriff auf die Anwendung. Können die **Robert Hatley** AD-Konto und die **Claimapp** Beispiel-App, die Sie in konfiguriert [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Diese Aktion aus, leitet die Anforderung automatisch an den Verbundserver und Sie werden aufgefordert, sich mit einem Benutzernamen und Kennwort anmelden.

2.  Geben Sie die Anmeldeinformationen von der **Robert Hatley** AD-Konto, das Sie erstellt haben [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

    Sie können den Zugriff auf die Anwendung gewährt werden.

## <a name="BKMK_3"></a>Schritt 3: Konfigurieren der mehrstufigen Authentifizierung auf dem Verbundserver
Es gibt zwei Teile für die Konfiguration der MFA in AD FS unter Windows Server 2012 R2:

-   [Wählen Sie eine zusätzliche Authentifizierungsmethode](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [Einrichten der MFA-Richtlinie](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="BKMK_5"></a>Wählen Sie eine zusätzliche Authentifizierungsmethode
Zum Einrichten der MFA, müssen Sie eine zusätzliche Authentifizierungsmethode auswählen. In dieser exemplarischen Vorgehensweise für zusätzliche Authentifizierungsmethode können Sie zwischen den folgenden Optionen auswählen:

-   Wählen Sie [Zertifikatauthentifizierung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7) Methode, die in AD FS unter Windows Server 2012 R2 standardmäßig verfügbar ist.

-   Konfigurieren und aktivieren Sie [Windows Azure Multi-Factor Authentication](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8)

#### <a name="BKMK_7"></a>Zertifikatbasierte Authentifizierung
Führen Sie eine der folgenden Verfahren, um die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode auswählen:

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>So konfigurieren Sie die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode über die AD FS-Verwaltungskonsole

1.  Navigieren Sie auf dem Verbundserver in der AD FS-Verwaltungskonsole zu den **Authentifizierungsrichtlinien** Knoten, und wählen Sie unter **Multi-Factor Authentication** auf die **bearbeiten** neben Verknüpfen der **globale Einstellungen** Unterabschnitt.

2.  In der **globale Authentifizierungsrichtlinie bearbeiten** wählen **Zertifikatauthentifizierung** als zusätzliche Authentifizierungsmethode, und klicken Sie dann auf **OK**.

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>So konfigurieren Sie die Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode über Windows PowerShell

1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus:

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > Um sicherzustellen, dass dieser Befehl erfolgreich ausgeführt wurde, können Sie Ausführen der `Get-AdfsGlobalAuthenticationPolicy` Befehl.

#### <a name="BKMK_8"></a>Windows Azure Multi-Factor Authentication
Führen Sie die folgenden Verfahren zum Herunterladen und konfigurieren, und wählen Sie **Windows Azure Multi-Factor Authentication** zusätzlichen Authentifizierung auf dem Verbundserver:

1.  [Erstellen Sie einen Multi-Factor Authentication-Anbieter über das Windows Azure-Portal](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Herunterladen von Windows Azure Multi-Factor Authentication-Server](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [Installieren Sie Windows Azure Multi-Factor Authentication-Server, auf dem Verbundserver](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [Konfigurieren von Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="BKMK_a"></a>Erstellen Sie einen Multi-Factor Authentication-Anbieter über das Windows Azure-Portal

1.  Melden Sie sich bei Windows Azure Portal als Administrator.

2.  Wählen Sie auf der linken Seite Active Directory.

3.  Wählen Sie auf der Seite Active Directory oben **Multi-Factor Authentication-Anbieter**.  Klicken Sie dann unten auf **neu**.

4.  Unter **App-Dienste -> Active Directory**Option **Multi-Factor Authentication-Anbieters**, und wählen Sie **Schnellerfassung**.

5.  Unter **App-Dienste**Option **Active Auth Providers**, und wählen Sie **Schnellerfassung**.

6.  Füllen Sie die folgenden Felder und wählen Sie **erstellen**.

    1.  **Namen** -der Name des Multi-Factor Authentication-Anbieters.

    2.  **Verwendungsmodell** – das Syntaxmodell des Multi-Factor Authentication-Anbieter.

        -   **Pro Authentifizierung** – einkaufsmodell, die Gebühren pro Authentifizierung erhoben. In der Regel verwendet für Szenarien mit Windows Azure Multi-Factor Authentication in einer Anwendung verbraucherorientierte.

        -   **Pro aktiviertem Benutzer** – einkaufsmodell, die Gebühren pro aktiviertem Benutzer erhoben.  In der Regel verwendet für mitarbeiterorientierte Szenarien wie Office 365.

        Weitere Informationen zu nutzungsmodellen finden Sie unter [Windows Azure-Preisdetails](http://www.windowsazure.com/pricing/details/active-directory/).

    3.  **Directory** -der Windows Azure Active Directory-Mandanten, die den Multi-Factor Authentication-Anbieter zugeordnet ist. Dies ist optional, da der Anbieter nicht mit Windows Azure Active Directory verknüpft sein, beim Sichern lokaler Anwendungen.

7.  Nach dem Klicken auf erstellen, die Multi-Factor Authentication-Anbieter erstellt werden, und Sie sollten eine Meldung angezeigt: Anbieter für Multi-Factor Authentication wurde erstellt.  Klicken Sie auf **Ok**.

Als Nächstes müssen Sie den Windows Azure Multi-Factor Authentication-Server herunterladen. Hierzu können Sie über das Windows Azure-Portal im Windows Azure Multi-Factor Authentication-Verwaltungsportal starten.

##### <a name="BKMK_b"></a>Herunterladen von Windows Azure Multi-Factor Authentication-Server

1.  Melden Sie sich bei Windows Azure-Portal als Administrator, und klicken Sie auf den Multi-Factor Authentication-Anbieter, die Sie den im vorherigen Verfahren erstellt haben. Klicken Sie dann auf die **verwalten** Schaltfläche.

    Dadurch wird die **Windows Azure Multi-Factor Authentication** Portal.

2.  In der **Windows Azure Multi-Factor Authentication** -Portal auf **Downloads**, und klicken Sie dann auf **herunterladen** eine Kopie von Windows Azure Multi-Factor Authentication-Server herunterladen.

Nachdem Sie die ausführbare Datei für die Windows Azure Multi-Factor Authentication-Server heruntergeladen haben, müssen Sie es auf dem Verbundserver installieren.

##### <a name="BKMK_c"></a>Installieren Sie Windows Azure Multi-Factor Authentication-Server, auf dem Verbundserver

1.  Herunterladen Sie, und doppelklicken Sie auf die ausführbare Datei für die Windows Azure Multi-Factor Authentication-Server.  Dadurch wird die Installation zu starten.

2.  Die Lizenzbedingungen, lesen Sie den Lizenzvertrag, wählen Sie auf **ich stimme zu** , und klicken Sie auf **Weiter**.

3.  Stellen Sie sicher, dass der Zielordner richtig ist, und klicken Sie auf **Weiter**.

4.  Wenn die Installation abgeschlossen ist, klicken Sie auf **Fertig stellen**.

Sie sind nun bereit zum Starten des Windows Azure Multi-Factor Authentication-Servers, den Sie auf dem Verbundserver installiert und ihn als zusätzliche Authentifizierungsmethode konfigurieren.

##### <a name="BKMK_d"></a>Konfigurieren von Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode

1.  Starten Sie **Windows Azure Multi-Factor Authentication** überprüfen Sie, wo Sie auf dem Verbundserver, und klicken Sie auf der Seite "Willkommen" installiert, die **überspringen mithilfe des Assistenten für die Authentifizierung** Kontrollkästchen und klicken Sie auf **Weiter**.

2.  Um den Multi-Factor Authentication-Server zu aktivieren, wechseln Sie zurück zur Seite im Multi-Factor Authentication-Verwaltungsportal, in dem Sie den Multi-Factor Authentication-Server heruntergeladen haben, und klicken Sie auf die **Anmeldeinformationen für Aktivierung generieren** Schaltfläche. Geben Sie in der Benutzeroberfläche des Multi-Factor Authentication-Server, die Anmeldeinformationen, die generiert wurden, und klicken Sie auf **aktivieren**.

3.  Als Nächstes wird die **Multi-Factor Authentication-Server** Benutzeroberfläche werden Sie aufgefordert, führen Sie die **Multiserverkonfigurations-Assistenten**.  Wählen Sie **keine**.

    > [!IMPORTANT]
    > Überspringen Sie Abschließen der **Multiserverkonfigurations-Assistenten** eine testumgebung mit nur einem Verbundserver, die zum Abschließen dieser exemplarischen Vorgehensweise verwendet wird. Jedoch Ihre Umgebung mehrere Verbundserver enthält, müssen Sie den Multi-Factor Authentication-Server installieren und Ausführen der **Multiserverkonfigurations-Assistenten** auf jedem Verbundserver, um die Replikation zwischen den Multi-Factor-Servern, die auf Ihrem Verbundserver zu aktivieren.

4.  In der **Multi-Factor Authentication-Server** Benutzeroberfläche der **Benutzer** Symbol, klicken Sie auf **aus Active Directory importieren**, wählen die **Robert Hatley** Bereitstellung in Windows Azure Multi-Factor Authentication-Konto, und klicken Sie dann auf **Import**.

5.  In der **Benutzer** Liste, wählen die **Robert Hatley** Konto ein, klicken Sie auf **bearbeiten**, und in der **Benutzer bearbeiten** Fenster eine Mobiltelefonnummer für dieses Konto angeben, stellen Sie sicher das **aktiviert** Kontrollkästchen aktiviert ist, und klicken Sie dann auf **übernehmen**.

6.  In der **Benutzer** Liste, wählen die **Robert Hatley** Konto, und klicken Sie auf **Test**. In der **Testbenutzer** Fenster, geben Sie die Anmeldeinformationen für die **Robert Hatley** Konto. Wenn das Mobiltelefon klingelt, drücken Sie "#", um die kontoüberprüfung abzuschließen.

7.  In der **Multi-Factor Authentication-Server** Benutzeroberfläche der **AD FS** Symbol, stellen Sie sicher, dass **benutzerregistrierung zulassen**, **ermöglichen Benutzern das Auswählen der Methode** (einschließlich **Telefonanruf** und **SMS**), **Sicherheitsfragen als Alternative verwenden** und **Aktivieren der Protokollierung** Kontrollkästchen aktiviert sind, klicken Sie auf **AD FS-Adapter installieren**, und schließen Sie die **Multi-Factor Authentication AD FS-Adapter** Installations-Assistenten.

    > [!NOTE]
    > Die **Multi-Factor Authentication AD FS-Adapter** Installations-Assistent erstellt eine Sicherheitsgruppe namens **PhoneFactor Admins** in Active Directory und fügt dann die AD FS-Dienstkonto Ihres Verbunddiensts dieser Gruppe.
    > 
    > Es wird empfohlen, vergewissern Sie sich auf dem Domänencontroller, die die **PhoneFactor Admins** Gruppe wird tatsächlich erstellt und die AD FS-Dienstkonto ein Mitglied dieser Gruppe ist.
    > 
    > Fügen Sie ggf. das AD FS-Dienstkonto der **PhoneFactor Admins** manuell auf dem Domänencontroller zu gruppieren.

    Weitere Informationen zum Installieren von AD FS-Adapter klicken Sie auf den Link Hilfe in der oberen rechten Ecke des Multi-Factor Authentication-Servers.

8.  Registrieren des Adapters im Verbunddienst auf dem Verbundserver Starten der Windows PowerShell-Befehlsfenster, und führen Sie den folgenden Befehl: `\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`. Der Adapter ist nun registriert, als **WindowsAzureMultiFactorAuthentication**.  Sie müssen Ihre AD FS-Dienst für die Registrierung wirksam neu starten.

9. So konfigurieren Sie Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode, in der AD FS-Verwaltungskonsole, navigieren Sie zu der **Authentifizierungsrichtlinien** Knoten, und wählen Sie unter **Multi-Factor Authentication** auf die **bearbeiten** neben dem Verknüpfen der **globale Einstellungen** Unterabschnitt. In der **globale Authentifizierungsrichtlinie bearbeiten** wählen **Multi-Factor Authentication** als zusätzliche Authentifizierungsmethode, und klicken Sie dann auf **OK**.

    > [!NOTE]
    > Sie können anpassen, dass der Name und Beschreibung des Windows Azure Multi-Factor Authentication-Methode als auch eine Authentifizierungsmethode von Drittanbietern konfiguriert, wie er in der AD FS-Benutzeroberfläche angezeigt, durch Ausführen wird der **Set-AdfsAuthenticationProviderWebContent** Cmdlet. Weitere Informationen finden Sie unter [https://technet.microsoft.com/library/dn479401.aspx](https://technet.microsoft.com/library/dn479401.aspx)

### <a name="BKMK_6"></a>Einrichten der MFA-Richtlinie
Um MFA zu aktivieren, müssen Sie die MFA-Richtlinie auf Ihrem Verbundserver einrichten. Für diese exemplarischen Vorgehensweise muss gemäß unserer MFA-Richtlinie **Robert Hatley** Konto ist erforderlich, um die MFA durchlaufen, da er zur Gruppe der **Finanzen** Gruppe, die Sie in einrichten [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Sie können die MFA-Richtlinie entweder über die AD FS-Verwaltungskonsole oder über die Windows PowerShell einrichten.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>So konfigurieren Sie die MFA-Richtlinie auf der Grundlage der Gruppenmitgliedschaftsdaten des Benutzers für "Claimapp" über die AD FS-Verwaltungskonsole

1.  Navigieren Sie auf dem Verbundserver in der AD FS-Verwaltungskonsole zu **Authentifizierungsrichtlinien**\\**pro Vertrauensstellungen der vertrauenden Seite Vertrauensstellung** Knoten, und wählen Sie die Vertrauensstellung aus der vertrauenden Seite, die Ihre beispielanwendung (**Claimapp**).

2.  In der **Aktionen** Seite oder durch Rechtsklick auf **Claimapp**Option **benutzerdefinierte mehrstufige Authentifizierung bearbeiten**.

3.  In der **Bearbeiten der vertrauenden Seite Vertrauensstellung für Claimapp** Fenster, klicken Sie auf die **hinzufügen** neben der **Benutzer/Gruppen** Liste. Geben Sie im **Finanzen** für den Namen des AD-Gruppe, die Sie in erstellt [Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md), und klicken Sie auf **Namen überprüfen**, und wenn der Name aufgelöst wird, klicken Sie auf **OK**.

4.  Klicken Sie auf **OK** in der **Bearbeiten der vertrauenden Seite Vertrauensstellung für Claimapp** Fenster.

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>So konfigurieren Sie die MFA-Richtlinie auf der Grundlage der Gruppenmitgliedschaftsdaten des Benutzers für 'Claimapp' über Windows PowerShell

1.  Auf dem Verbundserver das Windows PowerShell-Befehlsfenster geöffnet, und führen Sie den folgenden Befehl aus:

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  Führen Sie in der gleichen Windows PowerShell-Befehlsfenster den folgenden Befehl ein:

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > Achten Sie darauf, < Group_SID > durch den Wert der SID der AD-Gruppe ersetzen **Finanzen**.

## <a name="BKMK_4"></a>Schritt 4: Überprüfen des MFA-Mechanismus
In diesem Schritt überprüfen Sie die MFA-Funktionalität, die Sie im vorherigen Schritt haben eingerichtet. Sie können das folgende Verfahren verwenden, zu überprüfen, ob **Robert Hatley** AD-Benutzer auf Ihre beispielanwendung zugreifen kann und dieses Mal ist erforderlich, um die MFA durchlaufen, da er zur Gruppe der **Finanzen** Gruppe.

1.  Klicken Sie auf dem Clientcomputer ein Browserfenster öffnen, und navigieren Sie zur beispielanwendung: **https://webserv1.contoso.com/claimapp**.

    Diese Aktion aus, leitet die Anforderung automatisch an den Verbundserver und Sie werden aufgefordert, sich mit einem Benutzernamen und Kennwort anmelden.

2.  Geben Sie die Anmeldeinformationen von der **Robert Hatley** AD-Konto.

    An diesem Punkt wird aufgrund der MFA-Richtlinie, die Sie konfiguriert, der Benutzer aufgefordert werden zur zusätzlichen Authentifizierung. Der Standardtext der Meldung ist **aus Gründen der Sicherheit, die wir benötigen zusätzliche Informationen zur Überprüfung Ihres Kontos.** Dieser Text kann jedoch vollständig angepasst werden. Weitere Informationen zur Vorgehensweise beim Anpassen der Anmeldeseiten finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).

    Wenn Sie Zertifikatauthentifizierung als zusätzliche Authentifizierungsmethode konfiguriert haben, wird der Standardtext der Meldung **wählen Sie ein Zertifikat, das Sie für die Authentifizierung verwenden möchten. Wenn Sie den Vorgang abbrechen, schließen Ihr Browser, und versuchen Sie es erneut.**

    Wenn Sie Windows Azure Multi-Factor Authentication als zusätzliche Authentifizierungsmethode konfiguriert haben, wird der Standardtext der Meldung **ein Anruf wird auf Ihrem Handy, um Ihre Authentifizierung abzuschließen.** Weitere Informationen zum Anmelden mit Windows Azure Multi-Factor Authentication und mithilfe der verschiedenen Optionen für die bevorzugte Überprüfungsmethode finden Sie unter [Windows Azure Multi-Factor Authentication Overview](https://technet.microsoft.com/library/dn249479.aspx).

## <a name="see-also"></a>Siehe auch
[Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Einrichten der testumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



