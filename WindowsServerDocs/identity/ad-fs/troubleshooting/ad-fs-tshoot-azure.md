---
title: AD FS Problembehandlung-Azure AD
description: In diesem Dokument wird beschrieben, wie Sie verschiedene Aspekte von AD FS und Azure AD beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.openlocfilehash: d7941733ff2191e94c6c1e380d4349585a5c98d3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956177"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS Problembehandlung-Azure AD
Mit dem Wachstum der Cloud können viele Unternehmen Azure AD für ihre verschiedenen apps und Dienste nutzen.  Der Verbund mit Azure AD wurde in vielen Organisationen zu einer Standardübung.  In diesem Dokument werden einige Aspekte der Problembehandlung für diesen Verbund behandelt.  Einige der Themen im Dokument zur allgemeinen Problembehandlung betreffen weiterhin den Verbund mit Azure, sodass sich dieses Dokument auf Besonderheiten bei der Azure AD-und AD FS Interaktion konzentriert.

## <a name="redirection-to-ad-fs"></a>Umleitung zu AD FS

Die Umleitung erfolgt, wenn Sie sich bei einer Anwendung wie z. b. Office 365 anmelden und Sie an ihre Organisationen umgeleitet werden, AD FS Server sich anmelden.

![Umleitungs Bildschirm zum AD FS](media/ad-fs-tshoot-azure/azure1.png)

### <a name="first-things-to-check"></a>Zuerst zu überprüfen

Wenn keine Umleitung erfolgt, müssen Sie einige Dinge überprüfen.

1. Stellen Sie sicher, dass Ihr Azure AD Mandanten für den Verbund aktiviert ist, indem Sie sich beim Azure-Portal anmelden und unter Azure AD Connect einchecken.

   ![Bildschirm "Benutzeranmeldung" in Azure AD Connect](media/ad-fs-tshoot-azure/azure2.png)

2. Stellen Sie sicher, dass Ihre benutzerdefinierte Domäne überprüft wird, indem Sie in der Azure-Portal auf die Domäne neben Verbund klicken.

   ![Im Portal neben Verbund angezeigte Domäne](media/ad-fs-tshoot-azure/azure3.png)

3. Zum Schluss sollten Sie [DNS](ad-fs-tshoot-dns.md) überprüfen und sicherstellen, dass Ihre AD FS Server oder WAP-Server über das Internet aufgelöst werden.  Vergewissern Sie sich, dass dieser Vorgang aufgelöst wird und Sie dorthin navigieren können.

