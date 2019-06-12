---
title: AD FS-Problembehandlung – Azure AD
description: In diesem Dokument wird beschrieben, wie verschiedene Aspekte des AD FS und Azure AD-Problembehandlung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 228ef34ab25276c1cf98f9b2b64e997390023c87
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444011"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS-Problembehandlung – Azure AD
Mit dem Wachstum der Cloud wurden viele Unternehmen über Azure AD für ihre verschiedenen apps und Dienste verschieben.  Den Verbund mit Azure AD ist ein Standardverfahren für viele Organisationen geworden.  In diesem Dokument behandelt einige der Aspekte der Behandlung von Problemen, die mit diesen Verbund auftreten.  Einige der in den Themen in des Dokuments die allgemeine Problembehandlung noch beziehen sich auf den Verbund mit Azure, damit in diesem Dokument auf nur Besonderheiten in Azure AD Fokus wird und AD FS-Interaktion.

## <a name="redirection-to-ad-fs"></a>Umleitung an AD FS
Umleitung tritt auf, wenn Sie anmelden, um eine Anwendung z. B. Office 365, und Sie "umgeleitet sind" zu Ihrer Organisation AD FS-Server anmelden.

![](media/ad-fs-tshoot-azure/azure1.png)


### <a name="first-things-to-check"></a>Erste Schritte zur überprüfen
Wenn die Umleitung nicht ausgeführt wird, dass es einige Dinge, das Sie überprüfen möchten

   1. Stellen Sie sicher, dass Azure AD-Mandanten für Verbund durch Anmeldung beim Azure-Portal, und überprüfen unter Azure AD Connect aktiviert ist.

![](media/ad-fs-tshoot-azure/azure2.png)

1. Stellen Sie sicher, dass Ihre benutzerdefinierte Domäne überprüft wurde, indem Sie in der Domäne neben Verbund im Azure-Portal auf.
   ![](media/ad-fs-tshoot-azure/azure3.png)

2. Zum Schluss Sie überprüfen möchten [DNS](ad-fs-tshoot-dns.md) und stellen Sie sicher, dass Ihre AD FS-Server oder die WAP-Server über das Internet aufgelöst werden.  Stellen Sie sicher, dass dies aufgelöst wird und Sie dorthin navigieren können.
3. Sie können auch das PowerShell-Cmdlet `Get-AzureADDomain` auf diese Informationen auch abrufen.

