---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: dc6608713ddd60d20b0b717d4133d93d23fc7b25
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816253"
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen




-   [Einrichten der Laborumgebung für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [Leitfaden für die exemplarische Vorgehensweise: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>In diesem Handbuch
Dieses Handbuch enthält die folgenden Informationen:

-   [Authentifizierungsmechanismen in AD FS](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1) -Beschreibung der in Active Directory-Verbunddienste (AD FS) (AD FS) verfügbaren Authentifizierungsmechanismen in Windows Server 2012 R2

-   [Szenarioübersicht](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2) : eine Beschreibung eines Szenarios, in dem Sie mithilfe Active Directory-Verbunddienste (AD FS) (AD FS) die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) basierend auf der Gruppenmitgliedschaft des Benutzers aktivieren.

    > [!NOTE]
    > In AD FS unter Windows Server 2012 R2 können Sie die MFA basierend auf Netzwerkadresse, Geräte Identität und Benutzeridentität oder Gruppenmitgliedschaft aktivieren.

    Ausführliche Schritt-für-Schritt-Anleitungen zum Konfigurieren und überprüfen dieses Szenarios finden Sie unter Exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).

## <a name="key-concepts---authentication-mechanisms-in-ad-fs"></a><a name="BKMK_1"></a>Schlüsselkonzepte: Authentifizierungsmechanismen in AD FS

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>Vorteile der Authentifizierungsmechanismen in AD FS
Active Directory-Verbunddienste (AD FS) (AD FS) in Windows Server 2012 R2 bietet IT-Administratoren einen umfassenderen, flexiblere Satz von Tools zum Authentifizieren von Benutzern, die auf Unternehmensressourcen zugreifen möchten. Dadurch können Administratoren die primären und zusätzlichen Authentifizierungsmethoden flexibel steuern. Außerdem bietet Sie eine umfassende Verwaltungs Oberfläche für die Konfiguration von Authentifizierungs Richtlinien (sowohl über die Benutzeroberfläche als auch über Windows PowerShell) und verbessert die Benutzerfreundlichkeit für Endbenutzer, die auf die von AD FS gesicherten Anwendungen und Dienste zugreifen. Im folgenden finden Sie einige der Vorteile, die sich aus der Sicherung Ihrer Anwendung und ihrer Dienste mit AD FS in Windows Server 2012 R2 ergeben:

-   Globale Authentifizierungs Richtlinie: eine zentrale Verwaltungsfunktion, von der ein IT-Administrator auswählen kann, welche Authentifizierungsmethoden zum Authentifizieren von Benutzern basierend auf dem Netzwerk Speicherort verwendet werden, von dem aus Sie auf geschützte Ressourcen zugreifen. Dies ermöglicht Administratoren Folgendes:

    -   Erzwingen der Verwendung sichererer Authentifizierungsmethoden für Zugriffsanforderungen über das Extranet

    -   Aktivieren der Geräteauthentifizierung für nahtlose zweistufige Authentifizierung. Dadurch wird die Identität des Benutzers mit dem registrierten Gerät verknüpft, das für den Zugriff auf die Ressource verwendet wird. Dadurch wird eine sicherere Überprüfung der Verbund Identität angeboten, bevor auf geschützte Ressourcen zugegriffen wird.

        > [!NOTE]
        > Weitere Informationen über Geräte Objekt, Geräte Registrierungsdienst, Workplace Join und das Gerät als nahtlose zweistufige Authentifizierung und einmaliges Anmelden (SSO) finden [Sie unter Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

    -   Festlegen der MFA-Anforderung für den gesamten Extranetzugriff oder bedingt basierend auf der Identität des Benutzers, dem Netzwerk Speicherort oder einem Gerät, das für den Zugriff auf geschützte Ressourcen verwendet wird.

-   Höhere Flexibilität beim Konfigurieren von Authentifizierungs Richtlinien: Sie können benutzerdefinierte Authentifizierungs Richtlinien für AD FS gesicherte Ressourcen mit unterschiedlichen Geschäftswerten konfigurieren. Beispielsweise können Sie die MFA für Anwendungen mit großem Einfluss auf das Unternehmen erforderlich machen.

-   Einfache Verwendung: einfache und intuitive Verwaltungs Tools wie das GUI-basierte MMC-Snap-in "AD FS-Verwaltung" und Windows PowerShell-Cmdlets ermöglichen IT-Administratoren das einfache Konfigurieren von Authentifizierungs Richtlinien. Mit Windows PowerShell können Sie Ihre Lösungen für die Verwendung in unterschiedlichem Umfang schreiben und alltägliche Verwaltungsaufgaben automatisieren.

-   Bessere Kontrolle über Unternehmensressourcen: da Sie als Administrator mithilfe von AD FS eine Authentifizierungs Richtlinie konfigurieren können, die für eine bestimmte Ressource gilt, können Sie besser steuern, wie Unternehmensressourcen gesichert werden. Die von IT-Administratoren angegebenen Authentifizierungsrichtlinien können von Anwendungen nicht außer Kraft gesetzt werden. Für sensible Anwendungen und Dienste können Sie für jeden Zugriff auf die Ressource die MFA-Anforderung, Geräteauthentifizierung und optional die erneute Authentifizierung aktivieren.

-   Unterstützung für benutzerdefinierte MFA-Anbieter: für Organisationen, die MFA-Methoden von Drittanbietern nutzen, bietet AD FS die Möglichkeit, diese Authentifizierungsmethoden nahtlos zu integrieren und zu verwenden.

### <a name="authentication-scope"></a>Authentifizierungsbereich
In AD FS in Windows Server 2012 R2 können Sie eine Authentifizierungs Richtlinie in einem globalen Bereich angeben, die für alle von AD FS gesicherten Anwendungen und Dienste gilt.  Sie können auch Authentifizierungs Richtlinien für bestimmte Anwendungen und Dienste (Vertrauens Stellungen der vertrauenden Seite) festlegen, die durch AD FS gesichert werden. Wenn Sie eine Authentifizierungsrichtlinie für eine bestimmte Anwendung (pro Vertrauensstellung der vertrauenden Seite) angeben, wird dadurch nicht die globale Authentifizierungsrichtlinie außer Kraft gesetzt. Wenn von der globalen Authentifizierungsrichtlinie oder der pro Vertrauensstellung der vertrauenden Seite geltenden Authentifizierungsrichtlinie die MFA angefordert wird, wird die MFA ausgelöst, wenn der Benutzer versucht, sich für diese Vertrauensstellung der vertrauenden Seite zu authentifizieren.  Die globale Authentifizierungsrichtlinie dient als Fallback für Vertrauensstellungen der vertrauenden Seite (Anwendungen und Dienste), für die keine spezielle Authentifizierungsrichtlinie konfiguriert wurde.

Eine globale Authentifizierungs Richtlinie gilt für alle vertrauenden Seiten, die durch AD FS gesichert werden. Die folgenden Einstellungen können als Teil der globalen Authentifizierungsrichtlinie konfiguriert werden:

-   Die für die primäre Authentifizierung zu verwendenden Authentifizierungsmethoden

-   Einstellungen und Methoden für die MFA

-   Angabe, ob die Geräteauthentifizierung aktiviert ist. Weitere Informationen finden Sie unter [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Authentifizierungsrichtlinien für Vertrauensstellungen der vertrauenden Seite gelten speziell bei Versuchen, auf die Vertrauensstellung der vertrauenden Seite (Anwendung oder Dienst) zuzugreifen. Als Teil der Authentifizierungsrichtlinie, die pro Vertrauensstellung der vertrauenden Seite gilt, können die folgenden Einstellungen konfiguriert werden:

-   Angabe, ob Benutzer ihre Anmeldeinformationen bei jeder Anmeldung eingeben müssen

-   MFA-Einstellungen auf Grundlage von Benutzer/Gruppe, Geräteregistrierung und Standortdaten der Zugriffsanforderung

### <a name="primary-and-additional-authentication-methods"></a>Primäre Authentifizierungsmethode und zusätzliche Authentifizierungsmethoden
Mit AD FS in Windows Server 2012 R2 können Administratoren zusätzlich zum primären Authentifizierungsmechanismus weitere Authentifizierungsmethoden konfigurieren. Primäre Authentifizierungsmethoden sind integriert und dienen zum Überprüfen der Benutzer Identitäten. Sie können zusätzliche Authentifizierungsfaktoren konfigurieren, um anzufordern, dass weitere Informationen zur Identität des Benutzers bereitgestellt werden, und somit eine stärkere Authentifizierung sicherzustellen.

Mit der primären Authentifizierung in AD FS in Windows Server 2012 R2 haben Sie die folgenden Optionen:

-   Für Ressourcen, die für den Zugriff von außerhalb des Unternehmensnetzwerks veröffentlicht wurden, wird automatisch die Formularauthentifizierung aktiviert. Darüber hinaus können Sie auch die Zertifikatauthentifizierung aktivieren (d. h. Smartcard-basierte Authentifizierung oder Benutzerclientzertifikat-Authentifizierung, die mit AD DS verwendet werden kann).

-   Für Intranetressourcen ist automatisch die Windows-Authentifizierung aktiviert. Sie können zusätzlich die Formular- und/oder die Zertifikatauthentifizierung aktivieren.

Durch die Auswahl mehrerer Authentifizierungsmethoden können Ihre Benutzer wählen, mit welcher Methode sie sich auf der Anmeldeseite für Ihre Anwendung oder Ihren Dienst authentifizieren.

Sie können auch die Geräteauthentifizierung für die nahtlose zweistufige Authentifizierung aktivieren. Dadurch wird die Identität des Benutzers mit dem registrierten Gerät verknüpft, das für den Zugriff auf die Ressource verwendet wird. Dadurch wird eine sicherere Überprüfung der Verbund Identität angeboten, bevor auf geschützte Ressourcen zugegriffen wird.

> [!NOTE]
> Weitere Informationen über Geräte Objekt, Geräte Registrierungsdienst, Workplace Join und das Gerät als nahtlose zweistufige Authentifizierung und einmaliges Anmelden (SSO) finden [Sie unter Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Wenn Sie die Windows-Authentifizierung (Standardoption) für Ihre Intranetressourcen festlegen, werden Authentifizierungsanforderungen in Browsern, die die Windows-Authentifizierung unterstützen, nahtlos dieser Methode unterzogen.

> [!NOTE]
> Die Windows-Authentifizierung wird nicht in allen Browsern unterstütz. Der Authentifizierungsmechanismus in AD FS in Windows Server 2012 R2 erkennt den Browser Benutzer-Agent des Benutzers und verwendet eine konfigurierbare Einstellung, um zu bestimmen, ob der Benutzer-Agent die Windows-Authentifizierung unterstützt. Administratoren können diese Liste der Benutzer-Agents (über den Windows PowerShell-Befehl `Set-AdfsProperties -WIASupportedUserAgents`) ergänzen, um alternative Zeichenfolgen des Benutzer-Agenten für Browser anzugeben, die die Windows-Authentifizierung unterstützen. Wenn die Windows-Authentifizierung vom Benutzer-Agent des Clients nicht unterstützt wird, ist die Standardfall backmethode die Formular Authentifizierung.

### <a name="configuring-mfa"></a>Konfigurieren der MFA
Die Konfiguration der MFA in AD FS in Windows Server 2012 R2 besteht aus zwei Teilen: Angeben der Bedingungen, unter denen MFA erforderlich ist, und Auswählen einer zusätzlichen Authentifizierungsmethode. Weitere Informationen zu zusätzlichen Authentifizierungsmethoden finden Sie unter [Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md).

**MFA-Einstellungen**

Für MFA-Einstellungen (Bedingungen, unter denen die MFA erforderlich ist) stehen folgende Optionen zur Verfügung:

-   Sie können die MFA für bestimmte Benutzer und Gruppen in der AD-Domäne anfordern, der Ihr Verbundserver angehört.

-   Sie können die MFA für registrierte (mit dem Arbeitsplatz verbundene) oder nicht registrierte (nicht mit dem Arbeitsplatz verbundene) Geräte anfordern.

    Windows Server 2012 R2 verwendet einen benutzerorientierten Ansatz für moderne Geräte, bei denen Geräte Objekte eine Beziehung zwischen user@device und einem Unternehmen darstellen. Geräte Objekte sind eine neue Klasse in AD in Windows Server 2012 R2, die verwendet werden kann, um eine Verbund Identität beim Zugriff auf Anwendungen und Dienste bereitzustellen. Mit dem Geräteregistrierungsdienst (Device Registration Service, DRS), einer neuen Komponente in AD FS, wird eine Geräteidentität in Active Directory bereitgestellt und ein Zertifikat auf dem Gerät des Verbrauchers festgelegt, mit dem die Geräteidentität dargestellt wird. Mithilfe dieser Geräteidentität kann das Gerät anschließend mit dem Arbeitsplatz verbunden werden, d. h. zwischen dem persönlichen Gerät und dem Active Directory Ihres Arbeitsplatzes wird eine Verbindung hergestellt. Wenn Sie Ihr persönliches Gerät mit dem Arbeitsplatz verbinden, wird es zu einem bekannten Gerät und stellt die nahtlose zweistufige Authentifizierung für geschützte Arbeitsplatzressourcen und -anwendung bereit. Anders ausgedrückt: Nachdem ein Gerät mit dem Arbeitsplatz verbunden ist, ist die Identität des Benutzers an dieses Gerät gebunden und kann für eine nahtlose zusammengesetzte Identitätsüberprüfung verwendet werden, bevor auf eine geschützte Ressource zugegriffen wird.

    Weitere Informationen zum Arbeitsplatz Beitritt und zum Verlassen des Arbeitsbereichs finden [Sie unter Verbinden mit Workplace von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

-   Sie können die MFA verlangen, wenn die Zugriffsanforderung für die geschützten Ressourcen über das Extranet oder das Intranet erfolgt.

## <a name="scenario-overview"></a><a name="BKMK_2"></a>Szenarioübersicht
In diesem Szenario aktivieren Sie die MFA auf Grundlage der Gruppen Mitgliedschafts Daten eines Benutzers für eine bestimmte Anwendung. In anderen Worten: Sie richten eine Authentifizierungsrichtlinie auf dem Verbundserver so ein, dass die MFA erforderlich ist, wenn Benutzer aus einer bestimmten Gruppe Zugriff auf eine spezielle auf einem Webserver gehostete Anwendung anfordern.

Genauer gesagt aktivieren Sie in diesem Szenario eine Authentifizierungsrichtlinie für eine anspruchsbasierte Testanwendung namens **claimapp**. Dabei muss der AD-Benutzer **Robert Hatley** die MFA durchlaufen, da er zur AD-Gruppe **Finance** gehört.

Die Schritt-für-Schritt-Anweisungen zum Einrichten und überprüfen dieses Szenarios finden Sie unter Exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md). Um die Schritte in dieser exemplarischen Vorgehensweise ausführen zu können, müssen Sie eine Lab-Umgebung einrichten und die Schritte unter [Einrichten der Lab-Umgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)ausführen.

Weitere Szenarien zum Aktivieren der MFA in AD FS sind:

-   Aktivieren der MFA, falls die Zugriffsanforderung über das Extranet erfolgt. Sie können den Code ändern, der im Abschnitt "Einrichten der MFA-Richtlinie" unter Exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit folgendem Code dargestellt wird:

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   Aktivieren der MFA, falls die Zugriffsanforderung über ein Gerät erfolgt, das nicht mit dem Arbeitsplatz verbunden ist.  Sie können den Code ändern, der im Abschnitt "Einrichten der MFA-Richtlinie" unter Exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit folgendem Code dargestellt wird:

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   Aktivieren der MFA, falls ein Benutzer über ein Gerät zugreifen möchte, das mit dem Arbeitsplatz verbunden, aber nicht für diesen Benutzer registriert ist. Sie können den Code ändern, der im Abschnitt "Einrichten der MFA-Richtlinie" unter Exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) mit folgendem Code dargestellt wird:

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>Weitere Informationen
Leitfaden für die exemplarische Vorgehensweise [: Verwalten von Risiken mit zusätzlichen Multi-Factor Authentication für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Einrichten der Lab-Umgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