4. Sie können auch das PowerShell-Cmdlet verwenden `Get-AzureADDomain` , um diese Informationen zu erhalten.

   ![Bildschirm Abbildung von PowerShell-Cmdlets](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>Sie erhalten einen unbekannten Authentifizierungsmethoden Fehler.
Möglicherweise wird die Fehlermeldung "unbekannte Authentifizierungsmethode" angezeigt, die besagt, dass authncontext auf AD FS-oder STS-Ebene nicht unterstützt wird, wenn Sie von Azure umgeleitet werden.

Dies wird am häufigsten verwendet, wenn Azure AD mithilfe eines Parameters, der eine Authentifizierungsmethode erzwingt, zum AD FS oder STS weiterleitet.

Um eine Authentifizierungsmethode zu erzwingen, verwenden Sie eine der folgenden Methoden:
- Verwenden Sie für WS-Federation eine WAUTH-Abfrage Zeichenfolge, um eine bevorzugte Authentifizierungsmethode zu erzwingen.

- Verwenden Sie für SAML 2.0 Folgendes:
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  Wenn die erzwungene Authentifizierungsmethode mit einem falschen Wert gesendet wird oder wenn diese Authentifizierungsmethode auf AD FS oder STS nicht unterstützt wird, erhalten Sie eine Fehlermeldung, bevor Sie authentifiziert werden.

|Authentifizierungsmethode erwünscht|WAUTH-URI|
|-----|-----|
|Benutzernamen- und Kennwortauthentifizierung|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL-Client Authentifizierung|urn: IETF: RFC: 2246|
|Integrierte Windows-Authentifizierung|urn: Verbund: Authentifizierung: Windows|

Unterstützte SAML-Authentifizierungs Kontext Klassen

|Authentifizierungsmethode|URI der Authentifizierungs Kontext Klasse|
|-----|-----|
|Benutzername und Kennwort|urn:oasis:names:tc:SAML:2.0:ac:classes:Password|
|Kenn Wort geschützter Transport|urn: Oasis: names: TC: SAML: 2.0: AC: Classes: passwordprotectedtransport|
|Transport Layer Security (TLS)-Client|urn: Oasis: names: TC: SAML: 2.0: AC: Classes: tlsclient
|X.509-Zertifikat|urn: Oasis: names: TC: SAML: 2.0: AC: Classes: X509
|Integrierte Windows-Authentifizierung|urn: Verbund: Authentifizierung: Windows|
|Kerberos|urn: Oasis: names: TC: SAML: 2.0: AC: Classes: Kerberos|

Überprüfen Sie Folgendes, um sicherzustellen, dass die Authentifizierungsmethode auf AD FS Ebene unterstützt wird.

#### <a name="ad-fs-20"></a>AD FS 2.0

Stellen Sie sicher, dass unter **/adfs/ls/web.config**der Eintrag für den Authentifizierungstyp vorhanden ist.

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

Klicken Sie unter **AD FS Verwaltung**im AD FS-Snap-in auf **Authentifizierungs Richtlinien** .

Klicken Sie im Abschnitt **primäre Authentifizierung** neben globale Einstellungen auf Bearbeiten. Sie können auch mit der rechten Maustaste auf Authentifizierungs Richtlinien klicken und dann globale primäre Authentifizierung bearbeiten auswählen. Oder wählen Sie im Bereich Aktionen die Option globale primäre Authentifizierung bearbeiten aus.

Im Fenster Globale Authentifizierungs Richtlinie bearbeiten auf der Registerkarte Primär können Sie Einstellungen als Teil der globalen Authentifizierungs Richtlinie konfigurieren. Bei der primären Authentifizierung können Sie beispielsweise unter Extranet und Intranet verfügbare Authentifizierungsmethoden auswählen.

* * Stellen Sie sicher, dass das Kontrollkästchen erforderliche Authentifizierungsmethode aktiviert ist.

#### <a name="ad-fs-2016"></a>AD FS 2016

Klicken Sie unter **AD FS Verwaltung**auf **Dienst** -und **Authentifizierungsmethoden** im AD FS-Snap-in.

Klicken Sie im Abschnitt **primäre Authentifizierung** auf Bearbeiten.

Im Fenster " **Authentifizierungsmethoden bearbeiten** " können Sie auf der Registerkarte "Primär" Einstellungen als Teil der Authentifizierungs Richtlinie konfigurieren.

![Fenster "Authentifizierungsmethoden bearbeiten"](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>Von AD FS ausgestellte Token

### <a name="azure-ad-throws-error-after-token-issuance"></a>Azure AD löst nach der Tokenausstellung einen Fehler aus
Wenn AD FS ein Token ausgibt, kann Azure AD einen Fehler auslösen. Überprüfen Sie in diesem Fall die folgenden Probleme:
- Die Ansprüche, die von AD FS im Token ausgegeben werden, sollten den jeweiligen Attributen des Benutzers in Azure AD entsprechen.
- Das Token für Azure AD sollte die folgenden erforderlichen Ansprüche enthalten:
    - WSFED
        - UPN: der Wert dieses Anspruchs sollte mit dem UPN der Benutzer in Azure AD identisch sein.
        - Immutableid: der Wert dieses Anspruchs sollte mit "sourceanchor" oder "immutableid" des Benutzers in Azure AD identisch sein.

Um den Wert des Benutzer Attributs in Azure AD zu erhalten, führen Sie die folgende Befehlszeile aus:`Get-AzureADUser –UserPrincipalName <UPN>`

![Bildschirm Abbildung von PowerShell-Cmdlets](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2,0:
       - Idpeer Mail: der Wert dieses Anspruchs sollte mit dem Benutzer Prinzipal Namen der Benutzer in Azure AD identisch sein.
       - NameID: der Wert dieses Anspruchs sollte mit "sourceanchor" oder "immutableid" des Benutzers in Azure AD identisch sein.

Weitere Informationen finden Sie unter [Verwenden eines SAML 2,0-Identitäts Anbieters zum Implementieren von Single Sign-on](/previous-versions/azure/azure-services/dn641269(v=azure.100)).

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>Das Tokensignaturzertifikat ist zwischen AD FS und Azure AD nicht übereinstimmen.

AD FS verwendet das Tokensignaturzertifikat, um das Token zu signieren, das an den Benutzer oder die Anwendung gesendet wird. Die Vertrauensstellung zwischen dem AD FS und Azure AD ist eine Verbund Vertrauensstellung, die auf diesem Tokensignaturzertifikat basiert.

Wenn jedoch das Tokensignaturzertifikat auf der AD FS Seite aufgrund eines automatischen zertifikatrol Lovers oder durch einen gewissen Eingriff geändert wird, müssen die Details des neuen Zertifikats auf Azure AD Seite für die Verbund Domäne aktualisiert werden. Wenn das primäre Tokensignaturzertifikat für die AD FS von Azure ADS abweicht, wird das von AD FS ausgegebene Token von Azure AD nicht als vertrauenswürdig eingestuft. Der Verbund Benutzer darf sich daher nicht anmelden.

Um dieses Problem zu beheben, können Sie die Schritte in [Erneuern von Verbund Zertifikaten für Office 365 und Azure Active Directory](/azure/active-directory/connect/active-directory-aadconnect-o365-certs)verwenden.

## <a name="other-common-things-to-check"></a>Weitere gängige Dinge, die überprüft werden müssen
Im folgenden finden Sie eine kurze Liste der Dinge, die Sie überprüfen sollten, wenn Sie Probleme mit AD FS und Azure AD Interaktion haben.
- veraltete oder zwischengespeicherte Anmelde Informationen in Windows Credential Manager
- Der sichere Hash Algorithmus, der für die Vertrauensstellung der vertrauenden Seite für Office 365 konfiguriert ist, ist auf SHA1 festgelegt

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