![](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>Sie erhalten einen Fehler der unbekannte Auth-Methode
Sie können auftreten, eine "Unbekannte Authentifizierungsmethode" Fehler, die besagt, dass AuthnContext auf der AD FS oder den STS-Ebene nicht unterstützt wird, wenn Sie von Azure weitergeleitet werden. 

Das geschieht meistens, wenn es sich bei Azure AD umgeleitet, die AD FS oder STS mithilfe eines Parameters, das eine Authentifizierungsmethode erzwingt. 

Um eine Authentifizierungsmethode zu erzwingen, verwenden Sie eine der folgenden Methoden:
- Verwenden Sie für die WS-Verbund eine WAUTH-Abfragezeichenfolge, um eine bevorzugte Authentifizierungsmethode zu erzwingen.

- Verwenden Sie für SAML2.0 die folgenden Schritte aus:
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  Wenn die erzwungene Authentifizierungsmethode mit einem falschen Wert gesendet wird oder wenn diese Authentifizierungsmethode für AD FS oder STS nicht unterstützt wird, erhalten Sie eine Fehlermeldung angezeigt, bevor Sie authentifiziert sind.

|Authentifizierungsmethode möchten|Wauth-URI|
|-----|-----|
|Authentifizierung mit Benutzername und Kennwort|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL-Clientauthentifizierung|urn:ietf:rfc:2246|
|Integrierte Windows-Authentifizierung|urn:federation:authentication:windows|

Unterstützte Kontextklassen der SAML-Authentifizierung

|Authentifizierungsmethode|Authentication Context URI-Klasse|
|-----|-----| 
|Benutzername und Kennwort|urn:oasis:names:tc:SAML:2.0:ac:classes:Password|
|Ein Kennwort geschützt transport|urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport|
|Transport Layer Security (TLS)-client|urn:oasis:names:tc:SAML:2.0:ac:classes:TLSClient
|X.509-Zertifikat|urn:oasis:names:tc:SAML:2.0:ac:classes:X509
|Integrierte Windows-Authentifizierung|urn:federation:authentication:windows|
|Kerberos|urn:oasis:names:tc:SAML:2.0:ac:classes:Kerberos|

Überprüfen Sie die folgenden Schritte aus, um sicherzustellen, dass die Authentifizierungsmethode auf AD FS-Ebene unterstützt wird.

#### <a name="ad-fs-20"></a>AD FS 2.0 

Klicken Sie unter **/adfs/ls/web.config**, stellen Sie sicher, dass der Eintrag für den Authentifizierungstyp vorhanden ist.

```
<microsoft.identityServer.web>
<localAuthenticationTypes>
<add name="Forms" page="FormsSignIn.aspx" />
<add name="Integrated" page="auth/integrated/" />
<add name="TlsClient" page="auth/sslclient/" />
<add name="Basic" page="auth/basic/" />
</localAuthenticationTypes>
```

#### <a name="ad-fs-2012-r2"></a>AD FS 2012 R2

Klicken Sie unter **AD FS-Verwaltung**, klicken Sie auf **Authentifizierungsrichtlinien** in der AD FS-Snap-in.

In der **primäre Authentifizierung** auf "Bearbeiten" neben der globalen Einstellungen. Sie können auch Maustaste Authentifizierungsrichtlinien und wählen Sie dann auf globale primäre Authentifizierung bearbeiten. Oder wählen Sie im Aktionsbereich, globale primäre Authentifizierung bearbeiten.

Klicken Sie im Fenster globale Authentifizierungsrichtlinie bearbeiten können auf der Registerkarte "primäre" Sie Einstellungen als Teil der globalen Authentifizierungsrichtlinie konfigurieren. Für die primäre Authentifizierung, können Sie z. B. unter Extranet und Intranet verfügbaren Authentifizierungsmethoden auswählen.

** Stellen Sie sicher, dass die erforderliche Authentifizierung Methode Kontrollkästchen aktiviert ist. 

#### <a name="ad-fs-2016"></a>AD FS 2016

Klicken Sie unter **AD FS-Verwaltung**, klicken Sie auf **Service** und **Authentifizierungsmethoden** in der AD FS-Snap-in.

In der **primäre Authentifizierung** auf Bearbeiten.

In der **Authentifizierungsmethoden bearbeiten** Fenster auf der Registerkarte "primäre" können Sie Einstellungen konfigurieren, als Teil der Authentifizierungsrichtlinie.

![](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>Von AD FS ausgestellten Token

### <a name="azure-ad-throws-error-after-token-issuance"></a>Azure AD löst Fehler aus, nach der Ausstellung von token
Nach der AD FS ein Token ausgibt, kann Azure AD einen Fehler auslösen. Überprüfen Sie in diesem Fall die folgenden Probleme:
- Die Ansprüche, die von AD FS in Token ausgegeben werden, sollten die entsprechenden Attribute des Benutzers in Azure AD abzugleichen.
- Das Token für Azure AD sollte die folgenden erforderlichen Ansprüche enthalten:
    - WSFED: 
        - UPN: Der Wert dieses Anspruchs sollte den UPN der Benutzer in Azure AD abzugleichen.
        - ImmutableID: Der Wert dieses Anspruchs soll das "sourceanchor" oder die ImmutableID des Benutzers in Azure AD abzugleichen.

Um den Attributwert für den Benutzer in Azure AD zu erhalten, führen Sie die folgende Befehlszeile ein: `Get-AzureADUser –UserPrincipalName <UPN>`

![](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2.0:
       - IDPEmail: Der Wert dieses Anspruchs sollte die Benutzerprinzipalnamen der Benutzer in Azure AD abzugleichen.
       - NAMEID: Der Wert dieses Anspruchs soll das "sourceanchor" oder die ImmutableID des Benutzers in Azure AD abzugleichen.

Weitere Informationen finden Sie unter [verwenden Sie einen SAML 2.0-Identitätsanbieter, um einmaliges Anmelden implementieren](https://technet.microsoft.com/library/dn641269.aspx).

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>Token-signing Certificate-Konflikt zwischen AD FS und Azure AD.

AD FS verwendet das Token-signing-Zertifikat zum Signieren des Tokens, die für den Benutzer oder die Anwendung gesendet wird. Die Vertrauensstellung zwischen dem AD FS und Azure AD ist eine verbundvertrauensstellung, die für dieses Token-signing-Zertifikat basiert.

Wenn das Token-Signaturzertifikat auf der AD FS-Seite aufgrund automatische Zertifikatrollover oder ein Eingreifen geändert wird, müssen jedoch die Details des neuen Zertifikats auf der Azure AD-Seite für die verbunddomäne aktualisiert werden. Wenn das primäre Tokensignaturzertifikat für die AD FS, Azure ADs unterscheidet, wird das Token, das von AD FS ausgestellt wird nicht von Azure AD vertraut. Aus diesem Grund ist der verbundene Benutzer zur Anmeldung nicht zulässig.

Zum Beheben dieses Problems Sie können die Schritte werden [Erneuern von verbundzertifikaten für Office 365 und Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs).

## <a name="other-common-things-to-check"></a>Andere allgemeinen Überprüfungen
Folgendes ist eine Liste der Dinge zu überprüfen, ob Sie mit AD FS und Azure AD-Interaktion Probleme auftreten.
- Veraltete oder zwischengespeicherte Anmeldeinformationen in der Windows-Anmeldeinformationsverwaltung
- Sicheren Hashalgorithmus, der auf die vertrauenden Seite Vertrauensstellung für Office 365 konfiguriert ist wird 1 als Standardoption festgelegt.

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)