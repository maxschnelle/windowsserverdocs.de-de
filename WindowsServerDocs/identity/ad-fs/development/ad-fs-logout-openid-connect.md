---
title: Einmaliges Abmelden für OpenID Connect mit AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.openlocfilehash: 1ab6735e09d912bac5b1a319a3793ee6e0c70fa2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964937"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>Einmaliges Abmelden für OpenID Connect mit AD FS

## <a name="overview"></a>Übersicht
Bei der anfänglichen OAuth-Unterstützung in AD FS in Windows Server 2012 R2 hat AD FS 2016 die Unterstützung für die OpenID Connect-Anmeldung eingeführt. Mit [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)unterstützt AD FS 2016 jetzt das einmalige abmelden für OpenID Connect-Szenarios. Dieser Artikel bietet eine Übersicht über das Szenario für die einmalige Abmeldung für OpenID Connect und bietet Anleitungen zur Verwendung für Ihre OpenID Connect-Anwendungen in AD FS.


## <a name="discovery-doc"></a>Discovery-Dokument
OpenID Connect verwendet ein JSON-Dokument mit dem Namen "Discovery Document", um Details zur Konfiguration bereitzustellen.  Dies schließt URIs der Authentifizierung, des Tokens, der userinfo und der öffentlichen Endpunkte ein.  Im folgenden finden Sie ein Beispiel für das Discovery-Dokument.

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



Die folgenden zusätzlichen Werte sind im Discovery doc verfügbar, um die Unterstützung für die Front-Channel-Abmeldung anzuzeigen:

- frontchannel_logout_supported: der Wert ist "true".
- frontchannel_logout_session_supported: der Wert ist "true".
- end_session_endpoint: Dies ist der OAuth-Abmelde-URI, den der Client verwenden kann, um die Abmeldung auf dem Server zu initiieren.


## <a name="ad-fs-server-configuration"></a>AD FS Server-Konfiguration
Die AD FS-Eigenschaft "enableoauthlogout" wird standardmäßig aktiviert.  Diese Eigenschaft weist den AD FS Server an, die URL (logouturi) mit der SID zu durchsuchen, um die Abmeldung auf dem Client zu initiieren.
Wenn [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) nicht installiert ist, können Sie den folgenden PowerShell-Befehl verwenden:

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout`der Parameter wird nach der Installation von [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)als veraltet markiert. `EnableOAUthLogout`ist immer true und wirkt sich nicht auf die Abmelde Funktionalität aus.

>[!NOTE]
>frontchannel_logout wird **erst** nach der Installation von [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) unterstützt.

## <a name="client-configuration"></a>Clientkonfiguration
Der Client muss eine URL implementieren, mit der der angemeldete Benutzer protokolliert wird. Der Administrator kann logouturi in der Client Konfiguration mithilfe der folgenden PowerShell-Cmdlets konfigurieren.


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

`LogoutUri`Ist die URL, die von AF FS zum Abmelden des Benutzers verwendet wird. Zum Implementieren `LogoutUri` von muss der Client sicherstellen, dass er den Authentifizierungs Zustand des Benutzers in der Anwendung löscht, z. b. das Löschen der Authentifizierungs Token, die er besitzt. AD FS navigieren zu dieser URL, wobei die SID als Abfrage Parameter verwendet wird, und signalisiert der vertrauenden Seite/Anwendung, den Benutzer abzumelden.

![AD FS-Abmelde Benutzer Diagramm](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)

1.  **OAuth-Token mit Sitzungs-ID**: AD FS enthält eine Sitzungs-ID im OAuth-Token zum Zeitpunkt der id_token Tokenausstellung. Diese wird später AD FS verwendet, um die relevanten SSO-Cookies zu identifizieren, die für den Benutzer bereinigt werden sollen.
2.  Der **Benutzer initiiert die Abmeldung auf App1**: der Benutzer kann eine Abmeldung von allen angemeldeten Anwendungen initiieren. In diesem Beispielszenario initiiert ein Benutzer eine Abmeldung von App1.
3.  Die Anwendung sendet eine Abmelde **Anforderung an AD FS**: Nachdem der Benutzer die Abmeldung initiiert hat, sendet die Anwendung eine GET-Anforderung an end_session_endpoint von AD FS. Die Anwendung kann optional id_token_hint als Parameter für diese Anforderung einschließen. Wenn id_token_hint vorhanden ist, wird Sie von AD FS zusammen mit der Sitzungs-ID verwendet, um herauszufinden, an welchen URI der Client nach der Abmeldung umgeleitet werden soll (post_logout_redirect_uri).  Der post_logout_redirect_uri muss ein gültiger URI sein, der bei AD FS mithilfe des Parameters redirecturis registriert ist.
4.  **AD FS sendet die Abmeldung an angemeldete Clients**: AD FS verwendet den Sitzungs-ID-Wert, um die relevanten Clients zu finden, bei denen der Benutzer angemeldet ist. Die identifizierten Clients werden an den logouturi gesendet, der bei AD FS registriert ist, um eine Abmeldung auf der Clientseite zu initiieren.

## <a name="faqs"></a>Häufig gestellte Fragen
**F:** Die Parameter "frontchannel_logout_supported" und "frontchannel_logout_session_supported" werden im Discovery-Dokument nicht angezeigt.</br>
**A:** Stellen Sie sicher, dass [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) auf allen AD FS Servern installiert ist. Weitere Informationen finden Sie unter Single Log-out in Server 2016 with [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801).

**F:** Ich habe die einmalige Abmeldung wie angegeben konfiguriert, aber der Benutzer bleibt bei anderen Clients angemeldet.</br>
**A:** Stellen Sie sicher, dass `LogoutUri` für alle Clients, auf denen der Benutzer angemeldet ist, festgelegt ist. Außerdem führt AD FS einen optimalen Versuch aus, die Abmelde Anforderung für die registrierte zu senden `LogoutUri` . Der Client muss Logik implementieren, um die Anforderung zu verarbeiten und Maßnahmen zum Abmelden des Benutzers aus der Anwendung zu ergreifen.</br>

**F:** Wenn ein Client nach der Abmeldung an AD FS mit einem gültigen Aktualisierungs Token zurückgeht, AD FS ein Zugriffs Token ausgeben?</br>
**A:** Ja. Die Client Anwendung muss alle authentifizierten Artefakte löschen, nachdem eine Abmelde Anforderung beim registrierten empfangen wurde `LogoutUri` .


## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)
