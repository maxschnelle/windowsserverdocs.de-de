---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: Verwalten von Risiken mit der bedingten Zugriffssteuerung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 719c8ad0b39ccb4e252243e64385b12f8dbe6a28
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816223"
---
# <a name="manage-risk-with-conditional-access-control"></a>Verwalten von Risiken mit der bedingten Zugriffssteuerung




-   [Schlüsselkonzepte: bedingte Zugriffs Steuerung in AD FS](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Verwalten von Risiken mit bedingtem Access Control](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="key-concepts---conditional-access-control-in-ad-fs"></a><a name="BKMK_1"></a>Schlüsselkonzepte: bedingte Zugriffs Steuerung in AD FS
Die allgemeine Funktion von AD FS besteht darin, ein Zugriffs Token auszugeben, das einen Satz von Ansprüchen enthält. Die Entscheidung bezüglich der Ansprüche, die AD FS akzeptiert und dann Probleme behandelt, unterliegt den Anspruchs Regeln.

Die Zugriffs Steuerung in AD FS wird mit Anspruchs Regeln für Ausstellungs Autorisierung implementiert, mit denen Zulassungs-oder Verweigerungs Ansprüche ausgegeben werden, die bestimmen, ob ein Benutzer oder eine Gruppe von Benutzern auf AD FS gesicherte Ressourcen zugreifen darf. Autorisierungsregeln können nur für Vertrauensstellungen der vertrauenden Seite festgelegt werden.

|Regeloption|Regellogik|
|---------------|--------------|
|Alle Benutzer zulassen|Wenn der Typ des eingehenden Anspruchs einem *beliebigen Anspruchstyp* und der Wert einem *beliebigen Wert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|
|Benutzern mit diesem eingehenden Anspruch Zugriff gewähren|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|
|Benutzern mit diesem eingehenden Anspruch Zugriff verweigern|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert* entspricht, wird der Ausstellungsanspruch mit Wert auf *Verweigern* festgelegt.|

Weitere Informationen zu diesen Regeloptionen und der entsprechenden Logik finden Sie unter [Verwendung einer Autorisierungsanspruchsregel](https://technet.microsoft.com/library/ee913560.aspx).

In AD FS in Windows Server 2012 R2 wurde die Zugriffs Steuerung durch mehrere Faktoren erweitert, einschließlich Benutzer-, Geräte-, Standort-und Authentifizierungsdaten. Dies wird durch eine größere Vielfalt an für die Autorisierungsanspruchsregeln verfügbaren Anspruchstypen ermöglicht.  Anders ausgedrückt: in AD FS in Windows Server 2012 R2 können Sie die bedingte Zugriffs Steuerung basierend auf der Benutzeridentität oder der Gruppenmitgliedschaft, dem Netzwerk Speicherort und dem Gerät (mit dem Arbeitsplatz Beitritt) erzwingen. Weitere Informationen finden Sie unter [Verbinden mit Workplace von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Die bedingte Zugriffs Steuerung in AD FS in Windows Server 2012 R2 bietet die folgenden Vorteile:

-   Flexible und deutliche Autorisierungsrichtlinien pro Anwendung, wodurch der Zugriff basierend auf Benutzer, Gerät, Netzwerkadresse und Authentifizierungsstatus zugelassen oder verweigert werden kann

-   Erstellen von Ausstellungsautorisierungsregeln für Anwendungen der vertrauenden Seite

-   Komfortable Benutzeroberfläche für die allgemeinen Szenarien der bedingten Zugriffssteuerung

-   Umfassende Unterstützung von Anspruchssprachen und Windows PowerShell für erweiterte Szenarien der bedingten Zugriffssteuerung

-   Benutzerdefinierte Meldung "Zugriff verweigert" (pro Anwendung der vertrauenden Seite). Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx). Da diese Meldungen angepasst werden können, können Sie erläutern, warum einem Benutzer der Zugriff verweigert wird und außerdem die eigenständige Wartung dort vereinfachen, wo es möglich ist. Fordern Sie beispielsweise Benutzer dazu auf, eine Verbindung zwischen ihren Geräten und dem Arbeitsplatz herzustellen. Weitere Informationen finden Sie unter [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

In der folgenden Tabelle sind alle in AD FS in Windows Server 2012 R2 verfügbaren Anspruchs Typen enthalten, die für die Implementierung der bedingten Zugriffs Steuerung verwendet werden können.

|Anspruchstyp|Beschreibung|
|--------------|---------------|
|E-Mail-Adresse|E-Mail-Adresse des Benutzers|
|Vorname|Angegebener Name des Benutzers|
|Name|Eindeutiger Name des Benutzers|
|UPN|Prinzipalname (UPN) des Benutzers|
|Allgemeiner Name|Allgemeiner Name des Benutzers|
|AD FS 1.x-E-Mail-Adresse|Die E-Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|
|Gruppe|Eine Gruppe, in der der Benutzer Mitglied ist|
|AD FS 1.x UPN|UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|
|Rolle|Eine Rolle, über die der Benutzer verfügt.|
|Nachname|Nachname des Benutzers|
|PPID|Private ID des Benutzers|
|Namens-ID|SAML-Namensbezeichner des Benutzers|
|Zeitstempel der Authentifizierung|Wird zum Anzeigen der Uhrzeit und des Datums der Benutzerauthentifizierung verwendet|
|Authentifizierungsmethode|Zur Authentifizierung des Benutzers verwendete Methode|
|Nur Gruppen-SID verweigern|Die Gruppen-SID %%amp;quot;Nur verweigern%%amp;quot; des Benutzers|
|Nur primäre SID verweigern|Die primäre SID %%amp;quot;Nur verweigern%%amp;quot; des Benutzers|
|Nur primäre Gruppen-SID verweigern|Die primäre Gruppen-SID %%amp;quot;Nur verweigern%%amp;quot; des Benutzers|
|Gruppen-SID|Die Gruppen-SID des Benutzers|
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers|
|Primäre SID|Primäre SID des Benutzers|
|Windows-Kontoname|Domänenkontenname des Benutzers in der Form %%amp;quot;Domäne\Benutzer%%amp;quot;.|
|Ist registrierter Benutzer|Benutzer ist für die Verwendung dieses Geräts registriert|
|Gerätebezeichner|Bezeichner des Geräts|
|Geräteregistrierungsbezeichner|Bezeichner für die Geräteregistrierung|
|Geräteregistrierungs-Anzeigename|Anzeigename der Geräteregistrierung|
|Geräte-BS-Typ|BS-Typ des Geräts|
|Geräte-BS-Version|Betriebssystemversion des Geräts|
|Ist verwaltetes Gerät|Gerät wird von einem Verwaltungsdienst verwaltet|
|Weitergeleitete Client-IP|IP-Adresse des Benutzers|
|Clientanwendung|Typ der Clientanwendung|
|Client-Benutzer-Agent|Gerätetyp, mit dem vom Client auf die Anwendung zugegriffen wird|
|Client-IP|IP-Adresse des Clients|
|Endpunktpfad|Absoluter Endpunktpfad, der zum Bestimmen von aktiven bzw. passiven Clients verwendet werden kann|
|Proxy|DNS-Name des Verbundserverproxys, von dem die Anforderung übergeben wurde|
|Anwendungsbezeichner|Bezeichner für die vertrauende Seite|
|Anwendungsrichtlinien|Anwendungsrichtlinien des Zertifikats|
|Zertifizierungsstellenschlüssel-ID|Erweiterung der Zertifizierungsstellenschlüssel-ID des Zertifikats, von dem ein ausgestelltes Zertifikat signiert wurde|
|Basiseinschränkung|Eine der Basiseinschränkungen des Zertifikats|
|Erweiterte Schlüsselverwendung|Beschreibt eine der erweiterten Schlüsselverwendungen des Zertifikats|
|Aussteller|Der Name der Zertifizierungsstelle, die das X.509-Zertifikat ausgestellt hat|
|Ausstellername|Definierter Name des Zertifikatausstellers|
|Schlüsselverwendung|Eine der Schlüsselverwendungen des Zertifikats|
|Nicht nach|Datum (lokale Zeit), nach dem ein Zertifikat nicht mehr gültig ist|
|Nicht vor|Datum (lokale Zeit), ab dem ein Zertifikat gültig ist|
|Zertifikatrichtlinien|Die bei der Zertifikatausstellung gültigen Richtlinien|
|Öffentlicher Schlüssel|Öffentlicher Schlüssel des Zertifikats|
|Zertifikatrohdaten|Rohdaten des Zertifikats|
|Alternativer Antragstellername|Einer der alternativen Namen des Zertifikats|
|Seriennummer|Seriennummer des Zertifikats|
|Signaturalgorithmus|Zum Erstellen der Signatur eines Zertifikats verwendeter Algorithmus|
|Subject (Antragsteller)|Antragsteller des Zertifikats|
|Schlüsselkennung des Antragstellers|Schlüsselkennung des Antragstellers des Zertifikats|
|Antragstellername|Definierter Antragstellername aus einem Zertifikat|
|V2-Vorlagenname|Name der Zertifikatvorlage Version 2, die beim Ausstellen oder Erneuern eines Zertifikats verwendet wird. Dies ist ein Microsoft-spezifischer Wert.|
|V1-Vorlagenname|Name der Zertifikatvorlage Version 1, die beim Ausstellen oder Erneuern eines Zertifikats verwendet wird. Dies ist ein Microsoft-spezifischer Wert.|
|Fingerabdruck|Fingerabdruck des Zertifikats.|
|X.509-Version|X.509-Formatversion des Zertifikats|
|Innerhalb des Unternehmensnetzwerks|Wird verwendet, um anzuzeigen, ob eine Anforderung aus dem Unternehmensnetzwerk stammt|
|Zeitpunkt des Kennwortablaufs|Zeigt den Zeitpunkt an, zu dem das Kennwort abläuft|
|Tage bis zum Kennwortablauf|Zeigt die Anzahl der Tage bis zum Ablauf des Kennworts an|
|Kennwortaktualisierungs-URL|Zeigt die Webadresse des Kennwortaktualisierungsdiensts an|
|Authentifizierungsmethodenreferenzen|Gibt alle Authentifizierungsmethoden an, die zum Authentifizieren des Benutzers verwendet werden|

## <a name="managing-risk-with-conditional-access-control"></a><a name="BKMK_2"></a>Verwalten von Risiken mit bedingtem Access Control
Mithilfe der verfügbaren Einstellungen können Risiken durch Implementierung der bedingten Zugriffssteuerung verwaltet werden.

### <a name="common-scenarios"></a>Allgemeine Szenarien
Stellen Sie sich z. b. ein einfaches Szenario für die Implementierung der bedingten Zugriffs Steuerung auf Grundlage der Gruppen Mitgliedschafts Daten eines Benutzers für eine bestimmte Anwendung (Vertrauensstellung der vertrauenden Seite) vor. Anders ausgedrückt: Sie können eine Ausstellungs Autorisierungs Regel auf dem Verbund Server einrichten, um Benutzern, die einer bestimmten Gruppe in Ihrer AD-Domäne angehören, Zugriff auf eine bestimmte Anwendung zu gewähren, die durch AD FS gesichert ist.  Die ausführlichen Schritte (auf der Benutzeroberfläche und mit Windows PowerShell) zum Implementieren dieses Szenarios werden unter [Walkthrough Guide: Manage Risk with Conditional Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)behandelt. Um die Schritte in dieser exemplarischen Vorgehensweise ausführen zu können, müssen Sie eine Lab-Umgebung einrichten und die Schritte unter [Einrichten der Lab-Umgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)ausführen.

### <a name="advanced-scenarios"></a>Erweiterte Szenarien
Weitere Beispiele für die Implementierung der bedingten Zugriffs Steuerung in AD FS in Windows Server 2012 R2:

-   Gewähren Sie den Zugriff auf eine durch AD FS gesicherte Anwendung nur dann, wenn die Identität dieses Benutzers mit MFA bestätigt wurde.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Gewähren Sie den Zugriff auf eine durch AD FS gesicherte Anwendung nur dann, wenn die Zugriffs Anforderung von einem mit dem Arbeitsplatz verbundenen Gerät stammt, das für den Benutzer registriert ist.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Gewähren Sie den Zugriff auf eine durch AD FS gesicherte Anwendung nur dann, wenn die Zugriffs Anforderung von einem mit dem Arbeitsplatz verbundenen Gerät stammt, das für einen Benutzer registriert ist, dessen Identität mit der MFA bestätigt wurde.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Lassen Sie den Extranetzugriff auf eine durch AD FS gesicherte Anwendung nur zu, wenn die Zugriffs Anforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>Weitere Informationen
Leitfaden für die exemplarische Vorgehensweise [: Verwalten von Risiken mit bedingten Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)
[Einrichten der Lab-Umgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



