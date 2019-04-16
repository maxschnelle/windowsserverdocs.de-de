---
title: "Einzelne Abmeldung für OpenID Connect mit AD FS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3af10ec139edbc72e75bf80f544ac5b4f1cf9222
ms.sourcegitcommit: c16a2bf1b8a48ff267e71ff29f18b5e5cda003e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>Einzelne Abmeldung für OpenID Connect mit AD FS

## <a name="overview"></a>(Übersicht)
Erstellen der ersten Oauth-Unterstützung in AD FS unter Windows Server2012 R2 AD FS 2016, die Unterstützung für das OpenId Connect anmelden eingeführt. Mit [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801), AD FS 2016 jetzt einzelne Abmeldung für OpenId Connect-Szenarien unterstützt. Dieser Artikel enthält eine Übersicht über die einzelnen Abmeldung für Szenario OpenId Connect und enthält Informationen für Ihre Anwendung OpenId Connect in AD FS verwendet.


## <a name="discovery-doc"></a>Discovery-Dokument
OpenID Connect-Features ein JSON-Dokument namens "Ermittlung Dokument" Details zur Konfiguration bereitstellen.  Dazu gehören die URIs, der die Authentifizierung, Token, Userinfo und öffentlichen Endpunkte.  Im folgenden finden ein Beispiel für die Discovery-Dokument.

```
{
"issuer":"https://fs.fabidentity.com/adfs",
"authorization_endpoint":"https://fs.fabidentity.com/adfs/oauth2/authorize/",
"token_endpoint":"https://fs.fabidentity.com/adfs/oauth2/token/",
"jwks_uri":"https://fs.fabidentity.com/adfs/discovery/keys",
"token_endpoint_auth_methods_supported":["client_secret_post","client_secret_basic","private_key_jwt","windows_client_authentication"],
"response_types_supported":["code","id_token","code id_token","id_token token","code token","code id_token token"],
"response_modes_supported":["query","fragment","form_post"],
"grant_types_supported":["authorization_code","refresh_token","client_credentials","urn:ietf:params:oauth:grant-type:jwt-bearer","implicit","password","srv_challenge"],
"subject_types_supported":["pairwise"],
"scopes_supported":["allatclaims","email","user_impersonation","logon_cert","aza","profile","vpn_cert","winhello_cert","openid"],
"id_token_signing_alg_values_supported":["RS256"],
"token_endpoint_auth_signing_alg_values_supported":["RS256"],
"access_token_issuer":"http://fs.fabidentity.com/adfs/services/trust",
"claims_supported":["aud","iss","iat","exp","auth_time","nonce","at_hash","c_hash","sub","upn","unique_name","pwd_url","pwd_exp","sid"],
"microsoft_multi_refresh_token":true,
"userinfo_endpoint":"https://fs.fabidentity.com/adfs/userinfo",
"capabilities":[],
"end_session_endpoint":"https://fs.fabidentity.com/adfs/oauth2/logout",
"as_access_token_token_binding_supported":true,
"as_refresh_token_token_binding_supported":true,
"resource_access_token_token_binding_supported":true,
"op_id_token_token_binding_supported":true,
"rp_id_token_token_binding_supported":true,
"frontchannel_logout_supported":true,
"frontchannel_logout_session_supported":true
} 
 
```



Die folgenden zusätzlichen Werte in das Dokument Ermittlung an Unterstützung für Front-Kanal Abmelden zur Verfügung:

- Frontchannel_logout_supported: Wert ist "true",
- Frontchannel_logout_session_supported: Wert wird "true" sein.
- End_session_endpoint: Hierbei handelt es sich um die OAuth-Abmeldung URI, mit denen der Client Abmelden auf dem Server zu initiieren.


