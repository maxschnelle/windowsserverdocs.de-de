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
ms.openlocfilehash: 87ada412e6b4ab47aa18a62953b84d8a1369dffa
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544515"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>Konfigurieren von AD FS zum Authentifizieren von Benutzern, die in LDAP-Verzeichnissen gespeichert sind

Im folgenden Thema wird die Konfiguration beschrieben, die erforderlich ist, um Ihre AD FS-Infrastruktur zum Authentifizieren von Benutzern zu aktivieren, deren Identitäten in LDAP-kompatiblen Verzeichnissen (Lightweight Directory Access Protocol) gespeichert sind.

In vielen Organisationen bestehen Lösungen zur Identitätsverwaltung aus einer Kombination aus Active Directory-, AD LDS-oder LDAP-Verzeichnissen von Drittanbietern. Durch das Hinzufügen AD FS Unterstützung für die Authentifizierung von Benutzern, die in LDAP-kompatiblen Verzeichnissen gespeichert sind, können Sie von der gesamten Unternehmensklasse AD FS Featuresatz profitieren, unabhängig davon, wo Ihre Benutzer Identitäten gespeichert werden. AD FS unterstützt ein beliebiges LDAP-V3-kompatibles Verzeichnis.

> [!NOTE]
> Zu den AD FS Features zählen einmaliges Anmelden (Single Sign-on, SSO), Geräte Authentifizierung, flexible Richtlinien für den bedingten Zugriff, Unterstützung für die Arbeit von überall über die Integration mit dem webanwendungsproxy und nahtloser Verbund mit Azure AD, der wiederum ermöglicht Ihnen und ihren Benutzern die Nutzung der Cloud, einschließlich Office 365 und anderer SaaS-Anwendungen.  Weitere Informationen finden Sie unter [Active Directory-Verbunddienste (AD FS) Übersicht](../../ad-fs/AD-FS-2016-Overview.md).

Damit AD FS Benutzer von einem LDAP-Verzeichnis authentifizieren können, müssen Sie dieses LDAP-Verzeichnis mit Ihrer AD FS Farm verbinden, indem Sie eine **lokale Anspruchs Anbieter-Vertrauens**Stellung erstellen.  Eine lokale Anspruchs Anbieter-Vertrauensstellung ist ein Vertrauensstellungs Objekt, das ein LDAP-Verzeichnis in Ihrer AD FS Farm darstellt. Ein lokales Anspruchs Anbieter-Vertrauensstellungs Objekt besteht aus einer Vielzahl von Bezeichnernamen, Namen und Regeln, die dieses LDAP-Verzeichnis für den lokalen Verbund Dienst identifizieren.

Sie können mehrere LDAP-Verzeichnisse unterstützen, die jeweils über eine eigene Konfiguration innerhalb derselben AD FS Farm verfügen, indem Sie mehrere **lokale Anspruchs Anbieter**-Vertrauens Stellungen hinzufügen. Außerdem können AD DS Gesamtstrukturen, die von der Gesamtstruktur, in der AD FS Leben, nicht als vertrauenswürdig eingestuft werden. Sie können lokale Anspruchs Anbieter-Vertrauens Stellungen mithilfe von Windows PowerShell erstellen.

LDAP-Verzeichnisse (lokale Anspruchs Anbieter-Vertrauens Stellungen) können zusammen mit AD-Verzeichnissen (Anspruchs Anbieter-Vertrauens Stellungen) auf demselben AD FS Server innerhalb derselben AD FS Farm vorhanden sein. Daher ist eine einzelne Instanz von AD FS in der Lage, den Zugriff für Benutzer zu authentifizieren und zu autorialisieren, die in AD-und nicht-AD-Verzeichnissen gespeichert.

Zum Authentifizieren von Benutzern von LDAP-Verzeichnissen wird nur die Formular basierte Authentifizierung unterstützt. Die Zertifikat basierte und die integrierte Windows-Authentifizierung werden nicht für die Authentifizierung von Benutzern in LDAP-Verzeichnissen unterstützt.

Alle passiven Autorisierungs Protokolle, die von AD FS unterstützt werden, einschließlich SAML, WS-Federation und OAuth, werden auch für Identitäten unterstützt, die in LDAP-Verzeichnissen gespeichert sind.

Das WS-Trust Active Authorization-Protokoll wird auch für Identitäten unterstützt, die in LDAP-Verzeichnissen gespeichert sind.

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>Konfigurieren AD FS für die Authentifizierung von Benutzern, die in einem LDAP-Verzeichnis gespeichert sind
Führen Sie die folgenden Schritte aus, um die AD FS-Farm zum Authentifizieren von Benutzern über ein LDAP-Verzeichnis zu konfigurieren:

1. Konfigurieren Sie zunächst mithilfe des Cmdlets **New-adfsldapserverconnection** eine Verbindung mit Ihrem LDAP-Verzeichnis:

   ```
   $DirectoryCred = Get-Credential
   $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
   ```

   > [!NOTE]
   > Es wird empfohlen, ein neues Verbindungs Objekt für jeden LDAP-Server zu erstellen, mit dem Sie eine Verbindung herstellen möchten. AD FS können eine Verbindung mit mehreren Replikat-LDAP-Servern herstellen und automatisch ein Failover ausführen, falls ein bestimmter LDAP-Server ausfällt. In einem solchen Fall können Sie für jeden dieser LDAP-Replikat Server eine adfsldapserverconnection erstellen und dann das Array der Verbindungs Objekte mithilfe des Parameters-**ldapserverconnection** des Cmdlets **Add-adfslocalclaimsprovidertrust** hinzufügen.

   **HINWEIS:** Der Versuch, Get-Credential zu verwenden und einen DN und ein Kennwort einzugeben, die für die Bindung an eine LDAP-Instanz verwendet werden, kann aufgrund der Benutzeroberflächen Anforderung für bestimmte Eingabeformate (z. b. Domäne \ Benutzer user@domain.tldName oder) zu einem Fehler führen. Stattdessen können Sie das ConvertTo-SecureString-Cmdlet wie folgt verwenden (im Beispiel unten wird UID = admin, ou = System als DN der Anmelde Informationen verwendet, die für die Bindung an die LDAP-Instanz verwendet werden sollen):

   ```
   $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
   $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
   ```

   Geben Sie dann das Kennwort für UID = admin ein, und führen Sie die restlichen Schritte aus.

2. Als nächstes können Sie den optionalen Schritt der Zuordnung von LDAP-Attributen zu den vorhandenen AD FS Ansprüchen mithilfe des Cmdlets **New-adfsldapattributetoclaimmapping** ausführen. Im folgenden Beispiel ordnen Sie die LDAP-Attribute "givenName", "Nachname" und "CommonName" den AD FS Ansprüchen zu:

   ```
   #Map given name claim
   $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
   # Map surname claim
   $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
   # Map common name claim
   $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
   ```

   Diese Zuordnung erfolgt, um Attribute aus dem LDAP-Speicher als Ansprüche in AD FS verfügbar zu machen, um Regeln für die bedingte Zugriffs Steuerung in AD FS zu erstellen. Außerdem ermöglicht es AD FS das Arbeiten mit benutzerdefinierten Schemas in LDAP-speichern, indem es eine einfache Möglichkeit bietet, LDAP-Attribute Anspruchs Karten zuzuordnen.

3. Zum Schluss müssen Sie den LDAP-Speicher bei AD FS als lokale Anspruchs Anbieter-Vertrauensstellung mithilfe des Cmdlets **Add-ADF slocalclaimsprovidertrust** registrieren:

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

   Im obigen Beispiel erstellen Sie eine lokale Anspruchs Anbieter-Vertrauensstellung mit dem Namen "Lieferanten". Sie geben Verbindungsinformationen für AD FS zum Herstellen einer Verbindung mit dem LDAP-Verzeichnis an, das diese lokale Anspruchs `$vendorDirectory` Anbieter- `-LdapServerConnection` Vertrauensstellung darstellt, indem Sie dem-Parameter zuweisen. Beachten Sie, dass Sie in Schritt 1 eine `$vendorDirectory` Verbindungs Zeichenfolge zugewiesen haben, die beim Herstellen einer Verbindung mit Ihrem spezifischen LDAP-Verzeichnis verwendet werden soll. Schließlich geben Sie an, dass die `$GivenName`LDAP `$Surname`-Attribute `$CommonName` , und (die Sie den AD FS Ansprüchen zugeordnet haben) für die bedingte Zugriffs Steuerung verwendet werden sollen, einschließlich Multi-Factor Authentication-Richtlinien und Ausstellung. Autorisierungs Regeln sowie für die Ausstellung über Ansprüche in AD FS ausgestellten Sicherheits Token. Um aktive Protokolle wie WS-Trust mit AD FS zu verwenden, müssen Sie den organizationalaccountsuffix-Parameter angeben, der es AD FS ermöglicht, bei der Wartung einer aktiven Autorisierungs Anforderung zwischen lokalen Anspruchs Anbieter-Vertrauens Stellungen zu unterscheiden.

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)


