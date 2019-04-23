---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f8b8991e664a84c3f2b3200de4068af8d1476a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846611"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind

>Gilt für: Windows Server 2016

Das folgende Thema beschreibt die Konfiguration erforderlich, damit Ihre AD FS-Infrastruktur zum Authentifizieren von Benutzern, deren Identitäten in v3-kompatiblen Verzeichnissen (LDAP = Lightweight Directory Access Protocol) gespeichert werden, kann.

In vielen Organisationen bestehen Lösungen zur identitätsverwaltung eine Kombination von Active Directory, AD LDS oder Drittanbieter-LDAP-Verzeichnissen aus. Durch das Hinzufügen von AD FS-Unterstützung zum Authentifizieren von Benutzern in LDAP v3-kompatiblen Verzeichnissen gespeichert werden soll, können Sie profitieren von der gesamten Unternehmen AD FS Features unabhängig davon, wo Ihre Benutzeridentitäten gespeichert werden. AD FS unterstützt LDAP-Verzeichnis v3-kompatibel.

> [!NOTE]
> Teil der AD FS-Features enthalten, die einmaliges Anmelden (SSO), Geräteauthentifizierung, flexible bedingte Zugriffsrichtlinien, Unterstützung für die Arbeit-aus- und überall mit allen durch die Integration mit dem Webanwendungsproxy nahtlose Verbund mit Azure AD, die wiederum können Sie und Ihre Benutzer auf die Cloud, einschließlich Office 365 und andere SaaS-Anwendungen zu nutzen.  Weitere Informationen finden Sie unter [Active Directory-Verbunddienste: Übersicht](../../ad-fs/AD-FS-2016-Overview.md).

In der Reihenfolge für AD FS zum Authentifizieren von Benutzern aus einem LDAP-Verzeichnis, müssen Sie diese LDAP-Verzeichnis mit der AD FS-Farm verbinden, durch das Erstellen einer **lokales Anspruchsanbieter-Vertrauensstellung**.  Eine lokales Anspruchsanbieter-Vertrauensstellung ist ein Vertrauensstellungsobjekt, das ein LDAP-Verzeichnis, in der AD FS-Farm darstellt. Ein lokales Anspruchsanbieter-Vertrauensstellungsobjekt Objekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die dieses LDAP-Verzeichnis für den lokalen Verbunddienst identifizieren.

Sie können mehrere LDAP-Verzeichnisse, die jeweils über eine eigene Konfiguration, in der gleichen AD FS-Farm durch Hinzufügen mehrerer unterstützen **lokales Anspruchsanbieter-Vertrauensstellungen**. Darüber hinaus können AD DS-Gesamtstrukturen, die nicht von der Gesamtstruktur, die AD FS befindet sich vertraut in auch als lokales Anspruchsanbieter-Vertrauensstellungen modelliert werden. Sie können lokale Anspruchsanbieter-Vertrauensstellungen mithilfe von Windows PowerShell erstellen.

LDAP-Verzeichnissen (lokales Anspruchsanbieter-Vertrauensstellungen) können auf die gleiche AD FS-Server innerhalb der gleichen AD FS-Farm mit AD-Verzeichnissen (Anspruchsanbieter-Vertrauensstellungen) nebeneinander existieren, daher ist eine einzelne Instanz von AD FS authentifizieren und Autorisieren des Zugriffs für Benutzer, die werden kann in beiden AD gespeichert und nicht-AD-Verzeichnisse.

Nur die formularbasierte Authentifizierung wird zum Authentifizieren von Benutzern von LDAP-Verzeichnissen unterstützt. Zertifikat-basierte und die integrierte Windows-Authentifizierung werden nicht unterstützt, zum Authentifizieren von Benutzern in LDAP-Verzeichnissen.

Alle passiven autorisierungsprotokolle von AD FS, darunter SAML, WS-Verbund unterstützt werden und OAuth werden ebenfalls unterstützt, für Identitäten, die in LDAP-Verzeichnissen gespeichert sind.

Die WS-Trust-active-Authorization-Protokoll wird für Identitäten, die in LDAP-Verzeichnissen gespeichert sind, ebenfalls unterstützt.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in einem LDAP-Verzeichnis gespeichert
Um AD FS-Farm zum Authentifizieren von Benutzern aus einem LDAP-Verzeichnis zu konfigurieren, können Sie die folgenden Schritte ausführen:

1.  Konfigurieren Sie zunächst eine Verbindung mit Ihrem LDAP-Verzeichnis mithilfe der **New-AdfsLdapServerConnection** Cmdlet:

    ```
    $DirectoryCred = Get-Credential
    $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
    ```

    > [!NOTE]
    > Es wird empfohlen, dass Sie ein neues Verbindungsobjekt für jeden LDAP-Server erstellen, die Sie herstellen möchten. AD FS kann mehrere Replikatserver LDAP-Verbindung und automatisch ein Failover für den Fall, dass ein bestimmter LDAP-Server ausgefallen ist. Solch einem Fall können Sie eine AdfsLdapServerConnection für jeden dieser Replikat LDAP-Server erstellen und fügen Sie dann auf das Array von Verbindungsobjekten, die mit dem -**LdapServerConnection** Parameter der  **Hinzufügen AdfsLocalClaimsProviderTrust** Cmdlet.

    **HINWEIS:** Der Versuch, Get-Credential "und" Geben Sie einen DN und ein Kennwort verwenden, um mit einer Instanz des LDAP-Bindung verwendet werden, kann zu einem Fehler führen, da die der Benutzer-Schnittstelle Anforderungen für bestimmte Eingabeformate, z.B. "Domäne\Benutzername" oder user@domain.tld. Sie können stattdessen das ConvertTo-SecureString-Cmdlet verwenden, wie folgt (im folgenden Beispiel wird angenommen, Benutzer-ID = Admin, Ou = System als DN der Anmeldeinformationen verwendet werden, zum Binden an das LDAP-Instanz):

    ```
    $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
    $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
    ```

    Geben Sie dann das Kennwort für die Uid = Admin, und schließen Sie die Schritte aus.

2.  Als Nächstes können Sie ausführen, den optionalen Schritt der Zuordnung der LDAP-Attribute, die vorhandenen AD FS-Ansprüche, die mit der **New-AdfsLdapAttributeToClaimMapping** Cmdlet. Im folgenden Beispiel wird Sie "givenName", "Surname zuordnen, und CommonName LDAP-Attribute, die AD FS-Ansprüche:

    ```
    #Map given name claim
    $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
    # Map surname claim
    $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
    # Map common name claim
    $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
    ```

    Diese Zuordnung wird vorgenommen, um Attribute aus dem LDAP-Speicher als Ansprüche in AD FS zum Erstellen von Steuerelement-Regeln für bedingten Zugriff in AD FS zur Verfügung zu stellen. Darüber hinaus können AD FS für die Arbeit durch die Bereitstellung einer einfachen Möglichkeit zum Zuordnen von LDAP-Attributen für Ansprüche, die benutzerdefinierte Schemas in LDAP-Stores.

3.  Abschließend müssen Sie die LDAP-Speicher bei registrieren AD FS wie ein lokales Anspruchsanbieter Anbieter Vertrauensstellung mit der **hinzufügen-AdfsLocalClaimsProviderTrust** Cmdlet:

    ```
    Add-AdfsLocalClaimsProviderTrust -Name "Vendors" -Identifier "urn:vendors" -Type Ldap

    # Connection info
    -LdapServerConnection $vendorDirectory 

    # How to locate user objects in directory
    -UserObjectClass inetOrgPerson -UserContainer "CN=VendorsContainer,CN=VendorsPartition" -LdapAuthenticationMethod Basic 

    # Claims for authenticated users
    -AnchorClaimLdapAttribute mail -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -LdapAttributeToClaimMapping @($GivenName, $Surname, $CommonName) 

    # General claims provider properties
    -AcceptanceTransformRules "c:[Type != ''] => issue(claim=c);" -Enabled $true 

    # Optional - supply user name suffix if you want to use Ws-Trust
    -OrganizationalAccountSuffix "vendors.contoso.com"

    ```

    Im obigen Beispiel erstellen Sie eine lokales Anspruchsanbieter-Vertrauensstellung "Anbieter" bezeichnet. Sie werden Verbindungsinformationen für AD FS zur Verbindung mit des LDAP-Verzeichnis diese lokalen Anspruchsanbieter-Vertrauensstellung darstellt, durch Zuweisen von `$vendorDirectory` auf die `-LdapServerConnection` Parameter. Beachten Sie, dass im ersten Schritt, Sie zugewiesen haben `$vendorDirectory` eine Verbindungszeichenfolge zum Herstellen der Verbindung mit bestimmten LDAP-Verzeichnis verwendet werden. Schließlich werden Sie an, die die `$GivenName`, `$Surname`, und `$CommonName` LDAP-Attribute (die Sie die AD FS-Ansprüche zugeordnet) sind für die bedingte Zugriffssteuerung, einschließlich Multi-Factor Authentication-Richtlinien und Ausstellung verwendet werden soll Autorisierung Regeln auch für die Ausstellung über Ansprüche in AD FS ausgestellten Sicherheitstoken. Um aktive Protokolle wie Ws-Trust mit AD FS verwenden zu können, müssen Sie den OrganizationalAccountSuffix-Parameter angeben, der AD FS, um zwischen lokalen Anspruchsanbieter-Vertrauensstellungen bei der Wartung einer aktiven autorisierungsanforderung zu unterscheiden zu können.

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)


