---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: Konfigurieren von alternativen Anmelde-ID
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/04/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb4c98ff1090a9d3c35654614a43e12db99d691d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-alternate-login-id"></a>Konfigurieren von alternativen Anmelde-ID

>Gilt für: Windows Server 2016, Windows Server2012 R2

Benutzer können melden Sie sich Active Directory-Verbunddienste (AD FS) aktiviert von Anwendungen mit einer Benutzer-ID, die von Active Directory-Domänendienste (AD DS) akzeptiert wird. Dazu gehören Benutzerprinzipalnamen (UPNs) (johndoe@contoso.com) oder Domäne qualifiziert Sam-Kontonamen (Contoso\johndoe oder contoso.com\johndoe).

In einigen Umgebungen aufgrund von Unternehmensrichtlinien oder lokalen Line-of-Business-anwendungsabhängigkeiten können Endbenutzer nur ihre E-Mail-Adresse und nicht ihrer UPN oder Sam-Konten Namen kennen. In einigen Fällen der UPN ist auch nicht routbaren (jdoe@contoso.local) und wird nur für die Authentifizierung in Apps auf dem internen Netzwerk verwendet.

Da nicht routbaren Domänen (z. b. "Contoso.Local") kann nicht überprüft werden, Office365 ist erforderlich, alle Benutzernamen vollständig Internet Routingfähig sein. Wenn der lokalen UPN eine nicht routbaren Domäne (z. b. verwendet wird. "Contoso.Local"), oder der UPN kann nicht geändert werden, aufgrund von lokalen anwendungsabhängigkeiten, wir empfehlen das Einrichten von alternativen Anmelde-ID Alternativen Anmelde-ID können Sie so konfigurieren Sie ein Zeichen in Erfahrung, in denen Benutzer können sich ein Attribut als ihre UPN, z. B. Mail anmelden.

Einer der Vorteile dieser Funktion ist, dass Sie SaaS-Anbietern, z. B. Office 365 ohne Änderung Ihrer lokalen Benutzerprinzipalnamen übernehmen können. Darüber hinaus können Sie unterstützen das Line-of-Business-Dienst mit Identitäten Consumer bereitgestellt.