## <a name="ad-fs-server-configuration"></a>AD FS-Serverkonfiguration
Die AD FS-Eigenschaft EnableOAuthLogout wird standardmäßig aktiviert.  Diese Eigenschaft weist AD FS-Server, für die URL (LogoutURI) suchen, mit der SID zum Abmelden auf dem Client zu initiieren. Wenn Sie keinen [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) installiert ist, können Sie den folgenden PowerShell-Befehl verwenden:

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout` Parameter werden als veraltet markiert werden nach der Installation von [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801). `EnableOAUthLogout` Immer "true" und hat keine Auswirkung auf die Abmeldefunktionalität.

>[!NOTE]
>Frontchannel_logout wird unterstützt **nur** nach um installieren [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)

## <a name="client-configuration"></a>Client-Konfiguration
Client muss zu einer URL implementieren, die 'der angemeldete Benutzer sich abmeldet'. Administrator kann die LogoutUri in der Clientkonfiguration mit den folgenden PowerShell-Cmdlets konfigurieren. 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

Die `LogoutUri`lautet die URL zur Bestimmung von FS AF "den Benutzer abmelden". Für die Implementierung der `LogoutUri`, um sicherzustellen, dass die Client-Anforderungen löscht den Authentifizierungszustand des Benutzers in der Anwendung, z.B. die Authentifizierung ablegen Token hat. AD FS wird die URL, mit der SID als Abfrageparameter, hat die vertrauende Seite durchsuchen/Anwendung, die der Benutzer abgemeldet. 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **OAuth-Token mit Sitzungs-ID**: umfasst AD FS Sitzungs-ID in das OAuth-Token zum Zeitpunkt der ID_Token tokenausstellungs. Dies wird später von AD FS verwendet werden, identifizieren Sie die relevanten SSO Cookies für den Benutzer bereinigt werden.
2.  **Benutzer initiiert Abmelden auf App1**: der Benutzer kann eine Abmeldung von einer der angemeldeten Anwendungen initiieren. In diesem Beispielszenario startet ein Benutzer eine Abmeldung von App1.
3.  **Anwendung sendet Abmelde-Anforderung an AD FS**: Nachdem der Benutzer die Abmeldung initiiert, die Anwendung sendet eine GET-Anforderung an End_session_endpoint von AD FS. Die Anwendung kann optional ID_Token_hint als Parameter für diese Anforderung enthalten. Wenn ID_Token_hint vorhanden ist, wird AD FS in Verbindung mit der Sitzungs-ID verwendet um herauszufinden, welche, die URI nach der Abmeldung (Post_logout_redirect_uri) des Clients in umgeleitet werden sollen.  Die Post_logout_redirect_uri sollte es sich um einen gültigen Uri mit AD FS unter Verwendung des Parameters RedirectUris registriert sein.
4.  **AD FS sendet angemeldeten Clients Abmeldung**: AD FS verwendet, die auf der Bezeichnerwert Sitzung, die entsprechenden Clients den Benutzer angemeldet ist. Die identifizierten Clients sind auf die mit AD FS So initiieren Sie eine Abmeldung auf dem Client registriert LogoutUri Anforderung gesendet.

## <a name="faqs"></a>Häufig gestellte Fragen
**F:** Frontchannel_logout_supported und Frontchannel_logout_session_supported Parameter in der Discovery-Dokument nicht angezeigt.</br>
**A:** sicherstellen, dass die [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) für alle AD FS-Server installiert. Weitere Informationen finden Sie in einzelnen Abmeldung in Server2016 mit [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801).

**F:** ich einzelne Abmeldung wie beschrieben konfiguriert haben, aber Benutzer bleibt angemeldeten auf anderen Clients.</br>
**A:** sicher, dass `LogoutUri`festgelegt für alle Clients ist, in dem der Benutzer angemeldet ist. Zudem führt das AD FS einen günstigsten Versuch zum Senden der Abmeldung Anforderung auf den registrierten `LogoutUri`. Client muss die Logik zum Verarbeiten der Anforderungs und Maßnahmen zum Abmelden des Benutzers von der Anwendung implementieren.</br>

**F:** Falls nach der Abmeldung, die Clients zurück zu AD FS mit ein gültiges Aktualisierungstoken auftritt, werden ein Zugriffstoken AD FS ausstellen?</br>
**A:** Ja. Es wird der Client-Anwendung, alle authentifizierten Artefakte zu löschen, nachdem eine Abmelde Anforderung empfangen wurde auf den registrierten `LogoutUri`.


## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
