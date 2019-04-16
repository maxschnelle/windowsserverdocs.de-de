---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: Konfigurieren von AD FS zum Authentifizieren von Benutzern in LDAP-Verzeichnissen gespeichert
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f8b8991e664a84c3f2b3200de4068af8d1476a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>Konfigurieren von AD FS zum Authentifizieren von Benutzern in LDAP-Verzeichnissen gespeichert

>Gilt für: Windows Server 2016

Im folgende Thema wird beschrieben, die Konfiguration erforderlich, damit Ihre AD FS-Infrastruktur zum Authentifizieren von Benutzern, deren Identitäten in v3-kompatiblen Verzeichnissen (LDAP = Lightweight Directory Access Protocol) gespeichert sind.

In vielen Organisationen bestehen Lösungen zur identitätsverwaltung eine Kombination aus Active Directory, AD LDS oder Drittanbieter-LDAP-Verzeichnissen. Durch das Hinzufügen der AD FS-Unterstützung für die Authentifizierung von Benutzern in LDAP-v3-kompatiblen Verzeichnissen gespeichert sind, profitieren Sie von der gesamten robuste AD FS Features unabhängig davon, wo Ihre Benutzeridentitäten gespeichert werden. AD FS unterstützt alle v3-kompatiblen LDAP-Verzeichnis.

> [!NOTE]
> Einige der AD FS-Funktionen zählen einmaliges Anmelden (SSO), Geräteauthentifizierung, flexible bedingte Zugriffsrichtlinien, die Unterstützung für Sie und Ihre Benutzer nutzen die Cloud, einschließlich Office365 und andere SaaS-Apps arbeiten-von-überall durch die Integration in the Web Application Proxy und eine nahtlose Verbund mit Azure AD, die wiederum ermöglicht.  Weitere Informationen finden Sie unter [Active Directory-Verbunddienste: Übersicht ](../../ad-fs/AD-FS-2016-Overview.md).

In der Reihenfolge für AD FS zum Authentifizieren von Benutzern aus einem LDAP-Verzeichnis, müssen Sie diese LDAP-Verzeichnis mit der AD FS-Farm verbinden, durch das Erstellen einer **lokales Anspruchsanbieter-Vertrauensstellung **.  Eine lokales Anspruchsanbieter-Vertrauensstellung ist ein Vertrauensstellungsobjekt, das ein LDAP-Verzeichnis, in der AD FS-Farm darstellt. Ein lokales Anspruchsanbieter-Vertrauensstellungsobjekt besteht aus einer Vielzahl von IDs, Namen und Regeln, die dieses LDAP-Verzeichnis für den lokalen Verbunddienst identifizieren.

Sie können angeben, unterstützen mehrere LDAP-Verzeichnissen, die jeweils ihre eigene Konfiguration innerhalb der gleichen AD FS-Farm durch Hinzufügen von mehreren **lokales Anspruchsanbieter-Vertrauensstellungen **. Darüber hinaus können Sie AD DS-Gesamtstrukturen, die nicht von der Gesamtstruktur als vertrauenswürdig, die AD FS lebt eingestuft werden in auch als lokales Anspruchsanbieter-Vertrauensstellungen modellieren. Sie können lokale Anspruchsanbieter-Vertrauensstellungen mit Windows PowerShell erstellen.

LDAP-Verzeichnissen (lokales Anspruchsanbieter-Vertrauensstellungen) können nebeneinander auf dem gleichen AD FS-Server innerhalb der gleichen AD FS-Farm mit AD-Verzeichnissen (Anspruchsanbieter-Vertrauensstellungen) existieren, kann sich daher, eine einzelne Instanz von AD FS zu authentifizieren und Autorisieren des Zugriffs für Benutzer, die in beiden gespeichert sind AD und Nicht-AD-Verzeichnissen.

Nur die formularbasierte Authentifizierung wird unterstützt, für die Authentifizierung von Benutzern von LDAP-Verzeichnissen. Zertifikatbasierte und die integrierte Windows-Authentifizierung werden nicht unterstützt, für die Authentifizierung von Benutzern in LDAP-Verzeichnissen.

Alle Protokolle für passive Autorisierung von AD FS, darunter SAML, WS-Federation, unterstützt werden und OAuth werden ebenfalls unterstützt, für die Identitäten, die in LDAP-Verzeichnissen gespeichert sind.

Die WS-Trust active Authorization-Protokoll wird auch für Identitäten unterstützt, die in LDAP-Verzeichnissen gespeichert sind.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>Konfigurieren von AD FS zum Authentifizieren von Benutzern in einem LDAP-Verzeichnis gespeichert
Um Ihre AD FS-Farm zum Authentifizieren von Benutzern aus einem LDAP-Verzeichnis zu konfigurieren, können Sie die folgenden Schritteausführen:

1.  Konfigurieren Sie zunächst eine Verbindung mit der LDAP-Verzeichnis mit den **neu AdfsLdapServerConnection** Cmdlet:

    ```
    $DirectoryCred = Get-Credential
    $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
    ```

    > [!NOTE]
    > Es wird empfohlen, dass Sie ein neues Verbindungsobjekt für jeden LDAP-Server erstellen, um eine Verbindung herstellen möchten. AD FS kann eine Verbindung mit mehreren Replikat LDAP-Server herstellen und automatisch ein Failover für den Fall, dass Sie ein bestimmten LDAP-Server ausfällt. Einem solchen Fall können Sie eine AdfsLdapServerConnection für jede dieser Replikat LDAP-Server erstellen und fügen Sie dann das Array von Verbindungsobjekten, die mit dem -**LdapServerConnection** -Parameter von der **hinzufügen AdfsLocalClaimsProviderTrust** Cmdlet.

    **Hinweis:** Sie versucht haben, Get-Credential und geben Sie einen DN und ein Kennwort verwenden, um auf eine Instanz des LDAP-Bindung verwendet werden kann zu einem Fehler führen, da die für die Anforderung für die Schnittstelle für spezifische Input Formate, z.B. DOMÄNE\Benutzername oder user@domain.tld. Sie können stattdessen das Cmdlet ConvertTo-SecureString wie folgt verwenden (im folgenden Beispiel wird angenommen, Benutzer-ID = Admin, Ou = System mit dem DN des die Anmeldeinformationen zum Binden an das LDAP-Instanz verwendet werden):

    ```
    $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
    $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
    ```

    Geben Sie das Kennwort für das Uid = Admin, und führen Sie die übrigen Schritteaus.

2.  Als Nächstes können Sie ausführen, den optionalen Schrittdie vorhandene AD FS-Ansprüche, die mithilfe von LDAP-Attribute Zuordnen der **neu AdfsLdapAttributeToClaimMapping** Cmdlet. Im folgenden Beispiel wird Sie Vorname, Nachname, zuordnen und CommonName LDAP-Attribute für die Ansprüche, die AD FS:

    ```
    #Map given name claim
    $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
    # Map surname claim
    $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
    # Map common name claim
    $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
    ```

    Diese Zuordnung wird vorgenommen, um die Attribute aus dem LDAP-Speicher als Ansprüche in AD FS zum Erstellen von Zugriffsregeln für bedingten Zugriff in AD FS zur Verfügung zu stellen. Darüber hinaus ermöglicht AD FS bietet eine einfache Möglichkeit zum Zuordnen von LDAP-Attribute für Ansprüche, die beim Arbeiten mit benutzerdefinierten Schemas in LDAP-Speicher.

3.  Sie müssen registrieren Sie abschließend die LDAP-Speicher mit AD FS wie ein lokales Anspruchsanbieter Anbieter Vertrauensstellung mit der **hinzufügen AdfsLocalClaimsProviderTrust** Cmdlet:

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

    Im obigen Beispiel erstellen Sie eine Vertrauensstellung mit lokalem Anspruchsanbieter "Kreditoren" bezeichnet. Sie Verbindungsinformationen für AD FS zur Verbindung mit des LDAP-Verzeichnis steht für diese lokalen Anspruchsanbieter-Vertrauensstellung durch Zuweisen angeben `$vendorDirectory`auf die `-LdapServerConnection`Parameter. Beachten Sie, dass die in Schritt1, Ihnen zugewiesene `$vendorDirectory`eine Verbindungszeichenfolge für die Verbindung mit bestimmten LDAP-Verzeichnis verwendet werden. Sie sind außerdem angeben, die die `$GivenName`, `$Surname`, und `$CommonName`LDAP-Attribute (mit dem Sie die AD FS-Ansprüche zugeordnet) sind für die Steuerung des bedingten Zugriffs, einschließlich Multi-Factor Authentication-Richtlinien und Ausstellungsautorisierungsregeln, sowie für die Ausstellung über Ansprüche in AD FS ausgestellten Sicherheitstoken verwendet werden. Active Protokolle wie Ws-Trust mit AD FS verwenden möchten, müssen Sie den OrganizationalAccountSuffix-Parameter angeben, der AD FS to lokales Anspruchsanbieter-Vertrauensstellungen zur Wartung einer aktiven autorisierungsanforderung eindeutig machen können.

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)


