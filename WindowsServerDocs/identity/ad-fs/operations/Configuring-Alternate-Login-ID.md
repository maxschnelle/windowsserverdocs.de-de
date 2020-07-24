---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: Konfigurieren von alternativen Anmelde-ID
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0872131de7ba2a201b0a0e70fb6157b0e2706def
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958632"
---
# <a name="configuring-alternate-login-id"></a>Konfigurieren von alternativen Anmelde-ID


## <a name="what-is-alternate-login-id"></a>Was ist eine Alternative Anmelde-ID?
In den meisten Szenarien verwenden Benutzer ihren UPN (Benutzer Prinzipal Namen), um sich bei ihren Konten anzumelden. In einigen Umgebungen kann es jedoch sein, dass Benutzer aufgrund von Unternehmensrichtlinien oder lokalen Anwendungsabhängigkeiten eine andere Art von Anmeldung verwenden. 

>[!NOTE]
>Die empfohlenen Best Practices von Microsoft sind die Anpassung des UPN an die primäre SMTP-Adresse. In diesem Artikel wird der kleine Prozentsatz der Kunden behandelt, die die UPN nicht wiederherstellen können.

Sie können z. b. Ihre e-Mail-ID für die Anmeldung verwenden und sich vom UPN unterscheiden. Dies ist vor allem ein häufiges Vorkommen in Szenarien, in denen der UPN nicht Routing fähig ist. Nehmen Sie an, dass sich ein Benutzer Jane Doe mit UPN jdoe@contoso.local und e-Mail- jdoe@contoso.com Jane kennt den UPN möglicherweise nicht, da Sie Ihre e-Mail-ID für die Anmeldung immer verwendet hat. Die Verwendung einer anderen Anmelde Methode anstelle des UPN bildet eine Alternative ID. Weitere Informationen zur Erstellung des UPN finden Sie unter [Azure AD userPrincipalName Population](/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Mit Active Directory-Verbunddienste (AD FS) (AD FS) können Verbund Anwendungen, die AD FS verwenden, mithilfe der alternativen ID anmelden. Dadurch können Administratoren eine Alternative zum Standard-UPN angeben, die für die Anmeldung verwendet werden soll. AD FS unterstützt bereits die Verwendung einer beliebigen Art von Benutzer-ID, die von Active Directory Domain Services (AD DS) akzeptiert wird. Bei der Konfiguration für die Alternative ID ermöglicht AD FS Benutzern, sich mit dem konfigurierten alternativen ID-Wert anzumelden, z. h. e-Mail-ID. Mithilfe der alternativen ID können Sie SaaS-Anbieter, wie z. b. Office 365, übernehmen, ohne Ihre lokalen UPNs zu ändern. Sie ermöglicht außerdem die Unterstützung von Line-of-Business-Dienst Anwendungen mit von Kunden bereitgestellten Identitäten.

## <a name="alternate-id-in-azure-ad"></a>Alternative ID in Azure AD
Möglicherweise muss eine Organisation eine Alternative ID in den folgenden Szenarien verwenden:
1. Der lokale Domänen Name ist nicht Routing fähig, z. b.. "" Von "" in "" von "" in " jdoe@contoso.local ". Vorhandener UPN kann aufgrund lokaler Anwendungsabhängigkeiten oder Unternehmensrichtlinien nicht geändert werden. Azure AD und Office 365 erfordern, dass alle dem Azure AD Verzeichnis zugeordneten Domänen Suffixe vollständig über das Internet Routing fähig sind. 
2. Der lokale UPN ist nicht mit der e-Mail-Adresse des Benutzers identisch. um sich bei Office 365 anzumelden, verwenden Benutzer eine e-Mail-Adresse, und der UPN kann aufgrund von Einschränkungen der Organisation nicht verwendet werden.
   In den oben erwähnten Szenarios ermöglicht die Alternative ID mit AD FS Benutzern das Anmelden bei Azure AD, ohne Ihre lokalen UPNs zu ändern. 

## <a name="end-user-experience-with-alternate-login-id"></a>Endbenutzer mit alternativer Anmelde-ID
Die Endbenutzer-Benutzer Leistung variiert abhängig von der Authentifizierungsmethode, die mit der alternativen Anmelde-ID verwendet wird.  Derzeit gibt es drei verschiedene Möglichkeiten, wie eine Alternative Anmelde-ID verwendet werden kann.  Sie lauten wie folgt:

- **Reguläre Authentifizierung (Legacy)**: verwendet das Standard Authentifizierungsprotokoll.
- **Moderne Authentifizierung** : Active Directory-Authentifizierungsbibliothek (Adal)-basierte Anmeldung bei Anwendungen. Dies ermöglicht Anmelde Funktionen wie Multi-Factor Authentication (MFA), SAML-basierte Identitäts Anbieter von Drittanbietern mit Office-Client Anwendungen, Smartcard-und Zertifikat basierte Authentifizierung.
- **Hybride Hybrid Authentifizierung** : bietet alle Vorteile der modernen Authentifizierung und bietet Benutzern die Möglichkeit, mithilfe von Autorisierungs Token aus der Cloud auf lokale Anwendungen zuzugreifen.

>[!NOTE]
> Um die bestmögliche Leistung zu erzielen, empfiehlt Microsoft dringend die hybride Hybrid Authentifizierung.



## <a name="configure-alternate-logon-id"></a>Alternative Anmelde-ID konfigurieren
Mithilfe Azure AD Connect empfiehlt sich die Verwendung Azure AD Connect, um eine Alternative Anmelde-ID für Ihre Umgebung zu konfigurieren.

- Eine neue Konfiguration Azure AD Connect finden Sie unter Herstellen einer Verbindung mit Azure AD, um eine ausführliche Anleitung zum Konfigurieren alternativer ID und AD FS Farm zu erhalten.
- Informationen zum Ändern der Anmelde Methode für vorhandene Azure AD Connect Installationen finden Sie unter Ändern der Benutzer Anmelde Methode in AD FS

Wenn Azure AD Connect Details zur AD FS Umgebung bereitgestellt wird, wird automatisch geprüft, ob die richtige KB in Ihrem AD FS vorhanden ist, und AD FS für eine Alternative ID konfiguriert, einschließlich aller erforderlichen richtigen Anspruchs Regeln für Azure AD Verbund Vertrauensstellung. Es ist kein zusätzlicher Schritt erforderlich, der außerhalb des Assistenten zum Konfigurieren der alternativen ID erforderlich ist.

>[!NOTE]
> Microsoft empfiehlt die Verwendung von Azure AD Connect zum Konfigurieren einer alternativen Anmelde-ID.

### <a name="manually-configure-alternate-id"></a>Alternative ID manuell konfigurieren
Zum Konfigurieren einer alternativen Anmelde-ID müssen Sie die folgenden Aufgaben ausführen: Konfigurieren der AD FS Anspruchs Anbieter-Vertrauens Stellungen zum Aktivieren einer alternativen Anmelde-ID.

1.  Wenn Sie Server 2012r2 haben, stellen Sie sicher, dass KB2919355 auf allen AD FS Servern installiert ist. Sie können Sie über Windows Update Services herunterladen oder direkt herunterladen. 

2.  Aktualisieren Sie die AD FS Konfiguration, indem Sie das folgende PowerShell-Cmdlet auf einem der Verbund Server in der Farm ausführen (wenn Sie über eine wid-Farm verfügen, müssen Sie diesen Befehl auf dem primären AD FS Server in der Farm ausführen):

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>
```

" **Alternativen** Name" ist der LDAP-Name des Attributs, das Sie für die Anmeldung verwenden möchten.

**Lookupforest** ist die Liste der Gesamtstruktur-DNS, der Ihre Benutzer angehören.

Zum Aktivieren der alternativen Anmelde-ID-Funktion müssen Sie die Parameter "-Alternate eloginid" und "-lookupforest" mit einem gültigen Wert ungleich Null konfigurieren.

Im folgenden Beispiel aktivieren Sie alternative Anmelde-ID-Funktionen, sodass sich Ihre Benutzer mit Konten in contoso.com-und fabrikam.com-Gesamtstrukturen mit Ihrem "Mail"-Attribut bei AD FS aktivierten Anwendungen anmelden können.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
```

3. Um diese Funktion zu deaktivieren, legen Sie den Wert für beide Parameter auf NULL fest.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>Hybride moderne Authentifizierung mit alternativer ID

>[!IMPORTANT]
>Folgendes wurde nur für AD FS und nicht für Identitäts Anbieter von Drittanbietern getestet.

### <a name="exchange-and-skype-for-business"></a>Exchange und Skype for Business
Wenn Sie eine Alternative Anmelde-ID mit Exchange und Skype for Business verwenden, variiert die Benutzer Leistung abhängig davon, ob Sie HMA verwenden oder nicht.

>[!NOTE]
>Um die beste Endbenutzer Leistung zu erzielen, empfiehlt Microsoft die Verwendung der Hybriden modernen Authentifizierung.

Weitere Informationen finden Sie unter [Übersicht über die hybride moderne Authentifizierung](https://support.office.com/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d) .

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Voraussetzungen für Exchange und Skype for Business
Die folgenden Voraussetzungen müssen erfüllt sein, damit einmaliges Anmelden (SSO) mit alternativer ID erreicht wird.

- Für Exchange Online sollte die moderne Authentifizierung aktiviert sein.
- Skype for Business (SFB) Online sollte die moderne Authentifizierung aktiviert haben.
- Für Exchange lokal sollte die moderne Authentifizierung aktiviert sein.  Exchange 2013 CU19 oder Exchange 2016 CU18 und up sind auf allen Exchange-Servern erforderlich. Kein Exchange 2010 in der Umgebung.
- Für die lokale Skype for Business-Authentifizierung sollte die moderne Authentifizierung aktiviert sein.
- Sie müssen Exchange-und Skype-Clients verwenden, bei denen die moderne Authentifizierung aktiviert ist. Auf allen Servern muss der Server "SFB Server 2015 CU5" ausgeführt werden.
- Skype for Business-Clients, die modern Authentication-fähig sind
   - IOS, Android, Windows Phone
   - Der SFB 2016 (MA ist standardmäßig aktiviert, stellen Sie jedoch sicher, dass er nicht deaktiviert wurde.)
   - SFB 2013 (MA ist standardmäßig deaktiviert, stellen Sie sicher, dass MA aktiviert ist.)
   - SFB-Mac-Desktop
- Exchange-Clients, die moderne Authentifizierungs fähig sind und die Unterstützung für "altid"
    - Nur Office Pro Plus 2016





#### <a name="supported-office-version"></a>Unterstützte Office-Version

Wenn Sie Ihr Verzeichnis für einmaliges Anmelden mit alternativer ID mithilfe von Alternate-ID konfigurieren, können Sie zusätzliche Eingabe Aufforderungen für die Authentifizierung auslösen, wenn diese zusätzlichen Konfigurationen nicht abgeschlossen sind. Informationen zu möglichen Auswirkungen auf die Benutzer Darstellung mit alternativer ID finden Sie in diesem Artikel.

Mit der folgenden zusätzlichen Konfiguration wird die Benutzer Leistung erheblich verbessert, und Sie können für Benutzer mit alternativer ID in Ihrer Organisation fast null-Aufforderungen für die Authentifizierung erreichen.

##### <a name="step-1-update-to-required-office-version"></a>Schritt 1 Update auf erforderliche Office-Version
Office-Version 1712 (Build No 8827,2148) und höher hat die Authentifizierungs Logik aktualisiert, um das alternatives-ID-Szenario zu verarbeiten. Um die neue Logik nutzen zu können, müssen die Client Computer auf Office Version 1712 (Build No 8827,2148) und höher aktualisiert werden.

##### <a name="step-2-update-to-required-windows-version"></a>Schritt 2 Update auf erforderliche Windows-Version
Windows Version 1709 und höher hat die Authentifizierungs Logik aktualisiert, um das alternatives-ID-Szenario zu verarbeiten. Um die neue Logik nutzen zu können, müssen die Client Computer auf Windows, Version 1709 und höher, aktualisiert werden.

##### <a name="step-3-configure-registry-for-impacted-users-using-group-policy"></a>Schritt 3 Konfigurieren der Registrierung für betroffene Benutzer mithilfe von Gruppenrichtlinien
Die Office-Anwendungen basieren auf Informationen, die vom Verzeichnis Administrator zur Identifizierung der alternativen-ID-Umgebung übermittelt wurden. Die folgenden Registrierungsschlüssel müssen konfiguriert werden, damit Office-Anwendungen den Benutzer mit alternativer ID authentifizieren können, ohne dass zusätzliche Eingabe Aufforderungen angezeigt werden.

|Hinzu zufügende RegKey|Name, Typ und Wert von RegKey|Windows 7/8|Windows 10|Beschreibung|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER \software\microsoft\authn|DomainHint</br>REG_SZ</br>contoso.com|Erforderlich|Erforderlich|Der Wert dieses RegKey ist ein verifizierter benutzerdefinierter Domänen Name im Mandanten der Organisation. So kann z. b. der Wert contoso.com in diesem Registrierungsschlüssel von "Configuration Manager" bereitgestellt werden, wenn "contoso.com" einer der überprüften benutzerdefinierten Domänen Namen im Mandanten contoso.onmicrosoft.com ist.|
HKEY_CURRENT_USER \software\microsoft\office\16.0\common\identity|Enablealternative eidunterstützung</br>REG_DWORD</br>1|Erforderlich für Outlook 2016 ProPlus|Erforderlich für Outlook 2016 ProPlus|Der Wert dieses RegKey kann 1/0 sein, um der Outlook-Anwendung mitzuteilen, ob Sie die verbesserte Authentifizierungs Logik der alternativen ID einsetzen soll.|
HKEY_CURRENT_USER \software\microsoft\windows\currentversion\internet settings\zonemap\domains\condeso.com\sts|&#42;</br>REG_DWORD</br>1|Erforderlich|Erforderlich|Mit diesem RegKey kann der STS als vertrauenswürdige Zone in den Interneteinstellungen festgelegt werden. Bei der AD FS-Standard Bereitstellung wird empfohlen, den ADFS-Namespace zur lokalen Intranet-Zone für Internet Explorer hinzuzufügen|

## <a name="new-authentication-flow-after-additional-configuration"></a>Neuer Authentifizierungs Ablauf nach zusätzlicher Konfiguration

![Authentifizierungsfluss](media/Configure-Alternate-Login-ID/alt1a.png)

1. a: der Benutzer wird in Azure AD mithilfe der alternativen ID bereitgestellt.
   </br>b: der Verzeichnis Administrator schiebt die erforderlichen RegKey-Einstellungen auf betroffene Client Computer.
2. Der Benutzer authentifiziert sich auf dem lokalen Computer und öffnet eine Office-Anwendung.
3. Die Office-Anwendung übernimmt die Anmelde Informationen für lokale Sitzungen.
4. Die Office-Anwendung authentifiziert sich bei Azure AD mithilfe des Domänen Hinweises, der von Administrator-und lokalen
5. Azure AD authentifiziert den Benutzer erfolgreich durch Weiterleitung an den korrekten Verbund Bereich und gibt ein Token aus.

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>Anwendungen und Benutzeroberflächen nach der zusätzlichen Konfiguration

### <a name="non-exchange-and-skype-for-business-clients"></a>Nicht-Exchange-und Skype for Business-Clients

|Client|Supporthinweis|Bemerkungen|
| ----- | -----|-----|
|Microsoft Teams|Unterstützt|<li>Microsoft Teams unterstützt AD FS (SAML-P, WS-Fed, WS-Trust und OAuth) und die moderne Authentifizierung.</li><li> Wichtige Microsoft-Teams, wie z. b. Kanäle, Chats und Dateien, funktionieren mit einer alternativen Anmelde-ID.</li><li>Drittanbieter-apps müssen separat vom Kunden untersucht werden. Dies liegt daran, dass jede Anwendung über eigene Authentifizierungsprotokolle für die Unterstützung verfügt.</li>|     
|OneDrive for Business|Unterstützt-Client seitiger Registrierungsschlüssel empfohlen |Wenn eine Alternative ID konfiguriert ist, sehen Sie, dass der lokale UPN im Feld Überprüfung vorab ausgefüllt ist. Dies muss in die alternative Identität geändert werden, die verwendet wird. Es wird empfohlen, den Client seitigen Registrierungsschlüssel zu verwenden, der in diesem Artikel angegeben ist: Office 2013 und lync 2013 werden regelmäßig zur Eingabe von Anmelde Informationen für SharePoint Online, onedrive und lync Online aufgefordert.|
|Onedrive for Business Mobile-Client|Unterstützt|| 
|Office 365 pro Plus-Aktivierungs Seite|Unterstützt-Client seitiger Registrierungsschlüssel empfohlen|Wenn eine Alternative ID konfiguriert ist, sehen Sie, dass der lokale UPN im Feld Überprüfung vorab ausgefüllt ist. Dies muss in die alternative Identität geändert werden, die verwendet wird. Es wird empfohlen, den Client seitigen Registrierungsschlüssel zu verwenden, der in diesem Artikel beschrieben wird: Office 2013 und lync 2013 fordert regelmäßig zur Eingabe von Anmelde Informationen für SharePoint Online, onedrive und lync online auf.|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange-und Skype for Business-Clients

|Client|Support-Anweisung mit HMA|Support-Anweisung ohne HMA|
| ----- |----- | ----- |
|Outlook|Unterstützt, keine zusätzlichen Eingabe Aufforderungen|Unterstützt</br></br>Mit **moderner Authentifizierung** für Exchange Online: unterstützt</br></br>Mit **regulärer Authentifizierung** für Exchange Online: wird mit folgenden Einschränkungen unterstützt:</br><li>Sie müssen sich auf einem mit der Domäne verknüpften Computer befinden und mit dem Unternehmensnetzwerk verbunden sein. </li><li>Sie können nur eine Alternative ID in Umgebungen verwenden, die keinen externen Zugriff für Postfach-Benutzer zulassen. Dies bedeutet, dass Benutzer sich nur dann auf eine unterstützte Weise bei Ihrem Postfach authentifizieren können, wenn Sie mit dem Unternehmensnetzwerk, einem VPN oder über einen direkt Zugriffs Computer verbunden sind. Sie erhalten jedoch einige zusätzliche Eingabe Aufforderungen, wenn Sie Ihr Outlook-Profil konfigurieren.| 
|Hybride öffentliche Ordner|Unterstützt, keine zusätzlichen Eingabe Aufforderungen.|Mit **moderner Authentifizierung** für Exchange Online: unterstützt</br></br>Mit **regulärer Authentifizierung** für Exchange Online: nicht unterstützt</br></br><li>Hybride öffentliche Ordner können nicht erweitert werden, wenn alternative IDs verwendet werden, und sollten daher noch heute nicht mit regulären Authentifizierungsmethoden verwendet werden.|
|Standortübergreifende Delegierung|Weitere Informationen finden [Sie unter Konfigurieren von Exchange für die Unterstützung von Delegierten Post Fach Berechtigungen in](/exchange/hybrid-deployment/set-up-delegated-mailbox-permissions)|Weitere Informationen finden [Sie unter Konfigurieren von Exchange für die Unterstützung von Delegierten Post Fach Berechtigungen in](/exchange/hybrid-deployment/set-up-delegated-mailbox-permissions)|
|Archivieren des Post Fach Zugriffs (Postfach lokal-Archive in der Cloud)|Unterstützt, keine zusätzlichen Eingabe Aufforderungen|Unterstützt: Benutzer erhalten eine zusätzliche Aufforderung zum Eingeben von Anmelde Informationen, wenn Sie auf das Archiv zugreifen. Sie müssen bei entsprechender Aufforderung Ihre alternative ID angeben.| 
|Outlook Web Access|Unterstützt|Unterstützt|
|Outlook-Mobile Apps für Android, IOS und Windows Phone|Unterstützt|Unterstützt|
|Skype for Business/lync|Unterstützt, ohne zusätzliche Eingabe Aufforderungen|Unterstützt (außer wie bereits erwähnt), aber es gibt eine Möglichkeit für Benutzer Verwirrung.</br></br>Auf mobilen Clients wird die Alternative ID nur unterstützt, wenn SIP Address = Email Address = Alternative ID lautet.</br></br> Benutzer müssen sich möglicherweise zweimal beim Skype for Business-Desktop Client anmelden, zuerst den lokalen UPN verwenden und dann die Alternative ID verwenden. (Beachten Sie, dass es sich bei der "Anmelde Adresse" tatsächlich um die SIP-Adresse handelt, die möglicherweise nicht mit dem "Benutzernamen" identisch ist, obwohl dies häufig der Wert ist). Wenn Sie zum ersten Mal einen Benutzernamen eingeben, sollte der Benutzer den UPN eingeben, auch wenn er nicht korrekt mit der alternativen ID oder SIP-Adresse aufgefüllt ist. Nachdem der Benutzer mit dem UPN auf "Anmelden" geklickt hat, wird die Eingabeaufforderung für den Benutzernamen erneut angezeigt, dieses Mal mit dem UPN gefüllt. Dieses Mal muss der Benutzer dies durch die Alternative ID ersetzen und auf Anmelden klicken, um den Anmeldevorgang abzuschließen. Auf mobilen Clients sollten Benutzer die lokale Benutzer-ID auf der Seite "Erweitert" mit dem Sam-Format ("Domäne \ Benutzername") und nicht mit dem UPN-Format eingeben.</br></br>Wenn Skype for Business oder lync nach erfolgreicher Anmeldung besagt, dass Exchange ihre Anmelde Informationen benötigt, müssen Sie die Anmelde Informationen angeben, die für den Speicherort des Postfachs gültig sind. Wenn sich das Postfach in der Cloud befindet, müssen Sie die Alternative ID angeben. Wenn das Postfach lokal ist, müssen Sie den lokalen UPN bereitstellen.| 

## <a name="additional-details--considerations"></a>Weitere Details & Überlegungen

-   Die Alternative Anmelde-ID ist für Verbund Umgebungen mit AD FS bereitgestellt.  Dies wird in den folgenden Szenarien nicht unterstützt:
    -   Nicht Routing fähige Domänen (z. b. Conto so. local), die nicht von Azure AD überprüft werden können.
    -   Verwaltete Umgebungen, für die keine AD FS bereitgestellt wurde.


-   Wenn diese Option aktiviert ist, ist die Alternative Anmelde-ID nur für die Benutzernamen-/Kennwort-Authentifizierung über alle von AD FS (SAML-P, WS-Fed, WS-Trust und OAuth) unterstützten Benutzernamen-/Kennwort-authentifizierungprotokolle verfügbar.


-   Wenn die integrierte Windows-Authentifizierung (WIA) ausgeführt wird (z. b. Wenn Benutzer versuchen, über das Intranet auf eine Unternehmens Anwendung auf einem in eine Domäne eingebundenen Computer zuzugreifen, und AD FS Administrator die Authentifizierungs Richtlinie für die Verwendung von WIA für das Intranet konfiguriert hat), wird der UPN für die Authentifizierung verwendet. Wenn Sie Anspruchs Regeln für die vertrauende Seite für die Alternative Anmelde-ID-Funktion konfiguriert haben, sollten Sie sicherstellen, dass diese Regeln im Fall von WIA weiterhin gültig sind.

-   Wenn diese Funktion aktiviert ist, erfordert die Alternative Anmelde-ID mindestens einen globalen Katalogserver, der vom AD FS Server für jede von AD FS unterstützte Benutzerkonto Gesamtstruktur erreichbar ist. Wenn ein globaler Katalogserver in der Gesamtstruktur des Benutzerkontos nicht erreicht wird, führt AD FS zur Verwendung des UPN zurück. Standardmäßig sind alle Domänen Controller globale Katalogserver.

-   Wenn auf dem AD FS Server mehr als ein Benutzerobjekt mit demselben Alternativen Anmelde-ID-Wert gefunden wird, der in allen konfigurierten Benutzerkonten Gesamtstrukturen angegeben ist, schlägt die Anmeldung fehl.

-   Wenn das Feature für die Alternative Anmelde-ID aktiviert ist, versucht AD FS zuerst den Endbenutzer mit einer alternativen Anmelde-ID zu authentifizieren und dann auf den UPN zurückzugreifen, wenn kein Konto gefunden werden kann, das durch die Alternative Anmelde-ID identifiziert werden kann. Stellen Sie sicher, dass keine Konflikte zwischen der alternativen Anmelde-ID und dem UPN bestehen, wenn Sie die UPN-Anmeldung weiterhin unterstützen möchten. Wenn Sie z. b. ein e-Mail-Attribut mit dem UPN des anderen festlegen, wird der andere Benutzer daran gehindert, sich mit seinem UPN anzumelden.

-   Wenn eine der vom Administrator konfigurierten Gesamtstrukturen nicht aktiv ist, werden AD FS weiterhin ein Benutzerkonto mit alternativer Anmelde-ID in anderen Gesamtstrukturen suchen, die konfiguriert sind. Wenn AD FS Server in den Gesamtstrukturen, die durchsucht wurden, nach einem eindeutigen Benutzerobjekt sucht, meldet sich der Benutzer erfolgreich an.

-   Sie können außerdem die AD FS Anmeldeseite anpassen, um Endbenutzern einen Hinweis zur alternativen Anmelde-ID zu senden. Hierzu können Sie entweder die angepasste Anmelde Seiten Beschreibung hinzufügen (Weitere Informationen finden Sie unter [Anpassen der AD FS Anmelde Seiten](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11)) oder Anpassen der Zeichenfolge "Anmelden mit dem Organisations Konto" über das Feld "Benutzername" (Weitere Informationen finden Sie unter [Erweiterte Anpassung der AD FS Anmelde Seiten](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn636121(v=ws.11)).

-   Der neue Anspruchstyp, der den alternativen Anmelde-ID-Wert enthält, ist **http:schemas. Microsoft. com/WS/2013/11/Alternate eloginid**

## <a name="events-and-performance-counters"></a>Ereignisse und Leistungsindikatoren
Die folgenden Leistungsindikatoren wurden hinzugefügt, um die Leistung von AD FS Servern zu messen, wenn eine Alternative Anmelde-ID aktiviert ist:

-   Alternative Anmelde-ID-Authentifizierungen: Anzahl der Authentifizierungen, die mithilfe einer alternativen Anmelde-ID ausgeführt wurden

-   Alternative Anmelde-ID-Authentifizierungen/Sek.: die Anzahl der Authentifizierungen, die mit alternativer Anmelde-ID pro Sekunde ausgeführt wurden.

-   Durchschnittliche Such Wartezeit für alternative Anmelde-ID: durchschnittliche Such Latenz in den Gesamtstrukturen, die ein Administrator für die Alternative Anmelde-ID konfiguriert hat.

Im folgenden finden Sie verschiedene Fehlerfälle und die entsprechenden Auswirkungen auf die Benutzeranmeldung bei Ereignissen, die von AD FS protokolliert werden:



|                       **Fehlerfälle**                        | **Auswirkung auf die Anmelde Darstellung** |                                                              **Event**                                                              |
|--------------------------------------------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Es konnte kein Wert für "samAccountName" für das Benutzerobjekt "" erhalten werden. |          Anmeldefehler           |                  Ereignis-ID 364 mit Ausnahme Meldung MSIS8012: der sAMAccountName für den Benutzer wurde nicht gefunden: " {0} ".                   |
|        Auf das CanonicalName-Attribut kann nicht zugegriffen werden.         |          Anmeldefehler           |               Ereignis-ID 364 mit Ausnahme Meldung MSIS8013: CanonicalName: ' {0} ' des Benutzers: ' ' weist ein ungültiges {1} Format auf.                |
|        Es wurden mehrere Benutzer Objekte in einer Gesamtstruktur gefunden.        |          Anmeldefehler           | Ereignis-ID 364 mit Ausnahme Meldung MSIS8015: Es wurden mehrere Benutzerkonten mit {0} der Identität "" in der Gesamtstruktur " {1} " mit Identitäten gefunden:{2} |
|   Mehrere Benutzer Objekte werden in mehreren Gesamtstrukturen gefunden.    |          Anmeldefehler           |           Ereignis-ID 364 mit Ausnahme Meldung MSIS8014: Es wurden mehrere Benutzerkonten mit der Identität ' ' in Gesamtstrukturen gefunden {0} :{1}            |

## <a name="see-also"></a>Weitere Informationen
[AD FS-Vorgänge](../ad-fs-operations.md)
