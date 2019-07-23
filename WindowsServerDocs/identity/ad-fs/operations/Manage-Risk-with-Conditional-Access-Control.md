---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: Verwalten von Risiken mit der bedingten Zugriffssteuerung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2c399467a8bb70e723a86618aa37fc54425f4e7d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189047"
---
# <a name="manage-risk-with-conditional-access-control"></a>Verwalten von Risiken mit der bedingten Zugriffssteuerung




-   [Wichtige Konzepte – bedingte Zugriffssteuerung in AD FS](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="BKMK_1"></a>Wichtige Konzepte – bedingte Zugriffssteuerung in AD FS
Die allgemeine Funktion von AD FS ist ein Zugriffstoken ausstellen, die einen Satz von Ansprüchen enthält. Die Entscheidung, welche Ansprüche, die AD FS akzeptiert und gibt dann unterliegt Anspruchsregeln.

Zugriffssteuerung in AD FS wird implementiert, mit der Ausstellung von Anspruchsregeln, die verwendet werden, um die Ausstellung eines Zulassungs- oder verweigerungsansprüche, der bestimmt, ob ein Benutzer oder eine Gruppe von Benutzern werden auf AD FS-gesicherte Ressourcen oder nicht zugreifen darf. Autorisierungsregeln können nur für Vertrauensstellungen der vertrauenden Seite festgelegt werden.

|Regeloption|Regellogik|
|---------------|--------------|
|Alle Benutzer zulassen|Wenn der Typ des eingehenden Anspruchs einem *beliebigen Anspruchstyp* und der Wert einem *beliebigen Wert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|
|Benutzern mit diesem eingehenden Anspruch Zugriff gewähren|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*entspricht, wird der Ausstellungsanspruch mit Wert auf *Zulassen*festgelegt.|
|Benutzern mit diesem eingehenden Anspruch Zugriff verweigern|Wenn der Typ des eingehenden Anspruchs einem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert* entspricht, wird der Ausstellungsanspruch mit Wert auf *Verweigern* festgelegt.|

Weitere Informationen zu diesen Regeloptionen und zur Logik finden Sie unter [When to Use an Authorization Claim Rule](https://technet.microsoft.com/library/ee913560.aspx).

In AD FS in Windows Server 2012 R2 wurde die Zugriffssteuerung durch mehrere Faktoren, einschließlich Benutzer, Gerät, Standort und Authentifizierungsdaten verbessert. Dies wird durch eine größere Vielfalt an für die Autorisierungsanspruchsregeln verfügbaren Anspruchstypen ermöglicht.  Das heißt, in den AD FS in Windows Server 2012 R2 können Sie erzwingen bedingte Zugriffssteuerung basierend auf Benutzer Benutzeridentität oder der Gruppenmitgliedschaft, Netzwerkadresse, Gerät (sei es Arbeitsplatz, Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem Gerät für SSO und nahtlose Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)), und der Authentifizierungsstatus (ob Multi-Factor Authentication (MFA) ausgeführt wurde).

Bedingte Zugriffssteuerung in AD FS unter Windows Server 2012 R2, bietet die folgenden Vorteile:

-   Flexible und deutliche Autorisierungsrichtlinien pro Anwendung, wodurch der Zugriff basierend auf Benutzer, Gerät, Netzwerkadresse und Authentifizierungsstatus zugelassen oder verweigert werden kann

-   Erstellen von Ausstellungsautorisierungsregeln für Anwendungen der vertrauenden Seite

-   Komfortable Benutzeroberfläche für die allgemeinen Szenarien der bedingten Zugriffssteuerung

-   Umfassende Unterstützung von Anspruchssprachen und Windows PowerShell für erweiterte Szenarien der bedingten Zugriffssteuerung

-   Benutzerdefiniert (pro vertrauender Seite der Anwendung) Nachrichten "Zugriff verweigert". Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx). Da diese Meldungen angepasst werden können, können Sie erläutern, warum einem Benutzer der Zugriff verweigert wird und außerdem die eigenständige Wartung dort vereinfachen, wo es möglich ist. Fordern Sie beispielsweise Benutzer dazu auf, eine Verbindung zwischen ihren Geräten und dem Arbeitsplatz herzustellen. Weitere Informationen finden Sie unter [Arbeitsplatzbeitritt von einem beliebigen Gerät für SSO und die nahtlose zweistufige Authentifizierung bei allen Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Die folgende Tabelle enthält Anspruchstypen in AD FS verfügbar unter Windows Server 2012 R2 für die Implementierung der bedingten Zugriffssteuerung verwendet werden soll.

|Anspruchstyp|Beschreibung|
|--------------|---------------|
|E-Mail-Adresse|E-Mail-Adresse des Benutzers|
|Angegebener Name|Angegebener Name des Benutzers|
|Name|Eindeutiger Name des Benutzers|
|UPN|Prinzipalname (UPN) des Benutzers|
|Allgemeiner Name|Allgemeiner Name des Benutzers|
|AD FS 1.x-E-Mail-Adresse|Die E-Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|
|Gruppieren|Eine Gruppe, in der der Benutzer Mitglied ist|
|AD FS 1.x UPN|UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0|
|Role-Eigenschaft|Eine Rolle, über die der Benutzer verfügt.|
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
|Antragsteller|Antragsteller des Zertifikats|
|Schlüsselkennung des Antragstellers|Schlüsselkennung des Antragstellers des Zertifikats|
|Antragstellername|Definierter Antragstellername aus einem Zertifikat|
|V2-Vorlagenname|Name der Zertifikatvorlage Version 2, die beim Ausstellen oder Erneuern eines Zertifikats verwendet wird. Dies ist ein Microsoft-spezifischer Wert.|
|V1-Vorlagenname|Name der Zertifikatvorlage Version 1, die beim Ausstellen oder Erneuern eines Zertifikats verwendet wird. Dies ist ein Microsoft-spezifischer Wert.|
|Fingerabdruck|Fingerabdruck des Zertifikats|
|X.509-Version|X.509-Formatversion des Zertifikats|
|Innerhalb des Unternehmensnetzwerks|Wird verwendet, um anzuzeigen, ob eine Anforderung aus dem Unternehmensnetzwerk stammt|
|Zeitpunkt des Kennwortablaufs|Zeigt den Zeitpunkt an, zu dem das Kennwort abläuft|
|Tage bis zum Kennwortablauf|Zeigt die Anzahl der Tage bis zum Ablauf des Kennworts an|
|Kennwortaktualisierungs-URL|Zeigt die Webadresse des Kennwortaktualisierungsdiensts an|
|Authentifizierungsmethodenreferenzen|Gibt alle Authentifizierungsmethoden an, die zum Authentifizieren des Benutzers verwendet werden|

## <a name="BKMK_2"></a>Verwalten von Risiken mit der bedingten Zugriffssteuerung
Mithilfe der verfügbaren Einstellungen können Risiken durch Implementierung der bedingten Zugriffssteuerung verwaltet werden.

### <a name="common-scenarios"></a>Allgemeine Szenarien
Angenommen Sie, ein einfaches Szenario der Implementierung der bedingten Zugriffssteuerung auf Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für eine bestimmte Anwendung (relying Party Trust). Das heißt, Sie können einrichten eine ausstellungsautorisierungsregel auf Ihrem Verbundserver, die Benutzern ermöglicht, die einer bestimmten Gruppe, in der Active Directory gehören Domänenzugriff auf eine bestimmte Anwendung, die von AD FS geschützt ist.  Die ausführlichen Schritte (mithilfe der Benutzeroberfläche und Windows PowerShell) zum Implementieren dieses Szenarios finden Sie im [Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md). Um die Schritte in dieser exemplarischen Vorgehensweise ausführen zu können, müssen Sie eine Lab-Umgebung einrichten und führen Sie die Schritte in [Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

### <a name="advanced-scenarios"></a>Erweiterte Szenarien
Weitere Beispiele für die Implementierung der bedingten Zugriffssteuerung in AD FS unter Windows Server 2012 R2: die folgenden

-   Lassen Sie den Zugriff auf eine Anwendung, die durch AD FS gesicherten, nur dann, wenn die Identität des Benutzers mit der MFA bestätigt wurde

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Lassen Sie den Zugriff auf eine Anwendung, die durch AD FS gesicherten, nur dann, wenn die zugriffsanforderung von einem aus dem Arbeitsplatz verbundenen Gerät an, das registriert wird, die dem Benutzer

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Lassen Sie den Zugriff auf eine Anwendung, die durch AD FS gesicherten, nur dann, wenn die zugriffsanforderung ein aus dem Arbeitsplatz verbundenen Gerät an, das registriert wird, wird zu einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Ermöglichen Sie extranet-Zugriff auf eine Anwendung, die durch AD FS gesicherten, nur dann, wenn die zugriffsanforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>Siehe auch
[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)
[Einrichten der testumgebung für AD FS in Windows Server 2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



