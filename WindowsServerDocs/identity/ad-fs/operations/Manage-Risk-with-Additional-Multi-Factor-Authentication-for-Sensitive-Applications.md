---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9ee275e6fe38005394cd071e9cfe9a7999350e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855891"
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen

>Gilt für: Windows Server 2012 R2


-   [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [Konfigurieren Sie zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>Inhalt dieser Anleitung
Dieses Handbuch enthält die folgenden Informationen:

-   [Authentifizierungsmechanismen in AD FS](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1) -Beschreibung der in Active Directory Federation Services (AD FS) in Windows Server 2012 R2 verfügbaren Authentifizierungsmechanismen

-   [Übersicht über das Szenario](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2) -eine Beschreibung eines Szenarios, in dem Sie Active Directory-Verbunddienste (AD FS) verwenden, um die Aktivierung von mehrstufiger Authentifizierung (MFA) basierend auf Gruppenmitgliedschaft des Benutzers.

    > [!NOTE]
    > In AD FS unter Windows Server 2012 R2 können Sie MFA auf Grundlage der Netzwerkadresse, geräteidentität und Benutzeridentität oder der Gruppenmitgliedschaft von Benutzer aktivieren.

    Ausführliche schrittweise Anweisungen zum Konfigurieren und überprüfen dieses Szenarios, finden Sie unter [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).

## <a name="BKMK_1"></a>Wichtige Konzepte – Authentifizierungsmechanismen in AD FS

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>Vorteile der Authentifizierungsmechanismen in AD FS
Active Directory-Verbunddienste (AD FS) in Windows Server 2012 R2 bietet IT-Administratoren mit einem Satz komfortablere, flexiblere Tools für die Authentifizierung von Benutzern, die auf Unternehmensressourcen zugreifen möchten. Ermöglicht es Administratoren, mit dem primären und zusätzlichen Authentifizierungsmethoden flexibel steuern, verbessert und bietet eine umfassende verwaltungsmöglichkeiten zum Konfigurieren der Authentifizierung eingestuft (sowohl über die Benutzeroberfläche und die Windows PowerShell) die Erfahrung für Endbenutzer, die Zugriff auf Anwendungen und Dienste, die von AD FS geschützt sind. Im folgenden werden einige der Vorteile beim Sichern Ihrer Anwendungen und Dienste mit AD FS unter Windows Server 2012 R2:

-   Globale Authentifizierungsrichtlinie – eine zentrale Verwaltungsfunktion, aus der IT-Administrator auswählen kann, welche Authentifizierungsmethoden verwendet werden, zum Authentifizieren von Benutzern, die basierend auf der Netzwerkadresse, die von der aus sie geschützte Ressourcen zugreifen. Dies ermöglicht Administratoren Folgendes:

    -   Erzwingen der Verwendung sichererer Authentifizierungsmethoden für Zugriffsanforderungen über das Extranet

    -   Aktivieren der Geräteauthentifizierung für nahtlose zweistufige Authentifizierung. Dies verbindet die Identität des Benutzers mit dem registrierten Gerät, das verwendet wird, auf die Ressource, daher bieten sicherere Überprüfung der Verbundidentität, bevor geschützte Ressourcen zugegriffen werden.

        > [!NOTE]
        > Weitere Informationen zu Geräteobjekt, Geräteregistrierungsdienst, Arbeitsplatzbeitritt und das Gerät als nahtlose zweistufige Authentifizierung und SSO finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung Allen Unternehmensanwendungen](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

    -   Legen Sie die MFA-Anforderung für den gesamten Extranetzugriff oder bedingt auf Grundlage der Identität des Benutzers, der Speicherort im Netzwerk oder ein Gerät, das verwendet wird, auf geschützte Ressourcen zugreifen.

-   Größere Flexibilität beim Konfigurieren von Authentifizierungsrichtlinien: Sie können benutzerdefinierte Authentifizierungsrichtlinien für AD FS-gesicherte Ressourcen mit variierenden Geschäftswerten konfigurieren. Beispielsweise können Sie die MFA für Anwendungen mit großem Einfluss auf das Unternehmen erforderlich machen.

-   Einfache Bedienung: einfachen und intuitiven Verwaltungstools wie dem GUI-basierte AD FS Management MMC-Snap-in und die Windows PowerShell-Cmdlets können IT-Administratoren relativ einfach Authentifizierungsrichtlinien konfigurieren. Mit Windows PowerShell können Sie Ihre Lösungen für die Verwendung in unterschiedlichem Umfang schreiben und alltägliche Verwaltungsaufgaben automatisieren.

-   Bessere Kontrolle über Unternehmensdaten: Da Sie als Administrator Sie AD FS verwenden können, um eine Authentifizierungsrichtlinie konfigurieren, die für eine bestimmte Ressource gilt größer verfügen steuern, wie Unternehmensressourcen gesichert werden. Die von IT-Administratoren angegebenen Authentifizierungsrichtlinien können von Anwendungen nicht außer Kraft gesetzt werden. Für sensible Anwendungen und Dienste können Sie für jeden Zugriff auf die Ressource die MFA-Anforderung, Geräteauthentifizierung und optional die erneute Authentifizierung aktivieren.

-   Unterstützung für benutzerdefinierte MFA-Anbieter: für Organisationen, Drittanbieter-MFA-Methoden zu nutzen, bietet AD FS die Möglichkeit zum nahtlosen einbinden und Verwenden dieser Authentifizierungsmethoden.

### <a name="authentication-scope"></a>Authentifizierungsbereich
In AD FS unter Windows Server 2012 R2 können Sie eine Authentifizierungsrichtlinie für einen globalen Bereich angeben, die für alle Anwendungen und Dienste, die von AD FS geschützt sind.  Sie können auch festlegen, dass Authentifizierungsrichtlinien für bestimmte Anwendungen und Dienste (Vertrauensstellungen verlassen), die von AD FS geschützt sind. Wenn Sie eine Authentifizierungsrichtlinie für eine bestimmte Anwendung (pro Vertrauensstellung der vertrauenden Seite) angeben, wird dadurch nicht die globale Authentifizierungsrichtlinie außer Kraft gesetzt. Wenn von der globalen Authentifizierungsrichtlinie oder der pro Vertrauensstellung der vertrauenden Seite geltenden Authentifizierungsrichtlinie die MFA angefordert wird, wird die MFA ausgelöst, wenn der Benutzer versucht, sich für diese Vertrauensstellung der vertrauenden Seite zu authentifizieren.  Die globale Authentifizierungsrichtlinie dient als Fallback für Vertrauensstellungen der vertrauenden Seite (Anwendungen und Dienste), für die keine spezielle Authentifizierungsrichtlinie konfiguriert wurde.

Eine globale Authentifizierungsrichtlinie gilt für alle vertrauenden Seiten, die von AD FS geschützt sind. Die folgenden Einstellungen können als Teil der globalen Authentifizierungsrichtlinie konfiguriert werden:

-   Die für die primäre Authentifizierung zu verwendenden Authentifizierungsmethoden

-   Einstellungen und Methoden für die MFA

-   Angabe, ob die Geräteauthentifizierung aktiviert ist. Weitere Informationen finden Sie unter [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Authentifizierungsrichtlinien für Vertrauensstellungen der vertrauenden Seite gelten speziell bei Versuchen, auf die Vertrauensstellung der vertrauenden Seite (Anwendung oder Dienst) zuzugreifen. Als Teil der Authentifizierungsrichtlinie, die pro Vertrauensstellung der vertrauenden Seite gilt, können die folgenden Einstellungen konfiguriert werden:

-   Angabe, ob Benutzer ihre Anmeldeinformationen bei jeder Anmeldung eingeben müssen

-   MFA-Einstellungen auf Grundlage von Benutzer/Gruppe, Geräteregistrierung und Standortdaten der Zugriffsanforderung

### <a name="primary-and-additional-authentication-methods"></a>Primäre Authentifizierungsmethode und zusätzliche Authentifizierungsmethoden
Mit AD FS unter Windows Server 2012 R2, zusätzlich zum primären Authentifizierungsmechanismus können Administratoren weitere Authentifizierungsmethoden konfigurieren. Primären Authentifizierungsmethoden sind integriert und dienen zum Überprüfen der Benutzeridentität. Sie können konfigurieren zusätzliche Authentifizierungsstufen um anzufordern, dass weitere Informationen über die Identität des Benutzers bereitgestellt werden und stellen Sie daher eine stärkere Authentifizierung sicher.

Primäre Authentifizierung in AD FS unter Windows Server 2012 R2 haben Sie die folgenden Optionen aus:

-   Für Ressourcen, die für den Zugriff von außerhalb des Unternehmensnetzwerks veröffentlicht wurden, wird automatisch die Formularauthentifizierung aktiviert. Darüber hinaus können Sie auch die Zertifikatauthentifizierung aktivieren (d. h. Smartcard-basierte Authentifizierung oder Benutzerclientzertifikat-Authentifizierung, die mit AD DS verwendet werden kann).

-   Für Intranetressourcen ist automatisch die Windows-Authentifizierung aktiviert. Sie können zusätzlich die Formular- und/oder die Zertifikatauthentifizierung aktivieren.

Durch die Auswahl mehrerer Authentifizierungsmethoden können Ihre Benutzer wählen, mit welcher Methode sie sich auf der Anmeldeseite für Ihre Anwendung oder Ihren Dienst authentifizieren.

Sie können auch die Geräteauthentifizierung für die nahtlose zweistufige Authentifizierung aktivieren. Dies verbindet die Identität des Benutzers mit dem registrierten Gerät, das verwendet wird, auf die Ressource, daher bieten sicherere Überprüfung der Verbundidentität, bevor geschützte Ressourcen zugegriffen werden.

> [!NOTE]
> Weitere Informationen zu Geräteobjekt, Geräteregistrierungsdienst, Arbeitsplatzbeitritt und das Gerät als nahtlose zweistufige Authentifizierung und SSO finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung Allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Wenn Sie die Windows-Authentifizierung (Standardoption) für Ihre Intranetressourcen festlegen, werden Authentifizierungsanforderungen in Browsern, die die Windows-Authentifizierung unterstützen, nahtlos dieser Methode unterzogen.

> [!NOTE]
> Die Windows-Authentifizierung wird nicht in allen Browsern unterstütz. Der Authentifizierungsmechanismus in AD FS unter Windows Server 2012 R2 erkennt der Browser-Benutzer-Agent des Benutzers und eine konfigurierbare Einstellung verwendet, um zu bestimmen, ob dieser Benutzer-Agent auf Windows-Authentifizierung unterstützt. Administratoren können diese Liste der Benutzer-Agents (über den Windows PowerShell-Befehl `Set-AdfsProperties -WIASupportedUserAgents`) ergänzen, um alternative Zeichenfolgen des Benutzer-Agenten für Browser anzugeben, die die Windows-Authentifizierung unterstützen. Wenn der Benutzer-Agent des Clients die Windows-Authentifizierung nicht unterstützt, ist als standardfallbackmethode die Formularauthentifizierung.

### <a name="configuring-mfa"></a>Konfigurieren der MFA
Es gibt zwei Teile, die Konfiguration der MFA in AD FS unter Windows Server 2012 R2: Angeben der Bedingungen, unter denen die MFA erforderlich ist, und wählen eine zusätzliche Authentifizierungsmethode hinzuzufügen. Weitere Informationen über zusätzliche Authentifizierungsmethoden finden Sie unter [Konfigurieren zusätzlicher Authentifizierungsmethoden für AD FS](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md).

**MFA-Einstellungen**

Für MFA-Einstellungen (Bedingungen, unter denen die MFA erforderlich ist) stehen folgende Optionen zur Verfügung:

-   Sie können die MFA für bestimmte Benutzer und Gruppen in der AD-Domäne anfordern, der Ihr Verbundserver angehört.

-   Sie können die MFA für registrierte (mit dem Arbeitsplatz verbundene) oder nicht registrierte (nicht mit dem Arbeitsplatz verbundene) Geräte anfordern.

    Windows Server 2012 R2 wird einen benutzerorientierter Ansatz auf moderne Geräte, in denen stellen Geräteobjekte eine Beziehung zwischen user@device und einem Unternehmen dar. Geräteobjekte sind eine neue Klasse in AD unter Windows Server 2012 R2, die zum Verbundidentität bei der Bereitstellung des Zugriffs auf Anwendungen und Diensten verwendet werden kann. Mit dem Geräteregistrierungsdienst (Device Registration Service, DRS), einer neuen Komponente in AD FS, wird eine Geräteidentität in Active Directory bereitgestellt und ein Zertifikat auf dem Gerät des Verbrauchers festgelegt, mit dem die Geräteidentität dargestellt wird. Mithilfe dieser Geräteidentität kann das Gerät anschließend mit dem Arbeitsplatz verbunden werden, d. h. zwischen dem persönlichen Gerät und dem Active Directory Ihres Arbeitsplatzes wird eine Verbindung hergestellt. Wenn Sie Ihr persönliches Gerät mit dem Arbeitsplatz verbinden, wird es zu einem bekannten Gerät und stellt die nahtlose zweistufige Authentifizierung für geschützte Arbeitsplatzressourcen und -anwendung bereit. Das heißt, nachdem ein Gerät dem Arbeitsplatz beigetreten ist, die Identität des Benutzers mit diesem Gerät verknüpft ist und für eine nahtlose verbundidentitätsüberprüfung verwendet werden kann, bevor eine geschützte Ressource zugegriffen wird.

    Weitere Informationen zum arbeitsplatzbeitritt und verlassen können, finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

-   Sie können die MFA verlangen, wenn die Zugriffsanforderung für die geschützten Ressourcen über das Extranet oder das Intranet erfolgt.

## <a name="BKMK_2"></a>Übersicht über das Szenario
In diesem Szenario können Sie die MFA auf Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für eine bestimmte Anwendung. In anderen Worten: Sie richten eine Authentifizierungsrichtlinie auf dem Verbundserver so ein, dass die MFA erforderlich ist, wenn Benutzer aus einer bestimmten Gruppe Zugriff auf eine spezielle auf einem Webserver gehostete Anwendung anfordern.

Genauer gesagt aktivieren Sie in diesem Szenario eine Authentifizierungsrichtlinie für eine anspruchsbasierte Testanwendung namens **claimapp**. Dabei muss der AD-Benutzer **Robert Hatley** die MFA durchlaufen, da er zur AD-Gruppe **Finance** gehört.

Schritt-Schritt-Anweisungen zum Einrichten und überprüfen dieses Szenarios finden Sie [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md). Um die Schritte in dieser exemplarischen Vorgehensweise ausführen zu können, müssen Sie eine Lab-Umgebung einrichten und führen Sie die Schritte in [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

Weitere Szenarien zum Aktivieren der MFA in AD FS umfassen Folgendes:

-   Aktivieren der MFA, falls die Zugriffsanforderung über das Extranet erfolgt. Sie können den Code im Abschnitt "Legen Sie MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) durch Folgendes:

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   Aktivieren der MFA, falls die Zugriffsanforderung über ein Gerät erfolgt, das nicht mit dem Arbeitsplatz verbunden ist.  Sie können den Code im Abschnitt "Legen Sie MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) durch Folgendes:

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   Aktivieren der MFA, falls ein Benutzer über ein Gerät zugreifen möchte, das mit dem Arbeitsplatz verbunden, aber nicht für diesen Benutzer registriert ist. Sie können den Code im Abschnitt "Legen Sie MFA-Richtlinie" [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) durch Folgendes:

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>Siehe auch
[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



