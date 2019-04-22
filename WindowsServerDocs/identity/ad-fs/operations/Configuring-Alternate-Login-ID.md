---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: Konfigurieren von alternativen Anmelde-ID
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 615faf4153949aa4ad989f017068d1809fca26b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820871"
---
# <a name="configuring-alternate-login-id"></a>Konfigurieren von alternativen Anmelde-ID

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

## <a name="what-is-alternate-login-id"></a>Was ist eine alternative Anmelde-ID?
In den meisten Fällen verwenden Benutzer ihren UPN (User Principal Names) für die Anmeldung bei ihren Konten. Allerdings können in einigen Umgebungen aufgrund von Unternehmensrichtlinien oder Abhängigkeiten von lokalen LOB-Anwendung, die Benutzer eine andere Art der Anmeldung verwenden. 

>[!NOTE]
>Von Microsoft empfohlen, dass die bewährte Methoden sind UPN primären SMTP-Adresse übereinstimmen. Dieser Artikel behandelt ist die kleine Prozentsatz der Kunden, die UPN wiederherstellen kann nicht entsprechend.

Beispielsweise können werden Verwendung ihrer e-Mail-Id für die Anmeldung in und kann, die sich von der UPN sein. Dies kommt besonders häufig in Szenarien, in dem der UPN nicht geroutet werden kann. Der Benutzer Jane Doe mit UPN jdoe@contoso.local und e-Mail-Adresse jdoe@contoso.com. Jane ist möglicherweise nicht zu, dass es den UPN, da sie immer ihre e-Mail-Id für die Anmeldung verwendet hat. Verwenden einer anderen Anmeldung Methode anstelle von UPN stellt alternativen ID dar. Weitere Informationen dazu, wie der UPN ist, finden Sie unter erstellt [Auffüllen von Azure AD UserPrincipalName](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Active Directory-Verbunddienste (AD FS) können verbundanwendungen mithilfe von AD FS, melden Sie sich mit der alternativen ID Dadurch können Administratoren geben Sie eine Alternative zu der Standard-UPN-Anmeldung verwendet werden. AD FS unterstützt bereits mit der jede Form von Benutzer-ID, die von Active Directory Domain Services (AD DS) akzeptiert wird. Bei der Konfiguration für die alternative ID kann AD FS Benutzer melden sich mit den konfigurierten alternative ID-Wert, z. B. e-Mail-Id an. Mit der alternativen ID können Sie zum Übernehmen von SaaS-Anbietern, z. B. Office 365, ohne Ihre lokalen UPNs zu ändern. Darüber hinaus können Sie zur Unterstützung von Line-of-Business-Service-Anwendungen mit Identitäten Consumer bereitgestellt.

## <a name="alternate-id-in-azure-ad"></a>Alternative Id in Azure AD
Eine Organisation möglicherweise alternative ID in den folgenden Szenarien verwenden:
1.  Der Name der lokalen Domäne ist nicht routingfähig, z. B. "Contoso.Local" und der Standard-Benutzerprinzipalname ist daher nicht routingfähige (jdoe@contoso.local). Vorhandene UPN werden nicht aufgrund von lokalen anwendungsabhängigkeiten oder Richtlinien des Unternehmens geändert. Azure AD und Office 365 benötigen alle Domänensuffixe Internet routingfähige vollständig sein Azure AD-Verzeichnis zugeordnet. 
2.  Der lokale UPN ist nicht identisch mit die e-Mail-Adresse des Benutzers, um Office 365 anmelden, verwenden Benutzer e-Mail-Adresse und UPN nicht aufgrund von Einschränkungen für die Organisation verwendet werden.
In den oben genannten Szenarien kann alternative ID mit AD FS Benutzer Azure AD anmelden, ohne Ihre lokalen UPNs zu ändern. 

## <a name="end-user-experience-with-alternate-login-id"></a>Endbenutzer-Erfahrung mit der alternativen Anmelde-ID
Die benutzerfreundlichkeit hängt von der Authentifizierungsmethode, die mit der alternativen Anmelde-Id ab.  Derzeit es gibt drei Möglichkeiten, die in der Verwendung von alternativen Anmelde-Id erreicht werden kann.  Die Überladungen sind:

- **Reguläre Authentifizierung (Legacy)**-Standardauthentifizierungsprotokoll verwendet.
- **Moderne Authentifizierung** -Active Directory-Authentifizierungsbibliothek ADAL-basierte Anmeldung für Anwendungen bietet. Dadurch werden Anmeldefunktionen wie Multi-Factor Authentication (MFA), SAML-basierte Drittanbieter-Identitätsanbieter mit Office-Clientanwendungen, Smartcard- und zertifikatbasierte Authentifizierung.
- **Moderner hybrider Authentifizierung** : bietet alle Vorteile der modernen Authentifizierung und bietet Benutzern die Möglichkeit, den Zugriff auf lokale Anwendungen Autorisierungstoken abgerufen haben, aus der Cloud verwenden.

>[!NOTE]
> Für das bestmögliche Erlebnis empfiehlt Microsoft dringend moderner hybrider Authentifizierung.



## <a name="configure-alternate-logon-id"></a>Konfigurieren Sie alternative Anmelde-ID
Verbinden mithilfe von Azure AD verbinden wir empfehlen, die mithilfe von Azure AD zum Konfigurieren der alternativen Anmelde-ID für Ihre Umgebung.

- Neue Konfiguration von Azure AD Connect finden Sie unter Herstellen einer Verbindung mit Azure AD für detaillierte Anweisungen zum Konfigurieren der alternativen ID und den AD FS-Farm.
- Vorhandene Azure AD Connect-Installationen finden Sie unter der Benutzer Anmeldemethode Anleitungen zum Ändern der Anmeldemethode zu AD FS ändern

Wenn Azure AD Connect die Informationen zu AD FS-Umgebung bereitgestellt wird, automatisch überprüft, ob die richtigen KB auf der AD FS vorhanden und konfiguriert AD FS für alle erforderlichen Rechte Anspruchsregeln für Azure AD-Verbund-Vertrauensstellung einschließlich der alternativen ID gesucht. Es ist kein zusätzlicher Schritt erforderlich außerhalb des Assistenten zum alternativen ID konfigurieren

>[!NOTE]
> Microsoft empfiehlt die Verwendung von Azure AD Connect so konfigurieren Sie alternative Anmelde-ID

### <a name="manually-configure-alternate-id"></a>Manuell konfigurieren einer alternativen ID
Um alternative Anmelde-ID konfigurieren zu können, müssen Sie die folgenden Aufgaben ausführen: Konfigurieren Sie Ihre AD FS Anspruchsanbieter-Vertrauensstellungen zum Aktivieren der alternativen Anmelde-ID

1.  Wenn Sie Server 2012 R2 haben, stellen Sie sicher, dass Sie KB2919355 installiert auf allen AD FS-Servern verfügen. Sie können es über Windows Update Services zu erhalten oder direkter download durchgeführt. 

2.  Die AD FS-Konfiguration mit dem folgenden PowerShell-Cmdlet auf jedem Verbundserver in der Farm zu aktualisieren (Wenn Sie eine WID-Farm verfügen, müssen Sie diesen Befehl Ausführen auf dem primären AD FS-Server in der Farm):

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>
```

**AlternateLoginID** der LDAP-Name des Attributs, das Sie für die Anmeldung verwenden möchten.

**LookupForests** ist die Liste der Gesamtstruktur-DNS, die Ihre Benutzer zu gehören.

Um die alternative Anmelde-ID-Funktion zu aktivieren, müssen Sie sowohl AlternateLoginID - als auch LookupForests - Parameter mit einem Wert ungleich Null, ungültig konfigurieren.

Im folgenden Beispiel aktivieren Sie alternative Anmelde-ID-Funktionen, dass Ihre Benutzer mit Konten unter "contoso.com" und "Fabrikam.com" Gesamtstrukturen zu AD FS-fähigen Anwendungen mit ihren "Mail"-Attribut anmelden können.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
```

3.  Um dieses Feature zu deaktivieren, legen Sie den Wert für beide Parameter null sein.

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>Moderner hybrider Authentifizierung mit alternativen-ID

>[!IMPORTANT]
>Folgendes wurde nur mit AD FS und nicht 3. Identitätsanbieter getestet.

### <a name="exchange-and-skype-for-business"></a>Exchange und Skype for Business
Wenn Sie alternative Anmelde-Id mit Exchange und Skype for Business verwenden, hängt die benutzerfreundlichkeit, und zwar unabhängig davon, ob Sie diesen Speicherbereich verwenden.

>[!NOTE]
>Für die beste benutzerfreundlichkeit empfiehlt Microsoft die Verwendung moderner hybrider Authentifizierung.

oder Weitere Informationen finden Sie unter [Hybrid moderner Authentifizierung (Übersicht)](https://support.office.com/en-us/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d)

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Voraussetzungen für Exchange und Skype for Business
Im folgenden finden Sie Voraussetzungen für das Erreichen von einmaligem Anmelden mit einer alternativen ID

- Exchange Online muss die moderne Authentifizierung aktiviert haben.
- Skype für Unternehmen (SFB) Online sollten moderne Authentifizierung aktiviert haben.
- Exchange lokal moderne Authentifizierung ON aktiviert haben, sollten.  Exchange 2013 CU19 oder Exchange 2016 CU18, und Sie muss auf allen Exchange-Servern. Keine Exchange 2010 in der Umgebung.
- Skype for Business auf lokale moderne Authentifizierung ON aktiviert haben, sollten.
- Sie müssen Exchange und Skype-Clients verwenden, die moderne Authentifizierung aktiviert ist. Alle Server müssen SFB Server 2015 CU5 ausgeführt werden.
- Skype für Business-Clients, die moderne Authentifizierung fähig sind.
   - iOS, Android, Windows Phone
   - SFB 2016 (MA ist standardmäßig, aber stellen Sie sicher, dass es nicht deaktiviert wurde.)
   - SFB 2013 (MA ist standardmäßig deaktiviert, müssen Sie sicherstellen MA war eingeschaltet.)
   - SFB Mac-desktop
- Exchange-Clients, die moderne Authentifizierung kann und AltID Regkeys unterstützen
    - Office Pro Plus 2016 nur





#### <a name="supported-office-version"></a>Unterstützte Office-version

Konfigurieren Ihr Verzeichnis für SSO mit alternativen-Id mit alternativen-Id kann zusätzliche Anweisungen für die Authentifizierung verursachen, wenn es sich bei diesen zusätzlichen Konfigurationen nicht abgeschlossen werden. Finden Sie im Artikel für die möglichen Auswirkungen auf die benutzerfreundlichkeit mit alternativen-Id.

Die folgende zusätzliche Konfiguration ist die benutzererfahrung erheblich verbessert, und erreichen Sie in der Nähe von 0 (null) Anweisungen für die Authentifizierung für Benutzer von alternativen-Id in Ihrer Organisation.

##### <a name="step-1-update-to-required-office-version"></a>Schritt 1 Aktualisieren Sie auf die erforderlichen Office-version
Office-Version 1712 (keine 8827.2148 build) und höher aktualisiert die Authentifizierungslogik aus, um das alternative-Id-Szenario zu behandeln. Um die Logik die neue nutzen zu können, müssen die Clientcomputer für Office-Version 1712 (keine 8827.2148 build) und höher aktualisiert werden.

##### <a name="step-2-configure-registry-for-impacted-users-using-group-policy"></a>Schritt 2 Konfigurieren der Registrierung für die betroffenen Benutzer, die mithilfe der Gruppenrichtlinie
Die Office-Anwendungen basieren auf Informationen, die von der Verzeichnisadministrator zum Identifizieren der Umgebung für die alternative-Id an. Die folgenden Registrierungsschlüssel konfiguriert werden, um Office-Anwendungen, die den Benutzer mit alternativen-Id zu authentifizieren, ohne dass weitere aufforderungen zu müssen

|RegKey hinzufügen|RegKey Data source Name, Typ und Wert|Windows 7/8|Windows 10|Beschreibung|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER\Software\Microsoft\AuthN|DomainHint</br>REG_SZ</br>contoso.com|Erforderlich|Erforderlich|Der Wert von diesem Regkey ist einen Namen der überprüften benutzerdefinierten Domäne im Mandanten der Organisation. Contoso Corp. können beispielsweise einen Wert von "contoso.com" in diesem Regkey bereitstellen, wenn es sich bei "contoso.com" eine der überprüften benutzerdefinierten Domäne im Mandanten "contoso.onmicrosoft.com" lautet.|
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity|EnableAlternateIdSupport</br>REG_DWORD</br>1|Erforderlich für Outlook 2016 ProPlus|Erforderlich für Outlook 2016 ProPlus|Der Wert von diesem Regkey kann zwischen 1 / 0 Outlook-Anwendung an, ob es die Authentifizierungslogik für verbesserte alternative-Id erfassen soll.|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableADALatopWAMOverride</br>REG_DWORD</br>1|Nicht verfügbar|Erforderlich.|Dadurch wird sichergestellt, dass Office WAM nicht verwendet wird, wie Alt-Id von WAM unterstützt wird.|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableAADWAM</br>REG_DWORD</br>1|Nicht verfügbar|Erforderlich.|Dadurch wird sichergestellt, dass Office WAM nicht verwendet wird, wie Alt-Id von WAM unterstützt wird.|
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\contoso.com\sts|&#42;</br>REG_DWORD</br>1|Erforderlich|Erforderlich|Diese Regkey kann verwendet werden, der STS als vertrauenswürdigen Zone in den Internet-Einstellungen festlegen. Standardmäßige AD FS-Bereitstellung empfiehlt Hinzufügen des AD FS-Namespaces der lokalen Intranetzone für Internet Explorer|

## <a name="new-authentication-flow-after-additional-configuration"></a>Neuen authentifizierungsfluss nach zusätzliche Konfiguration

![Authentifizierungsablauf](media/Configure-Alternate-Login-ID/alt1a.png)

1. a: Benutzer wurde in Azure AD mithilfe von alternativen-Id bereitgestellt.
   </br>b: Directory-Administrator legt erforderlichen Regkey-Einstellungen auf den betroffenen Clientcomputern
2. Benutzer, auf dem lokalen Computer authentifiziert, und öffnet eine officeanwendung
3. Office-Anwendung verwendet die Anmeldeinformationen für die lokale Sitzung
4. Officeanwendung authentifiziert sich bei Azure AD mithilfe von DomänenHinweis von Administrator- und lokalen Anmeldeinformationen per Push übertragen
5. Azure AD authentifiziert den Benutzer erfolgreich durch, korrigieren die Verbund-Bereich, und geben ein Token weiterleiten

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>Anwendungen und Benutzern auftreten, nachdem die zusätzliche Konfiguration

### <a name="non-exchange-and-skype-for-business-clients"></a>Nicht-Exchange und Skype für Business-Clients
|Client|Support-Anweisung|Hinweise|
| ----- | -----|-----|
|Microsoft Teams|Unterstützt|<li>Microsoft Teams unterstützt AD FS (SAML-P, WS-Fed-, WS-Trust und OAuth) und die moderne Authentifizierung.</li><li> Core Microsoft Teams wie z. B. Funktionen von Kanälen, Chats und Dateien funktioniert mit der alternativen Anmelde-ID an.</li><li>1. und 3rd Party-apps müssen separat vom Kunden ermittelt werden. Dies ist, da jede Anwendung eigene Authentifizierungsprotokolle Unterstützung verfügt.</li>|     
|OneDrive for Business|Unterstützt – clientseitige Registrierungsschlüssel empfohlen |Mit der alternativen ID konfiguriert sehen Sie, dass der lokale UPN In das Feld für die Überprüfung bereits aufgefüllt ist. Dies muss in der alternativen Identität geändert werden, der verwendet wird. Es wird empfohlen, mithilfe des Client-Side-Registrierungsschlüssels in diesem Artikel erwähnt: Office 2013 und Lync 2013 können Sie in regelmäßigen Abständen aufgefordert, Anmeldeinformationen für SharePoint Online, OneDrive und Lync Online.|
|OneDrive for Business-Mobile-Client|Unterstützt|| 
|Office 365 Pro Plus-Aktivierungsseite|Unterstützt – clientseitige Registrierungsschlüssel empfohlen|Mit der alternativen ID konfiguriert sehen Sie, dass der lokale UPN in das Feld für die Überprüfung bereits aufgefüllt ist. Dies muss in der alternativen Identität geändert werden, der verwendet wird. Es wird empfohlen, mithilfe des Client-Side-Registrierungsschlüssels, der in diesem Artikel erwähnt: Office 2013 und Lync 2013 können Sie in regelmäßigen Abständen aufgefordert, Anmeldeinformationen für SharePoint Online, OneDrive und Lync Online.|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange und Skype für Business-Clients

|Client|Support-Anweisung verwendet werden – mit diesen Speicherbereich|Support-Anweisung verwendet werden – ohne diesen Speicherbereich|
| ----- |----- | ----- |
|Outlook|Unterstützte, keine zusätzlichen aufforderungen|Unterstützt</br></br>Mit **moderne Authentifizierung** für Exchange Online: Unterstützt</br></br>Mit **regulären Authentifizierung** für Exchange Online: Mit folgenden Einschränkungen unterstützt:</br><li>Sie müssen sich auf eine Domäne eingebundenen Computer befinden und mit dem Unternehmensnetzwerk verbunden sein </li><li>Sie können nur einer alternativen ID verwenden, die in Umgebungen, die keinen externen Zugriff für Postfachbenutzer zulassen. Dies bedeutet, dass nur Authentifizierung von Benutzern mit ihrem Postfach in ein unterstützter Weg dargestellt, wenn sie und verknüpft Sie mit dem Unternehmensnetzwerk eine VPN-Verbindung, oder verbunden sind über der direkte Zugriff auf Computer, aber ein paar zusätzliche aufforderungen zu erhalten, wenn Ihr Outlook-Profil konfigurieren.| 
|Hybride öffentlicher Ordner|Unterstützte, keine zusätzlichen aufforderungen.|Mit **moderne Authentifizierung** für Exchange Online: Unterstützt</br></br>Mit **regulären Authentifizierung** für Exchange Online: Nicht unterstützt</br></br><li>Hybride Öffentliche Ordner sind nicht erweitern, wenn alternative IDs verwendet werden und daher nicht soll noch heute mit regulären Authentifizierungsmethoden verwendet werden.|
|Cross-Premises Delegierung|Finden Sie unter [Exchange konfigurieren, um delegierte Berechtigungen in einer hybridbereitstellung zu unterstützen.](https://technet.microsoft.com/library/mt784505.aspx)|Finden Sie unter [Exchange konfigurieren, um delegierte Berechtigungen in einer hybridbereitstellung zu unterstützen.](https://technet.microsoft.com/library/mt784505.aspx)|
|Zugriff auf das Archiv-Postfach (Mailbox lokal - Archiv in der Cloud)|Unterstützte, keine zusätzlichen aufforderungen|Unterstützt – Benutzer erhalten eine zusätzliche Aufforderung zur Eingabe von Anmeldeinformationen, wenn Sie das Archiv zugreifen, müssen sie die alternative ID bei Aufforderung angeben.| 
|Outlook Web Access|Unterstützt|Unterstützt|
|Outlook Mobile-Apps für Android, IOS und Windows Phone|Unterstützt|Unterstützt|
|Skype for Business / Lync|Unterstützt werden, ohne zusätzliche aufforderungen|Unterstützt (sofern nicht anders angegeben), aber es besteht die Gefahr von Verwechslungen von Benutzern.</br></br>Für mobile Clients die, der alternativen Id wird nur unterstützt, wenn SIP-Adresse = e-Mail-Adresse = alternativen-ID.</br></br> Benutzer müssen möglicherweise zweimal auf die Skype für Business desktop-Client zunächst mit dem lokalen UPN und klicken Sie dann mit der alternativen ID anmelden (Beachten Sie, dass die "Anmeldeadresse" eigentlich die SIP-Adresse der möglicherweise nicht identisch mit "User Name" ist, jedoch ist häufig). Bei zuerst für einen Benutzer dazu aufgefordert werden, sollte der Benutzer UPN, eingeben, auch wenn es nicht ordnungsgemäß mit der alternativen ID oder SIP-Adresse vorab aufgefüllt wird. Nachdem der Benutzer klickt, melden Sie sich mit den UPN, der Benutzer die Eingabeaufforderung wieder angezeigt wird, dieses Mal enthält bereits den UPN. Melden Sie diesmal, die der Benutzer führt eine Ersetzung mit der alternativen ID muss, und klicken Sie auf an, um den Anmeldeprozess abzuschließen. Mobile Clients sollten Benutzer die lokalen Benutzer-ID in die Seite "Erweitert", geben Sie auf mit SAM-Stil-Format (Domäne\Benutzername), nicht die UPN-Format.</br></br>Nach der erfolgreichen Anmeldung Falls der Skype for Business oder Lync lautet "Exchange benötigt Ihre-Anmeldeinformationen", müssen Sie die Anmeldeinformationen angeben, die auf dem sich das Postfach befindet gültig sind. Wenn das Postfach in der Cloud befindet, Sie die alternative ID angeben müssen Wenn das Postfach lokal ist, die Sie den lokalen UPN angeben müssen.| 
 
## <a name="additional-details--considerations"></a>Weitere Informationen und Überlegungen

-   Die alternative Anmelde-ID-Funktion ist mit AD FS-Bereitstellung für verbundene Umgebungen verfügbar.  Es wird nicht in den folgenden Szenarien unterstützt:
    -   Nicht routingfähige Domänen (z. B. "contoso.Local"), die von Azure AD nicht überprüft werden können.
    -   Verwaltete Umgebungen, die nicht über AD FS-Bereitstellung verfügen.


-   Wenn aktiviert, die alternative Anmelde-ID-Funktion ist nur verfügbar für die Benutzername/Kennwort-Authentifizierung der Benutzer/Kennwort-Authentifizierung über alle Protokolle hinweg unterstützt, die von AD FS (SAML-P, WS-Fed-, WS-Trust und OAuth).


-   Wenn Windows integrierte Authentifizierung (WIA) wird ausgeführt (z. B. wenn Benutzer versuchen, eine Unternehmens-Anwendung auf eine Domäne eingebundenen Computer über das Intranet zugreifen und AD FS-Administrator hat die Authentifizierungsrichtlinie Verwendung WIA für das Intranet konfiguriert), UPN Isused für die Authentifizierung. Wenn Sie alle Anspruchsregeln der vertrauenden Seiten für alternative Anmelde-ID-Feature konfiguriert haben, sollten Sie sicherstellen, dass diese Regeln bei WIA noch gültig sind.

-   Wenn aktiviert, erfordert die Funktion der alternativen Anmelde-ID mindestens ein globaler Katalogserver aus der AD FS-Server für jeden Benutzer Kontogesamtstruktur erreichbar sein, die AD FS unterstützt. Fehler in der Kontogesamtstruktur Benutzer einen globaler Katalogserver erreicht führt in AD FS zurückgreifen, um den UPN verwenden. Standardmäßig sind alle Domänencontroller globalen Katalogserver zu erhalten.

-   Wenn aktiviert, wenn AD FS-Server mehr als ein Benutzerobjekt mit dem gleichen alternativen Anmelde-ID-Wert angegeben, die in allen Gesamtstrukturen die konfigurierten Benutzer-Konto gefunden, schlägt die Anmeldung fehl.

-   Bei der alternativen Anmelde-ID-Funktion aktiviert ist, versucht AD FS authentifizieren zunächst den Endbenutzer mit der alternativen Anmelde-ID, und klicken Sie dann zurückgegriffen um UPN verwenden, wenn ein Konto gefunden werden kann, die anhand der alternativen Anmelde-ID identifiziert werden können Sie sollten sicherstellen, dass keine Konflikte zwischen der alternativen Anmelde-ID und den UPN vorhanden sind, wenn Sie nach wie vor die UPN-Anmeldung unterstützen möchten. Zum Beispiel können Blöcke UPN der Mail-Attribut mit den anderen festlegen den andere Benutzer nicht mit seinem UPN anmelden.

-   Wenn eine der Gesamtstrukturen, die vom Administrator konfiguriert ist ausgefallen ist, weiterhin AD FS-Benutzerkonto mit der alternativen Anmelde-ID in anderen Gesamtstrukturen gesucht, die konfiguriert werden. Wenn AD FS-Server eine eindeutige Benutzer Objekte in den Gesamtstrukturen, die es durchsucht wurde findet, wird ein Benutzer erfolgreich anmeldet.

-   Sie sollten außerdem zum Anpassen der AD FS-Anmeldeseite zum Endbenutzer ein Hinweis über die alternative Anmelde-ID. Können Sie dies tun, indem Sie die Beschreibung der benutzerdefinierten Anmeldeseite hinzufügen (Weitere Informationen finden Sie unter [Anpassen der AD FS-Sign-in Webseiten](https://technet.microsoft.com/library/dn280950.aspx) oder Anpassen der Zeichenfolge "Mit Unternehmenskonto anmelden", über das Feld "Username" (Weitere Informationen Informationen finden Sie unter [Advanced Customization of AD FS-Sign-in-Webseiten](https://technet.microsoft.com/library/dn636121.aspx).

-   Der neue Anspruchstyp, der die alternative Anmelde-ID-Wert enthält ist **http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>Ereignisse und Leistungsindikatoren
Die folgenden Leistungsindikatoren wurden hinzugefügt, um die Leistung von AD FS-Servern zu messen, wenn die alternative Anmelde-ID aktiviert ist:

-   Alternative Anmelde-Id-Authentifizierungen: Anzahl der Authentifizierungen, die ausgeführt werden, mithilfe der alternativen Anmelde-ID

-   Alternativer Anmelde-Id-Authentifizierungen/Sek.: Anzahl der Authentifizierungen, die ausgeführt werden, mithilfe der alternativen Anmelde-ID/Sek.

-   Durchschnittliche Suchlatenz für alternative Anmelde-ID: Durchschnittliche Wartezeit bei Suchvorgängen in den Gesamtstrukturen, die ein Administrator, für die alternative Anmelde-ID konfiguriert hat

Im folgenden finden verschiedene Fehler und die entsprechenden Auswirkungen auf die der Anmeldung Benutzeroberfläche mit Ereignissen, die von AD FS protokolliert:



**Fehler**|**Auswirkungen auf die Anmeldung**|**Ereignis**|
---------|---------|---------
Kann nicht auf einen Wert für "sAMAccountName" für das Benutzerobjekt zu erhalten.|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8012: Wurde nicht gefunden "sAMAccountName" für den Benutzer: "{0}".|
Das CanonicalName-Attribut kann nicht zugegriffen werden|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8013: CanonicalName-Element: '{0}"des Benutzers:"{1}"befindet sich im hat ein ungültiges Format.|
Mehrere Benutzerobjekte befinden sich in einem Gesamtstrukturen|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8015: Finden Sie mehrere Konten mit Identität '{0}"in der Gesamtstruktur"{1}"mit Identitäten: {2}|
Mehrere Benutzerobjekte befinden sich in mehreren Gesamtstrukturen|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8014: Finden Sie mehrere Konten mit Identität '{0}"in Gesamtstrukturen: {1}|

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)


