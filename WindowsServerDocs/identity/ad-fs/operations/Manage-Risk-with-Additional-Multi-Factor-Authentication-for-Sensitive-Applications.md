---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: "Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9ee275e6fe38005394cd071e9cfe9a7999350e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen

>Gilt für: Windows Server 2012 R2


-   [Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [Konfigurieren Sie zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>In diesem Handbuch
Dieses Handbuch enthält die folgende Informationen:

-   [Authentifizierungsmechanismen in AD FS](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1) -Beschreibung der in Active Directory-Verbunddienste (AD FS) in Windows Server2012 R2 verfügbaren Authentifizierungsmechanismen

-   [Übersicht über das Szenario](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2) -eine Beschreibung eines Szenarios, in denen Sie Active Directory-Verbunddienste (AD FS) verwenden, um die mehrstufige Authentifizierung (MFA) aktivieren, basierend auf der Gruppenmitgliedschaft des Benutzers.

    > [!NOTE]
    > In AD FS unter Windows Server2012 R2 können Sie die MFA auf Grundlage der Netzwerkadresse, geräteidentität und Benutzer Benutzeridentität oder der Gruppenmitgliedschaft aktivieren.

    Ausführliche schrittweise Anleitung zum Konfigurieren und überprüfen dieses Szenarios finden Sie unter [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).

## <a name="BKMK_1"></a>Wichtige Konzepte – Authentifizierungsmechanismen in AD FS

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>Vorteile der Authentifizierungsmechanismen in AD FS
Active Directory-Verbunddienste (AD FS) in Windows Server2012 R2 bietet IT-Administratoren mit komfortablere, flexiblere Tools für die Authentifizierung von Benutzern, die auf Unternehmensressourcen zugreifen möchten. Sie können Administratoren die primären und zusätzlichen Authentifizierungsmethoden flexibel steuern, bietet eine umfassende Verwaltungsfunktionen zum Konfigurieren von Authentifizierungsrichtlinien Richtlinien (sowohl über die Benutzeroberfläche und Windows PowerShell) und verbessern die Benutzerfreundlichkeit für Endbenutzer, die Zugriff auf Anwendungen und Dienste, die von AD FS geschützt sind. Im folgenden sind einige der Vorteile beim Sichern Ihrer Anwendungen und Dienste mit AD FS unter Windows Server2012 R2:

-   Globale Authentifizierungsrichtlinie – eine zentrale Verwaltungsfunktion, aus der IT-Administrator auswählen kann, welche Authentifizierungsmethoden verwendet werden, zum Authentifizieren von Benutzern, die basierend auf den Speicherort im Netzwerk, von dem sie auf geschützte Ressourcen zugreifen. Dadurch können Administratoren die folgenden Schritteausführen:

    -   Geben Sie die Verwendung von Authentifizierungsmethoden für Zugriffsanforderungen über das Extranet.

    -   Aktivieren der Geräteauthentifizierung für nahtlose zweistufige Authentifizierung. Dies bindet die Identität des Benutzers mit dem registrierten Gerät, das verwendet wird, auf die Ressource, die somit sicherere Überprüfung der Verbundidentität anbieten, bevor auf geschützte Ressourcen zugegriffen wird.

        > [!NOTE]
        > Weitere Informationen zu Geräteobjekt, Geräteregistrierungsdienst, Arbeitsplatzbeitritt und das Gerät als nahtlose zweistufige Authentifizierung und SSO finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

    -   Legen die MFA-Anforderung für den gesamten Extranetzugriff oder bedingt auf Grundlage der Benutzeridentität, Netzwerkadresse oder ein Gerät, das verwendet wird, Zugriff auf geschützte Ressourcen.

-   Eine größere Flexibilität beim Konfigurieren von Authentifizierungsrichtlinien: Sie können benutzerdefinierte Authentifizierungsrichtlinien für AD FS-gesicherte Ressourcen mit variierenden Geschäftswerten konfigurieren. Beispielsweise können Sie für die Anwendung mit hoher unternehmensauswirkung die MFA verlangen.

-   Erleichterte Bedienung: einfachen und intuitiven Verwaltungstools wie der GUI-basierte AD FS-Management-MMC-Snap-In und Windows PowerShell-Cmdlets können IT-Administratoren relativ einfach Authentifizierungsrichtlinien konfigurieren. Mit der Windows PowerShell können Sie Skripts für Ihre Lösungen für die Verwendung bei einer Skalierung und alltägliche Verwaltungsaufgaben automatisieren.

-   Eine bessere Kontrolle über Unternehmensdaten: Da als Administrator können Sie AD FS so konfigurieren Sie eine Authentifizierungsrichtlinie, die für eine bestimmte Ressource gilt, größer Sie haben steuern, wie Unternehmensressourcen gesichert werden. Anwendungen können nicht von IT-Administratoren angegebenen Authentifizierungsrichtlinien überschreiben. Für sensible Anwendungen und Dienste können Sie MFA-Anforderung, Geräteauthentifizierung und optional die erneute Authentifizierung aktivieren, jedes Mal, wenn die Ressource zugegriffen wird.

-   Unterstützung für benutzerdefinierte MFA-Anbieter: für Organisationen, die MFA-Methoden von Drittanbietern nutzen, AD FS bietet die Möglichkeit zum nahtlosen einbinden und Verwenden dieser Authentifizierungsmethoden.

### <a name="authentication-scope"></a>Authentifizierung Bereich
In AD FS unter Windows Server2012 R2 können Sie eine Authentifizierungsrichtlinie für einen globalen Bereich angeben, die gilt für alle Anwendungen und Dienste, die von AD FS geschützt sind.  Sie können auch festlegen, dass Authentifizierungsrichtlinien für bestimmte Anwendungen und Dienste (Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen), die von AD FS geschützt sind. Geben Sie eine Authentifizierungsrichtlinie für eine bestimmte Anwendung (pro vertrauende Seite Vertrauensstellung) wird die globale Authentifizierungsrichtlinie nicht überschrieben. Wenn der globalen oder pro vertrauende Seite Authentifizierungsrichtlinie die MFA MFA Vertrauensstellung wird ausgelöst, wenn der Benutzer versucht, um diese Vertrauensstellung der vertrauenden Seite zu authentifizieren.  Die globale Authentifizierungsrichtlinie dient als Fallback für Vertrauensstellungen vertrauenden Seite (Anwendungen und Dienste), die keine spezielle Authentifizierungsrichtlinie konfiguriert haben.

Eine globale Authentifizierungsrichtlinie gilt für alle vertrauenden Seiten, die von AD FS geschützt sind. Sie können die folgenden Einstellungen als Teil der globalen Authentifizierungsrichtlinie konfigurieren:

-   Authentifizierungsmethoden für die primäre Authentifizierung verwendet werden

-   Einstellungen und Methoden für die MFA

-   Gibt an, ob die Geräteauthentifizierung aktiviert ist. Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Pro-Vertrauensstellungen der vertrauenden Seite Authentifizierungsrichtlinien für Vertrauensstellungen gelten speziell für Zugriffsversuche auf die Vertrauensstellung einer vertrauenden Seite (Anwendung oder Dienst). Sie können die folgenden Einstellungen im Rahmen der pro-Vertrauensstellungen der vertrauenden Seite Party Trust-Authentifizierungsrichtlinie konfigurieren:

-   Gibt an, ob Benutzer ihre Anmeldeinformationen jedes Mal beim Anmelden müssen

-   MFA-Einstellungen auf der Grundlage der Benutzer/Gruppe, Geräteregistrierung und Zugriffsanforderung Positionsdaten

### <a name="primary-and-additional-authentication-methods"></a>Primäre Authentifizierungsmethode und zusätzliche Methoden
Mit AD FS unter Windows Server2012 R2, zusätzlich zum primären Authentifizierungsmechanismus können Administratoren weitere Authentifizierungsmethoden konfigurieren. Die primären Authentifizierungsmethoden sind integriert und dienen zur Überprüfung der Benutzeridentität. Sie können anfordern, dass weitere Informationen über die Identität des Benutzers bereitgestellt werden zusätzliche Authentifizierungsstufen konfigurieren und daher eine zuverlässigere Authentifizierung gewährleistet.

Primäre Authentifizierung in AD FS unter Windows Server2012 R2 haben Sie die folgenden Optionen:

-   Für Ressourcen, die von außerhalb des Unternehmensnetzwerks zugegriffen werden veröffentlicht wurden wird die Formularauthentifizierung standardmäßig aktiviert. Darüber hinaus können Sie auch aktivieren Zertifikatauthentifizierung (anders ausgedrückt, Smartcard-basierte Authentifizierung oder benutzerclientzertifikat-Authentifizierung, die mit AD DS verwendet werden kann).

-   Windows-Authentifizierung ist für Intranetressourcen standardmäßig aktiviert. Darüber hinaus können Sie auch Formular- und/oder die Zertifikatauthentifizierung aktivieren.

Wenn Sie mehr als eine Authentifizierungsmethode auswählen, können Ihre Benutzer auswählen, welche Methode zur Authentifizierung beim auf der Anmeldeseite für Ihre Anwendung oder den Dienst haben.

Sie können auch die Geräteauthentifizierung für nahtlose zweistufige Authentifizierung aktivieren. Dies bindet die Identität des Benutzers mit dem registrierten Gerät, das verwendet wird, auf die Ressource, die somit sicherere Überprüfung der Verbundidentität anbieten, bevor auf geschützte Ressourcen zugegriffen wird.

> [!NOTE]
> Weitere Informationen zu Geräteobjekt, Geräteregistrierungsdienst, Arbeitsplatzbeitritt und das Gerät als nahtlose zweistufige Authentifizierung und SSO finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Wenn Sie Windows-Authentifizierungsmethode (Standardoption) für Ihre Intranetressourcen angeben, werden Authentifizierungsanforderungen diese Methode nahtlos in Browsern, die Windows-Authentifizierung unterstützen.

> [!NOTE]
> Windows-Authentifizierung wird nicht von allen Browsern unterstützt. Der Authentifizierungsmechanismus in AD FS unter Windows Server2012 R2 ermittelt der Browser-Benutzer-Agent des Benutzers und mithilfe einer konfigurierbaren Einstellung bestimmt, ob dieser Benutzer-Agent auf Windows-Authentifizierung unterstützt. Administratoren können diese Liste der Benutzer-Agents hinzufügen (über den Windows PowerShell `Set-AdfsProperties -WIASupportedUserAgents`Befehl, um alternative Benutzer-Agent-Zeichenfolgen für Browser anzugeben, die Windows-Authentifizierung unterstützen. Wenn der Client-Benutzer-Agent die Windows-Authentifizierung nicht unterstützt, wird als standardfallbackmethode die Formularauthentifizierung.

### <a name="configuring-mfa"></a>Konfiguration der MFA
Es gibt zwei Teile Konfiguration der MFA in AD FS unter Windows Server2012 R2: Angeben der Bedingungen, unter denen die MFA erforderlich ist, und wählen Sie eine zusätzliche Authentifizierungsmethode. Weitere Informationen über zusätzliche Authentifizierungsmethoden finden Sie unter [Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md).

**MFA-Einstellungen**

Die folgenden Optionen stehen für MFA-Einstellungen (Bedingungen, unter denen die MFA erforderlich ist):

-   Sie können die MFA verlangen, für bestimmte Benutzer und Gruppen in der AD-Domäne, der Ihr Verbundserver angehört.

-   Sie können die MFA für registrierte (mit dem Arbeitsplatz verbundene) oder nicht registriert (nicht mit dem Arbeitsplatz verbundene) anfordern Geräte.

    Windows Server2012 R2 wird einen benutzerorientierter Ansatz auf moderne Geräte, der Geräteobjekten, in denen eine Beziehung zwischen darstellen user@deviceund einem Unternehmen dar. Geräteobjekte sind eine neue Klasse in AD unter Windows Server2012 R2 zum Verbundidentität, bei der Bereitstellung des Zugriffs auf Anwendungen und Diensten verwendet werden kann. Eine neue Komponente von AD FS - des Geräteregistrierungsdiensts (DRS) – stellt eine geräteidentität in Active Directory und legt ein Zertifikat auf dem Gerät des Verbrauchers, das zum Darstellen der Identität des Geräts verwendet werden. Anschließend können Sie dieses Gerät Identität mit einem Arbeitsplatz verbinden Sie Ihr Gerät, in anderen Worten, um Ihr persönliches Gerät mit Active Directory Ihres Arbeitsplatzes zu verbinden. Wenn Sie Ihr persönliches Gerät mit dem Arbeitsplatz verbinden, wird zu einem bekannten Gerät und stellt die nahtlose zweistufige Authentifizierung auf geschützte Ressourcen und Anwendungen bereit. Anders ausgedrückt, nachdem ein Gerät dem Arbeitsplatz beigetreten ist, die Identität des Benutzers an das Gerät gebunden ist und für eine nahtlose verbundidentitätsüberprüfung verwendet werden kann, bevor eine geschützte Ressource zugegriffen werden kann.

    Weitere Informationen zum arbeitsplatzbeitritt und verlassen, finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

-   Sie können die MFA verlangen, wenn die Zugriffsanforderung für die geschützten Ressourcen über das Extranet oder das Intranet erfolgt.

## <a name="BKMK_2"></a>Beispielszenario (Übersicht)
In diesem Szenario können Sie die MFA auf Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für eine bestimmte Anwendung. Anders ausgedrückt, richten Sie eine Authentifizierungsrichtlinie auf dem Verbundserver die MFA erforderlich ist, wenn Benutzer, die einer bestimmten Gruppe angehören, den Zugriff auf eine bestimmte Anwendung anfordern, die auf einem Webserver gehostet wird.

Genauer gesagt aktivieren Sie in diesem Szenario eine Authentifizierungsrichtlinie für eine anspruchsbasierte Anwendung namens **Claimapp**, bei dem ein AD-Benutzer **Robert Hatley** ist erforderlich, um die MFA durchlaufen, da er zur AD-Gruppe gehört **Finanzen**.

Schritt-Schritt-Anweisungen zum Einrichten und überprüfen dieses Szenarios werden bereitgestellt, [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md). Um die Schrittein dieser exemplarischen Vorgehensweise abzuschließen, müssen Sie eine Testumgebung einrichten und führen Sie die Schrittein [Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Weitere Szenarien zum Aktivieren der MFA in AD FS umfassen Folgendes:

-   Aktivieren der MFA, falls die Zugriffsanforderung über das Extranet erfolgt. Sie können ändern, dass den Code im Abschnitt "Festlegen von MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit den folgenden:

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   Aktivieren der MFA, falls die Zugriffsanforderung von einem nicht mit dem Arbeitsplatz verbundenen Gerät stammt.  Sie können ändern, dass den Code im Abschnitt "Festlegen von MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit den folgenden:

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   Aktivieren der MFA, falls der Zugriff von einem Benutzer mit einem Gerät stammt, die Arbeitsplatz verbunden, aber nicht für diesen Benutzer registriert ist. Sie können ändern, dass den Code im Abschnitt "Festlegen von MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit den folgenden:

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>Siehe auch
[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)<ph x="2">
</ph>[Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



