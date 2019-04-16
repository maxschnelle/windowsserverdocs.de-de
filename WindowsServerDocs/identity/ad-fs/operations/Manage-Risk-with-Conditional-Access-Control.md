---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: Verwalten von Risiken mit Steuerung des bedingten Zugriffs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2ad7d1467abd6d69077b515b8c69a65f7e70f19
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-conditional-access-control"></a>Verwalten von Risiken mit Steuerung des bedingten Zugriffs

>Gilt für: Windows Server 2012 R2


-   [Wichtige Konzepte – bedingte Zugriffssteuerung in AD FS](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [Verwalten von Risiken mit Steuerung des bedingten Zugriffs](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="BKMK_1"></a>Wichtige Konzepte – bedingte Zugriffssteuerung in AD FS
Die allgemeine Funktion von AD FS ist, um die Ausstellung eines Zugriffstokens, das eine Gruppe von Ansprüchen enthält. Die Entscheidung, welche Ansprüche AD FS akzeptiert und anschließend ausgegeben unterliegt Anspruchsregeln.

Zugriffssteuerung in AD FS wird implementiert, mit Anspruchsregeln ausstellungsautorisierung, mit denen Zulassungs- oder verweigern Ansprüche, die bestimmt, ob ein Benutzer oder eine Gruppe von Benutzern auf AD FS-gesicherte Ressourcen zugreifen, oder nicht zulässig. Autorisierungsregeln können nur für Vertrauensstellungen der vertrauenden Seite festgelegt werden.

|Regeloption|Regellogik|
|---------------|--------------|
|Alle Benutzer zulassen|Wenn der eingehende Anspruchstyp dem *beliebigen Anspruchstyp* und der Wert einem *einen beliebigen Wert*, dann Problem Anspruch ausstellungsanspruch mit Wert *zulassen*|
|Benutzer mit diesem eingehenden Anspruch Zugriff gewähren|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, dann Problem Anspruch ausstellungsanspruch mit Wert *zulassen*|
|Benutzern mit diesem eingehenden Anspruch Zugriff verweigern|Wenn der eingehende Anspruchstyp dem *angegebenen Anspruchstyp* und der Wert einem *angegebenen Anspruchswert*, dann Problem Anspruch ausstellungsanspruch mit Wert *verweigern*|

Weitere Informationen zu diesen Regeloptionen und zur Logik finden Sie unter [Wann sollte eine Autorisierungsanspruchsregel verwendet](https://technet.microsoft.com/library/ee913560.aspx).

In AD FS unter Windows Server2012 R2 wurde die Zugriffssteuerung durch mehrere Faktoren, einschließlich Benutzer, Gerät, Standort und Authentifizierungsdaten verbessert. Dies wird durch eine größere Auswahl von Anspruchstypen für die autorisierungsanspruchsregeln verfügbaren ermöglicht.  Erzwingen Sie also in AD FS unter Windows Server2012 R2, Steuerung des bedingten Zugriffs basierend auf Benutzer Benutzeridentität oder der Gruppenmitgliedschaft, Netzwerkadresse, Gerät (an, ob es mit dem Arbeitsplatz verbundene, Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)), und Authentifizierungsstatus (ob mehrstufige Authentifizierung (MFA) ausgeführt wurde).

Steuerung des bedingten Zugriffs in AD FS unter Windows Server2012 R2 bietet die folgenden Vorteile:

-   Flexible und deutliche pro Anwendung Autorisierungsrichtlinien, bei dem Sie zulassen oder Verweigern des Zugriffs basierend auf Benutzer, Gerät, Netzwerkadresse und Authentifizierungsstatus können

-   Erstellen von Ausstellungsautorisierungsregeln für Anwendungen der vertrauenden Seite

-   Rich-UI-Oberfläche für die allgemeinen Szenarien der bedingten Zugriffssteuerung

-   Umfassende anspruchssprachen und Windows PowerShell-Unterstützung für erweiterte Szenarien der bedingten Zugriffssteuerung

-   Benutzerdefinierte (pro vertrauende Seite Anwendung) Nachrichten "Zugriff verweigert". Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx). Durch die Möglichkeit, diese Meldungen angepasst, können Sie erläutern, warum ein Benutzer Zugriff verweigert wird und auch Self-Service-Wiederherstellung, wo es möglich ist, ist z.B. Benutzer auffordern, Arbeitsplatz auf ihren Geräten beitreten, erleichtern. Weitere Informationen finden Sie unter [Verbinden mit einem Arbeitsplatz von einem beliebigen Gerät für SSO und nahtlose zweistufige Authentifizierung über Unternehmensanwendungen](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md).

Die folgende Tabelle enthält Anspruchstypen in AD FS verfügbar in Windows Server2012 R2 für die Implementierung der bedingten Zugriffssteuerung verwendet werden.

|Typ des Anspruchs|Beschreibung|
|--------------|---------------|
|E-Mail-Adresse|Die E-Mail-Adresse des Benutzers.|
|Vorname|Der Vorname des Benutzers.|
|Name|Der eindeutige Name des Benutzers,|
|UPN|Der Benutzerprinzipalname (UPN) des Benutzers.|
|Allgemeiner Name|Der allgemeine Name des Benutzers.|
|AD FS 1.x E-Mail-Adresse|Die E-Mail-Adresse des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0.|
|Gruppe|Eine Gruppe, der der Benutzer Mitglied ist.|
|AD FS x UPN|Der UPN des Benutzers bei der Interaktion mit AD FS 1.1 oder AD FS 1.0.|
|Rolle|Eine Rolle, die der Benutzer verfügt.|
|Nachname|Der Nachname des Benutzers.|
|PPID|Private ID des Benutzers.|
|Name-ID|SAML-Namensbezeichner des Benutzers.|
|Zeitstempel der Authentifizierung|Zum Anzeigen der Uhrzeit und Datum, an dem der Benutzer authentifiziert wurde.|
|Authentifizierungsmethode|Die Methode zum Authentifizieren des Benutzers verwendet.|
|Nur Gruppen-SID verweigern|Die "nur verweigern" Gruppen-SID des Benutzers.|
|Nur primäre SID verweigern|"Nur verweigern" primäre SID des Benutzers.|
|Nur primäre Gruppen-SID verweigern|"Nur verweigern" primäre Gruppen-SID des Benutzers.|
|Gruppen-SID|Die Gruppen-SID des Benutzers.|
|Primäre Gruppen-SID|Primäre Gruppen-SID des Benutzers.|
|Primäre SID|Die primäre SID des Benutzers.|
|Windows-Kontoname|Domänenkontenname des Benutzers in der Form %% amp;quot;Domäne\Benutzer%%amp;quot.|
|Ist registrierter Benutzer|Benutzer ist registriert, um dieses Gerät zu verwenden.|
|Geräte-ID|Der Bezeichner des Geräts.|
|Geräteregistrierungsbezeichner|Der Bezeichner für die Geräteregistrierung.|
|Geräteregistrierungs-Anzeigename|Der Anzeigename der Geräteregistrierung.|
|Geräte-BS-Typ|Betriebssystem-Typ des Geräts.|
|Betriebssystemversion des Geräts|Die Betriebssystemversion des Geräts.|
|Ist verwaltetes Gerät|Gerät wird von einem Verwaltungsdienst verwaltet.|
|Weitergeleitete Client-IP-|IP-Adresse des Benutzers.|
|Client-Anwendung|Typ der Clientanwendung.|
|Client-Agent für Benutzer|Typ des Geräts vom Client wird verwendet, auf die Anwendung zugreifen.|
|Client-IP-|IP-Adresse des Clients.|
|Endpunkt-Pfad|Absoluter endpunktpfad zum Bestimmen von aktiven bzw. passiven Clients verwendet werden kann.|
|Proxy|DNS-Name des Verbundserverproxys, die die Anforderung übergeben.|
|Bezeichner der Anwendung|Bezeichner für die vertrauende Seite.|
|Anwendungsrichtlinien|Anwendungsrichtlinien des Zertifikats.|
|Zertifizierungsstellenschlüssel-ID|Die Autorität für die Schlüssel-ID-Erweiterung des Zertifikats, das ein ausgestelltes Zertifikat signiert.|
|Grundlegende Einschränkung|Eine der basiseinschränkungen des Zertifikats.|
|Erweiterte Schlüsselverwendung|Beschreibt einen der erweiterten Schlüsselverwendungen des Zertifikats.|
|Aussteller|Der Name der Zertifizierungsstelle, die das x. 509-Zertifikat ausgestellt hat.|
|Namen des Herausgebers|Der distinguished Name des Zertifikatausstellers.|
|Schlüsselverwendung|Eine der Schlüsselverwendungen des Zertifikats.|
|Nicht nach|Das Datum in Ortszeit nach dem ein Zertifikat nicht mehr gültig ist.|
|Nicht vor|Das Datum in der lokalen Zeit auf dem ein Zertifikat gültig ist.|
|Richtlinien für Rechtekontozertifikate|Die Richtlinien unter denen das Zertifikat ausgestellt wurde.|
|Öffentlicher Schlüssel|Öffentliche Schlüssel des Zertifikats.|
|Zertifikatrohdaten|Die Rohdaten des Zertifikats.|
|Alternativer Antragstellername|Einer der alternativen Namen des Zertifikats.|
|Seriennummer|Die Seriennummer des Zertifikats.|
|Signaturalgorithmus|Der Algorithmus, der zum Erstellen der Signatur eines Zertifikats verwendet wird.|
|Betreff|Der Antragsteller des Zertifikats.|
|Schlüsselkennung des Antragstellers|Schlüsselkennung des Antragstellers des Zertifikats.|
|Antragstellername|Definierter Antragstellername aus einem Zertifikat.|
|V2-Vorlagenname|Der Name der Zertifikatvorlage Version 2 verwendet Wen ausstellen oder Erneuern eines Zertifikats. Dies ist ein Microsoft-spezifischen Wert.|
|V1-Vorlagenname|Der Name der Zertifikatvorlage Version 1 beim Ausstellen oder Erneuern eines Zertifikats verwendet. Dies ist ein Microsoft-spezifischen Wert.|
|Fingerabdruck|Fingerabdruck des Zertifikats.|
|X 509-Version|Die x. 509-Formatversion des Zertifikats.|
|Innerhalb des Unternehmensnetzwerks|Verwendet, um anzugeben, ob eine Anforderung von innerhalb des Unternehmensnetzwerks stammen.|
|Zeitpunkt des Kennwortablaufs|Verwendet, um die Uhrzeit anzuzeigen, das Kennwort abläuft.|
|Tage bis zum Kennwortablauf|Wird verwendet, um die Anzahl der Tage zum Kennwortablauf anzuzeigen.|
|Kennwortaktualisierungs-URL|Wird verwendet, um die Webadresse des kennwortaktualisierungsdiensts anzuzeigen.|
|Authentifizierungsmethodenreferenzen|Verwendet al Authentifizierungsmethoden verwendet zur Authentifizierung des Benutzers anzuzeigen.|

## <a name="BKMK_2"></a>Verwalten von Risiken mit Steuerung des bedingten Zugriffs
Mithilfe der verfügbaren Einstellungen werden in der Sie Risiken durch die Implementierung der bedingten Zugriffssteuerung verwaltet.

### <a name="common-scenarios"></a>Allgemeine Szenarien
Angenommen Sie, ein einfaches Szenario Implementierung der bedingten Zugriffssteuerung auf Grundlage der Gruppenmitgliedschaftsdaten des Benutzers, für eine bestimmte Anwendung (Vertrauensstellung einer vertrauenden Seite). In anderen Worten: Sie können richten Sie eine ausstellungsautorisierungsregel auf dem Verbundserver, Benutzer zu gestatten, die einer bestimmten Gruppe in Ihrer AD gehören Domänenzugriff auf eine bestimmte Anwendung, die von AD FS geschützt ist.  Die ausführlichen Schritte (mit der Benutzeroberfläche und Windows PowerShell) zum Implementieren dieses Szenarios werden in behandelt [Walkthrough Guide: Manage Risk with Conditional Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md). Um die Schrittein dieser exemplarischen Vorgehensweise abzuschließen, müssen Sie eine Testumgebung einrichten und führen Sie die Schrittein [Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md).

### <a name="advanced-scenarios"></a>Erweiterte Szenarien
Weitere Beispiele für das Implementieren der Steuerung des bedingten Zugriffs in AD FS unter Windows Server2012 R2 umfassen Folgendes:

-   Ermöglicht den Zugriff auf eine Anwendung, die von AD FS geschützt werden, nur dann, wenn die Identität des Benutzers mit der MFA bestätigt wurde

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Ermöglicht den Zugriff auf eine Anwendung, die von AD FS geschützt werden, nur dann, wenn die Zugriffsanforderung von einem Arbeitsplatz verbundenen Gerät, die registriert ist für den Benutzer

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Ermöglicht den Zugriff auf eine Anwendung, die von AD FS geschützt werden, nur zu, wenn die Zugriffsanforderung von einem Arbeitsplatz verbundenen Gerät, die registriert ist für einen Benutzer, dessen Identität mit der MFA bestätigt wurde

    Sie können den folgenden Code verwenden.

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Erlauben Sie Extranet-Zugriff auf eine Anwendung, die von AD FS geschützt werden, nur dann, wenn die Zugriffsanforderung von einem Benutzer stammt, dessen Identität mit der MFA bestätigt wurde.

    Sie können den folgenden Code verwenden:

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>Siehe auch
[Handbuch mit exemplarischer Vorgehensweise: Verwalten von Risiken mit der bedingten Zugriffssteuerung](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)<ph x="2">
</ph>[Einrichten der Testumgebung für AD FS unter Windows Server2012 R2](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



