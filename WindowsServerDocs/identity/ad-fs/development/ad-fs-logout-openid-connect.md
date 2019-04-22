---
title: Einzelne Abmeldung für OpenID Connect mit AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3af10ec139edbc72e75bf80f544ac5b4f1cf9222
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825771"
---
#  <a name="single-log-out-for-openid-connect-with-ad-fs"></a>Einzelne Abmeldung für OpenID Connect mit AD FS

## <a name="overview"></a>Übersicht
Erstellen auf die erste Oauth-Unterstützung in AD FS unter Windows Server 2012 R2, AD FS 2016, die Unterstützung für die OpenId Connect-Anmeldung eingeführt. Mit [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801), AD FS 2016 unterstützt jetzt einmaligen Abmeldens für OpenId Connect-Szenarien. Dieser Artikel bietet eine Übersicht über die einmaligen Abmeldens für OpenId Connect-Szenario und enthält Anleitungen für die OpenId Connect-Anwendungen in AD FS zu verwenden.


## <a name="discovery-doc"></a>Discovery-Dokument
Ein JSON-Dokument namens "Discovery-Dokument" OpenID Connect verwendet, um Details zur Konfiguration anzugeben.  Dies schließt die URIs der die Authentifizierung, Token, Benutzerinformationen und Public-Endpunkte.  Folgendes ist ein Beispiel für das Discovery-Dokument.

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



Die folgenden zusätzlichen Werte werden im Discovery-Dokument um die Unterstützung für die Front-Kanal Logout verfügbar:

- Frontchannel_logout_supported: Wert ist 'true',
- Frontchannel_logout_session_supported: Wert ist 'true' sein.
- End_session_endpoint: Hierbei handelt es sich um den OAuth-Abmelde-URI, mit denen der Client Abmeldung auf dem Server initiieren.


## <a name="ad-fs-server-configuration"></a>AD FS-Server-Konfiguration
Die AD FS-Eigenschaft EnableOAuthLogout wird standardmäßig aktiviert.  Diese Eigenschaft gibt die AD FS-Server, um die URL (LogoutURI) zu suchen, mit der SID einleiten Abmeldung auf dem Client. Wenn Sie keine [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) installiert ist, können Sie den folgenden PowerShell-Befehl:

```PowerShell
Set-ADFSProperties -EnableOAuthLogout $true
```

>[!NOTE]
> `EnableOAuthLogout` Parameter werden als veraltet markiert werden nach der Installation von [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801). `EnableOAUthLogout` ist immer "true", und hat keine Auswirkung auf die Abmeldefunktionalität.

>[!NOTE]
>Frontchannel_logout wird unterstützt **nur** nach dem Installieren von der [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801)

## <a name="client-configuration"></a>Client-Konfiguration
Client muss eine Url zu implementieren, die "des angemeldeten Benutzers abmeldet". Administrator kann die LogoutUri in der Clientkonfiguration, die mit den folgenden PowerShell-Cmdlets konfigurieren. 


- `(Add | Set)-AdfsNativeApplication`
- `(Add | Set)-AdfsServerApplication`
- `(Add | Set)-AdfsClient`

```PowerShell
Set-AdfsClient -LogoutUri <url>
```

Die `LogoutUri` ist die Url, die von AF-FS verwendet, um "den Benutzer abmelden". Für die Implementierung der `LogoutUri`, der Client benötigt, um sicherzustellen, dass löscht den Authentifizierungszustand des Benutzers in der Anwendung, z. B. Token löschen die Authentifizierung, aufweist. AD FS wird navigieren Sie zu dieser URL, mit der SID des Abfrageparameters, signalisiert die relying Party / Anwendung, um den Benutzer abzumelden. 

![](media/ad-fs-logout-openid-connect/adfs_single_logout2.png)


1.  **OAuth-Token mit der Sitzungs-ID**: Zum Zeitpunkt der Ausstellung von token "id_token" umfasst AD FS die Sitzungs-Id in das OAuth-Token. Dies wird später von AD FS verwendet werden, zum Identifizieren der entsprechenden SSO-Cookies für den Benutzer bereinigt werden.
2.  **Benutzer initiiert die Abmeldung auf dem Computer App1**: Der Benutzer kann das Einleiten einer Abmeldung von einem angemeldeten Anwendungen. In diesem Beispielszenario wird ein Benutzer eine Abmeldung von App1 initiiert.
3.  **Anwendung sendet eine abmeldeanforderung an AD FS**: Nachdem der Benutzer abmelden initiiert, sendet die Anwendung eine GET-Anforderung an End_session_endpoint von AD FS. Die Anwendung kann optional "id_token_hint" als Parameter für diese Anforderung enthalten. Wenn "id_token_hint" vorhanden ist, wird AD FS in Verbindung mit der Sitzungs-ID verwendet um zu ermitteln, welche, die URI nach der Abmeldung (Post_logout_redirect_uri) des Clients an umgeleitet werden soll.  Die Post_logout_redirect_uri muss ein gültiger Uri, der mit AD FS mithilfe des Parameters RedirectUris registriert.
4.  **AD FS sendet Abmeldung angemeldet Clients**: AD FS verwendet den Sitzungs-ID-Wert, um die entsprechenden Clients zu finden, bei denen der Benutzer angemeldet ist. Die angegebenen Clients werden Anforderung auf die mit AD FS einleiten eine Abmeldung auf der Clientseite registriert LogoutUri gesendet werden.

## <a name="faqs"></a>Häufig gestellte Fragen
**Q:** Ich sehe keine der Frontchannel_logout_supported und Frontchannel_logout_session_supported Parameter in der Discovery-Dokument.</br>
**A:** Stellen Sie sicher, dass man [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801) auf allen AD FS-Servern installiert. Finden Sie in der einmaligen Abmeldung in Server 2016 mit [KB4038801](https://support.microsoft.com/en-gb/help/4038801/windows-10-update-kb4038801).

**Q:** Ich habe die einmalige Abmeldung konfiguriert, wie angegeben, aber Benutzer bleibt angemeldet zu anderen Clients.</br>
**A:** Sicherstellen, dass `LogoutUri` festgelegt, wird er für alle Clients, in denen der Benutzer angemeldet. Außerdem erfolgt bei AD FS einen Best-Case beim Senden der Anforderung zur Abmeldung und auf dem registrierten `LogoutUri`. Client muss die Logik zum Verarbeiten der Anforderungs und Maßnahmen zur Abmeldung des Benutzers von Anwendung implementieren.</br>

**Q:** Ausstellen AD FS werden ein Zugriffstoken, wenn nach der Abmeldung einen der Clients zurück an AD FS mit einem gültigen Aktualisierungstoken wechselt?</br>
**A:** Ja. Es liegt in der Verantwortung der Clientanwendung, um allen authentifizierten Artefakte löschen, nachdem eine Anforderung zur Abmelde empfangen wurde an die registrierten `LogoutUri`.


## <a name="next-steps"></a>Nächste Schritte
[AD FS-Entwicklung](../../ad-fs/AD-FS-Development.md)  