> [!IMPORTANT]
> Mit einer alternativen ID in hybridumgebungen mit Exchange oder Skype for Business wird unterstützt, aber nicht empfohlen. Mit den gleichen Satz von Anmeldeinformationen (z. B. den UPN) für lokale und online bietet die bestmögliche benutzerfreundlichkeit in einer hybridumgebung.  Microsoft empfiehlt, dass Kunden ihre UPNs möglichst ändern, um die Notwendigkeit einer alternativen ID zu vermeiden. Mit einer alternativen ID Lync oder Skype für Unternehmen, ist Lync Server 2013 oder höher erforderlich. Benutzer von einer alternativen ID sollten aktivieren [moderne Authentifizierung](https://support.office.com/article/using-office-365-modern-authentication-with-office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) für Exchange in Office 365 für eine verbesserte Darstellung. Darüber hinaus müssen Kunden, die mit Skype for Business mit mobile Clients sicherstellen, dass die SIP-Adresse des Benutzers e-Mail-Adresse (und einer alternativen ID) entspricht. 

Finden Sie in der Tabelle unten für den Benutzer mit alternativen ID, die mit verschiedenen Office 365-Clients mit regulären Authentifizierung, modernen Authentifizierung und Zertifikat-basierte Authentifizierung (Aktivieren der modernen Authentifizierung erforderlich).

|**Clienttypen**|**Weitere Informationen**|**Informationen zur Unterstützung - regulären und moderne-Authentifizierung**|**Beschreibung**|
|--------------------|------------------------------|------------------------------|------------------------------|
|Outlook|Reguläre Authentifizierung: Sie müssen auf eine Domäne verbundenen Computer sein und mit dem Unternehmensnetzwerk verbunden<br /><br />Moderne Authentifizierung: unterstützt|Sie können nur einer alternativen ID in Umgebungen, die Benutzer keine externen Zugriff zulassen. Dies bedeutet, dass Benutzer nur es Postfach auf eine unterstützte Weise beim angeschlossen authentifizieren kann und mit dem Unternehmensnetzwerk in einem VPN verbunden oder über Direktzugriff verbunden sind. Wenn Sie sich entscheiden, um die modernen Authentifizierung (auch bekannt als ADAL) konfigurieren Sie verwenden Outlook von außerhalb der Domäne beigetreten/verbundenen Computern jedoch erhalten Sie ein paar zusätzliche Anweisungen, wenn Ihr Outlook-Profil zu konfigurieren.<br /><br />Das erste Bild unter der Tabelle User Experience Demo wird angezeigt.|[Moderne Authentifizierung in Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|Öffentliche Ordner Hybrid|Reguläre Authentifizierung: Nicht unterstützt<br /><br />Moderne Authentifizierung: unterstützt|Hybride Öffentliche Ordner nicht erweitern, wenn alternativen IDs verwendet werden und daher nicht werden noch heute mit regulären Authentifizierungsmethoden verwendet sollte. Öffentlicher Ordner in Hybrid verwenden sollen, müssen Sie moderne Authentifizierung (auch bekannt als ADAL) zu konfigurieren.<br /><br />Das erste Bild unter der Tabelle User Experience Demo wird angezeigt.|[Moderne Authentifizierung in Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|Plattformübergreifende lokalen Delegierung|Nicht unterstützt|Derzeit cross lokalen Berechtigungen werden nicht in einer hybridkonfiguration unterstützt, aber sie auch nicht funktioniert, wenn Sie AltID verwenden.||
|Zugriff auf das Archiv-Postfach (Postfach lokalen - Archiv in der Cloud)|Unterstützt|Erhalten Benutzer eine zusätzliche Aufforderung zur Eingabe von Anmeldeinformationen beim Zugriff auf das Archiv, haben Sie ermöglichen es alternativen ID verwenden, wenn Sie dazu aufgefordert werden.<br /><br />Das erste Bild unter der Tabelle User Experience Demo wird angezeigt.||
|Office 365 Pro Plus Seite "Aktivierung"|Unterstützt – Client-Side-Registrierungsschlüssel empfohlen.|Mit einer alternativen ID konfiguriert sehen Sie sich, dass die lokalen UPN im Feld Überprüfung bereits ausgefüllt ist. Dies muss auf die Identität des alternativen geändert werden, die verwendet wird. Wir empfehlen die Verwendung des Registrierungsschlüssels der Client-Seite in der Spalte Link angegeben.<br /><br />Das zweite Bild unter der Tabelle User Experience Demo wird angezeigt.|[Office 2013 und Lync 2013 in regelmäßigen Abständen Eingabeaufforderung zu Anmeldeinformationen auf SharePoint Online, OneDrive und Lync Online](https://support.microsoft.com/en-us/kb/2913639)|
|Microsoft-Teams|Unterstützt|Microsoft-Teams unterstützt AD FS (SAML-P, WS-eingezogen, WS-Trust und OAuth) und moderne.<br/><br/> Core-Microsoft-Teams wie z.B. Kanäle, Chats und Dateien Funktionen funktioniert mit Altnernate Benutzernamen an. </br></br>1. Und 3rd Party-Apps müssen separat vom Kunden untersucht werden. Dies ist, da jede Anwendung ihre eigenen Authentifizierungsprotokolle Wartungsfreundlichkeit hat.| 
|Skype for Business / Lync|Unterstützt (außer wie bereits erwähnt), aber es besteht die Gefahr für Benutzer verwirren.  Auf mobilen Clients einer alternativen Id wird nur unterstützt, wenn SIP-Adresse = e-Mail-Adresse = alternativen-ID.|Benutzer müssen möglicherweise zweimal, um die Skype for Business desktop-Client, zunächst mit den lokalen UPN und klicken Sie dann mit der alternativen ID anmelden (Beachten Sie, dass die "Sign-in-Adresse" tatsächlich die SIP-Adresse ist nicht identisch mit "Benutzername" jedoch häufig möglicherweise ist).  Zunächst sollte für einen Benutzernamen der Benutzer den UPN Geben Sie bei Aufforderung, auch wenn er nicht ordnungsgemäß mit der alternativen ID oder die SIP-Adresse bereits vorhanden ist. Nachdem der Benutzer klickt, melden Sie sich mit den UPN, der Benutzer, die Aufforderung zur Eingabe des wird erneut angezeigt, diesmal mit den UPN aufgefüllt. Dieses Mal der Benutzer muss dieses mit der alternativen ID zu ersetzen, und klicken Sie auf Melden Sie sich bei der Anmeldung Prozess abzuschließen. Mobile Clients sollten Benutzer die lokalen Benutzer-ID in der Registerkarte "Erweitert", geben Sie auf SAM-Style-Format (Domäne\Benutzername), nicht die UPN-Format verwenden.<br /><br />Nach erfolgreicher Anmeldung Skype for Business oder Lync lautet "Exchange benötigt Ihre Anmeldeinformationen", müssen Sie die Anmeldeinformationen angeben, die auf dem sich das Postfach befindet gültig sind. Wenn das Postfach in der Cloud ist, Sie den alternativen ID angeben müssen Wenn das Postfach lokalen ist, die Sie den lokalen UPN angeben müssen.|[Moderne Authentifizierung in Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|Outlook Web Access|Unterstützt|||
|Outlook Mobile Apps für Android, IOS und Windows Phone|Unterstützt|||
|OneDrive for Business|Unterstützt – Client-Side-Registrierungsschlüssel empfohlen.|Mit einer alternativen ID konfiguriert sehen Sie sich, dass die lokalen UPN im Feld Überprüfung bereits ausgefüllt ist. Dies muss auf die Identität des alternativen geändert werden, die verwendet wird. Wir empfehlen die Verwendung des Registrierungsschlüssels der Client-Seite in der Spalte Link angegeben.<br /><br />Das zweite Bild unter der Tabelle User Experience Demo wird angezeigt.|[Office 2013 und Lync 2013 in regelmäßigen Abständen Eingabeaufforderung zu Anmeldeinformationen auf SharePoint Online, OneDrive und Lync Online](https://support.microsoft.com/en-us/kb/2913639)|
|OneDrive for Business-Client – Mobile|Unterstützt|||

![Alternative login](media/Configure-Alternate-Login-ID/ADFS_Alt_ID1.png)

![Alternative login](media/Configure-Alternate-Login-ID/ADFS_Alt_ID2.png)

![Alternative login](media/Configure-Alternate-Login-ID/ADFS_Alt_ID3.png)

Im folgenden sind die folgenden Screenshots ein weiteres Beispiel mit Skype for Business.  Im Beispiel wird die folgende Informationen verwendet.


- SIP:userA@contoso.com 
- BENUTZERPRINZIPALNAME:userA@contoso.local
- E-Mail:userA@contoso.com
- AltId:userA@contoso.com 

Geben Sie die SIP-Adresse als anmelden.

![Skype](media/Configure-Alternate-Login-ID/SkypeA.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeB.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeC.png)

## <a name="to-configure-alternate-login-id"></a>So konfigurieren Sie alternativen Anmelde-ID
Um alternativen Anmelde-ID zu konfigurieren, müssen Sie die folgenden Aufgaben ausführen:

Konfigurieren Sie Ihre AD FS-Anspruchsanbieter-Vertrauensstellungen zum Aktivieren von alternativen Anmelde-ID

1.  Installieren Sie [KB2919355](https://go.microsoft.com/fwlink/?LinkID=396590).  Sie können über Windows Update Services herunterladen oder direkt herunterladen.

2.  Aktualisieren Sie die AD FS-Konfiguration durch Ausführen der folgenden PowerShell-Cmdlets auf jedem Verbundserver in der Farm (Wenn Sie ein Windows-datenbankfarm haben, Sie müssen diesen Befehl Ausführen auf dem primären AD FS-Server in der Farm):

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>

    ```

    **AlternateLoginID** der LDAP-Name des Attributs ein, das Sie für die Anmeldung verwenden möchten.

    **LookupForests** ist die Liste der Gesamtstruktur-DNS-, die Ihre Benutzer zu gehören.

    Um alternativen Anmelde-ID zu aktivieren, müssen Sie mit einem Wert ungleich Null, gültigen Parameter - AlternateLoginID und -LookupForests konfigurieren.

    Im folgenden Beispiel aktivieren Sie alternativen Anmelde-ID-Funktionen, dass Ihre Benutzer mit Konten in Gesamtstrukturen contoso.com und fabrikam.com, AD FS-fähige Anwendungen mit ihrem "Mail"-Attribut anmelden können.

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
    ```

3.  Um dieses Feature zu deaktivieren, legen Sie den Wert für beide Parameter null sein.

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
    ```

4.  Um alternativen Anmelde-ID mit Azure AD zu aktivieren, sind keine weiteren Konfigurationsschritte erforderlich, bei Verwendung von Azure AD Connect.   Alternative ID kann direkt mit dem Assistenten konfiguriert werden.  Finden Sie unter eindeutig identifizieren die Benutzer unter dem Abschnitt [mit Azure AD verbinden](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-get-started-custom/#connect-to-azure-ad).

## <a name="additional-details--considerations"></a>Weitere Informationen und Überlegungen

-   Die alternativen Anmelde-ID-Funktion steht nur für federated-Umgebungen mit AD FS, bereitgestellt.  In den folgenden Szenarien wird nicht unterstützt:
    -   Nicht routbare Domänen (z.B. "contoso.Local"), die von Azure AD nicht überprüft werden können.
    -   Verwaltete Umgebungen, in denen keine AD FS bereitgestellt haben.


-   Wenn aktiviert, die alternativen Anmelde-ID-Funktion ist nur verfügbar für die Authentifizierung mit Benutzername und Kennwort für alle Benutzer Benutzername und Kennwort Authentifizierungsprotokolle von AD FS unterstützt (SAML-P, WS-eingezogen, WS-Trust und OAuth).


-   Wenn Windows integrierte Authentifizierung (WIA) ausgeführt wird (z. B. wenn Benutzer versuchen, eine Unternehmens-Anwendung auf einem Computer mit domänenzugehörigkeit Intranet zugreifen, und AD FS-Administrator um WIA-Unterstützung für das Intranet verwenden die Authentifizierungsrichtlinie konfiguriert wurden), wird UPN für die Authentifizierung verwendet werden. Wenn Sie alle Anspruchsregeln für die vertrauenden Seiten für alternativen Anmelde-ID-Feature konfiguriert haben, sollten Sie sicherstellen, dass diese Regeln in der WIA Fall weiterhin gültig sind.

-   Wenn aktiviert, erfordert das Feature der alternativen Anmelde-ID mindestens einen globalen Katalogserver von AD FS-Server für jeden Benutzer Kontengesamtstruktur aus erreichbar sein, die AD FS unterstützt. Einen globaler Katalogserver in der benutzergesamtstruktur erreichen werden in AD FS mit korrektem um UPN zu verwenden, kann. Standardmäßig sind alle Domänencontroller globalen Katalogserver.

-   Wenn aktiviert, findet der AD FS-Server mehr als eine User-Objekt mit dem gleichen alternativen Anmelde-ID-Wert in allen Gesamtstrukturen die konfigurierte Benutzer Konto angegeben, schlägt die Anmeldung fehl.

-   Wenn alternativen Anmelde-ID-Funktion aktiviert ist, versucht AD FS zunächst, den Benutzer mit alternativen Anmelde-ID zu authentifizieren und dann zurückgreifen um UPN zu verwenden, wenn ein Konto gefunden werden kann, die von der alternativen Anmelde-ID identifiziert werden können Stellen Sie sicher, dass kein Konflikt zwischen den alternativen Anmelde-ID und den UPN vorhanden sind, wenn Sie die UPN-Anmeldung weiterhin unterstützen möchten. Einrichten der Mail-Attribut mit der anderen Person UPN wird z. B. den anderen Benutzer von seinem UPN anmelden blockiert.

-   Wenn eine der Gesamtstrukturen, die vom Administrator konfiguriert ist ausgefallen ist, wird AD FS weiterhin Benutzerkonto mit alternativen Anmelde-ID in anderen Gesamtstrukturen nachschlagen, die konfiguriert sind. Wenn AD FS-Server einen eindeutigen Benutzer Objekte in den Gesamtstrukturen, die sie durchsucht wurde findet, wird ein Benutzer erfolgreich anmelden.

-   Sie sollten außerdem Anpassen der AD FS-Anmeldeseite um End-Benutzern einige Hinweis auf die alternativen Anmelde-ID Können Sie dies tun, indem Sie die angepasste Anmeldeseite Beschreibung hinzufügen (Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx) oder Anpassen der oben genannten Feld "Benutzername" Zeichenfolge "Melden Sie sich mit Organisations-Konto" (Weitere Informationen finden Sie unter [Advanced Customization of AD FS Sign-in Pages](https://technet.microsoft.com/library/dn636121.aspx).

-   Die neuen Anspruchstyp, der den alternativen Anmelde-ID-Wert enthält, ist **http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>Ereignisse und Leistungsindikatoren
Die folgenden Leistungsindikatoren wurden hinzugefügt, um die alternativen Anmelde-ID aktiviert ist, wird durch das Messen der Leistung von AD FS-Server:

-   Alternativen Anmelde-Id-Authentifizierungen: Anzahl Authentifizierungen, die mithilfe von alternativen Anmelde-ID

-   Alternativen Anmelde-Id Authentifizierungen/s: Anzahl der Authentifizierungen mithilfe von alternativen Anmelde-ID pro Sekunde ausgeführt

-   Durchschnittliche Wartezeit bei der Suche für alternativen Anmelde-ID: Durchschnittliche Wartezeit bei der Suche in den Gesamtstrukturen, die ein Administrator für den alternativen Anmelde-ID konfiguriert wurde

Im folgenden finden verschiedene Fehlermeldungen und deren Einfluss auf eines Benutzers Anmeldung mit Ereignissen, die von AD FS protokolliert:



**Fehlermeldungen**|**Auswirkung auf die Anmeldung**|**Ereignis**|
---------|---------|---------
Keinen Wert für "sAMAccountName" für den Benutzer abrufen|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8012: konnte nicht gefunden "sAMAccountName" für den Benutzer: '{0}'.|
Das CanonicalName-Attribut kann nicht zugegriffen werden|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8013: CanonicalName-Element: '{0}' des Benutzers: '{1}' ist im Ungültiges Format.|
Mehrere Benutzerobjekte finden Sie in einem Gesamtstrukturen|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8015: mehrere Benutzerkonten mit der Identität '{0}' in '{1}' mit Identitäten gefunden: {2}|
Mehrere Benutzerobjekte sind in mehreren Gesamtstrukturen enthalten.|Fehler bei der Anmeldung|Ereignis-ID 364 mit Ausnahmemeldung MSIS8014: mehrere Benutzerkonten mit der Identität '{0}' in Gesamtstrukturen gefunden: {1}|

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)


