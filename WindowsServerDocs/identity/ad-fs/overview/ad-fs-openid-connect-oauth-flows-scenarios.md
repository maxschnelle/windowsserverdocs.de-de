---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS OpenID Connect-/OAuth-Flows und Anwendungsszenarien
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 05ee7a1e5e36ee7bc2ffcb41fbdabf4b5b6c2c4e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966827"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>AD FS OpenID Connect-/OAuth-Flows und Anwendungsszenarien
Gilt für Active Directory-Verbunddienste (AD FS) 2016 und höher


|Szenario|Exemplarische Vorgehensweise bei Szenarien mit Beispielen|OAuth 2.0 Flow/Gewährung|Clienttyp|
|-----|-----|-----|-----|
|Single-Page-App (SPA)</br> | &bull; [Beispiel mit ADAL](../development/Single-Page-Application-with-AD-FS.md)|[Implizit](#implicit-grant-flow)|Öffentlich|
|Web-App, die Benutzer anmeldet</br> | &bull; [Beispiel mit OWIN](../development/enabling-openid-connect-with-ad-fs.md)|[Autorisierungscode](#authorization-code-grant-flow)|Öffentlich, Vertraulich|
|Native App ruft Web-API auf</br>|&bull; [Beispiel mit MSAL](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull; [Beispiel mit ADAL](../development/native-client-with-ad-fs.md)|[Autorisierungscode](#authorization-code-grant-flow)|Öffentlich|
|Web-App ruft Web-API auf</br>|&bull; [Beispiel mit MSAL](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull; [Beispiel mit ADAL](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[Autorisierungscode](#authorization-code-grant-flow)|Vertraulich|
|Web-API ruft eine andere Web-API im Auftrag des (OBO) Benutzers auf</br>|&bull; [Beispiel mit MSAL](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull; [Beispiel mit ADAL](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[On-behalf-of](#on-behalf-of-flow)|Web-App agiert vertraulich|
|Daemon-App ruft Web-API auf||[Clientanmeldeinformationen](#client-credentials-grant-flow)|Vertraulich|
|Web-App ruft Web-API mit Benutzeranmeldeinformationen auf||[Kennwortanmeldeinformationen des Ressourcenbesitzers](#resource-owner-password-credentials-grant-flow-not-recommended)|Öffentlich, Vertraulich|
|Browserfreie App ruft Web-API auf||[Gerätecode](#device-code-flow)|Öffentlich, Vertraulich|

## <a name="implicit-grant-flow"></a>Impliziter Gewährungsflow

Für Single-Page-Apps (AngularJS, Ember.js, React.js usw.) unterstützt AD FS den impliziten OAuth 2.0-Gewährungsflow. Der implizite Flow ist in der  [OAuth 2.0-Spezifikation](https://tools.ietf.org/html/rfc6749#section-4.2) beschrieben. Sein Hauptvorteil besteht darin, dass die App entsprechende Token von AD FS abrufen kann, ohne dass ein Austausch von Anmeldeinformationen auf dem Back-End-Server durchgeführt werden muss. Dies ermöglicht es der App, den Benutzer anzumelden, die Sitzung aufrechtzuerhalten und Token für andere Web-APIs abzurufen, und dies alles innerhalb des JavaScript-Clientcodes. Es gibt einige wichtige Sicherheitsaspekte, die bei der Verwendung des impliziten Flows speziell bei  [Clients](https://tools.ietf.org/html/rfc6749#section-10.3) zu berücksichtigen sind.

Wenn du den impliziten Flow und AD FS verwenden möchtest, um deiner JavaScript-App die Authentifizierung hinzuzufügen, folge den nachfolgenden allgemeinen Schritten.

### <a name="protocol-diagram"></a>Protokolldiagramm

Das folgende Diagramm zeigt den gesamten impliziten Anmeldeflow, und die einzelnen Schritte werden in den folgenden Abschnitten ausführlicher beschrieben.

![Implizite Anmeldung](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>Anfordern von ID-Token und Zugriffstoken

Um den Benutzer zunächst in deiner App anzumelden, kannst du eine OpenID Connect-Authentifizierungsanforderung senden und ID-Token und Zugriffstoken vom AD FS-Endpunkt abrufen.

```
// Line breaks for legibility only

https://adfs.contoso.com/adfs/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid
&response_mode=fragment
&state=12345
```


|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|response_type|Erforderlich|Muss `id_token` für die OpenID Connect-Anmeldung enthalten. Sie kann auch den response_type `token` enthalten. Wenn du hier ein Token verwendest, kann deine App sofort ein Zugriffstoken vom Autorisierungsendpunkt erhalten, ohne eine zweite Anforderung an den Tokenendpunkt stellen zu müssen.|
|redirect_uri|Erforderlich|Der redirect_uri (Umleitungs-URI) deiner App, wohin Authentifizierungsantworten gesendet und von deiner App empfangen werden können. Er muss genau mit einem der Umleitungs-URIs übereinstimmen, die du in AD FS konfiguriert hast.|
|nonce|Erforderlich|Ein in der Anforderung enthaltener, von der App generierter Wert, der in das resultierende id_token als Anspruch einbezogen wird. Die App kann diesen Wert dann verifizieren, um Tokenwiederholungsangriffe abzuwehren. Der Wert ist in der Regel eine zufällige, eindeutige Zeichenfolge, die zur Identifizierung des Ursprungs der Anforderung verwendet werden kann. Nur erforderlich, wenn ein id_token angefordert wird.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen. Für OpenID Connect muss der Bereich `openid` enthalten sein.|
|resource|Optional|Die URL deiner Web-API.</br>Hinweis: Wenn die MSAL-Clientbibliothek verwendet wird, werden keine Ressourcenparameter gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichsparameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource hier oder im Bereich nicht übergeben wird, verwendet AD FS eine Standardressource: urn:microsoft:userinfo. Ressourcenrichtlinien für Benutzerinformationen wie MFA, Ausstellungs- oder Autorisierungsrichtlinien können nicht angepasst werden.|
|response_mode|Optional| Gibt die Methode an, die verwendet werden soll, um das resultierende Token an deine App zurückzusenden. Dies ist standardmäßig `fragment`.|
|state|Optional|Ein in der Anforderung enthaltener Wert, der auch in der Tokenantwort zurückgegeben wird. Es kann eine Zeichenfolge mit beliebigen gewünschten Inhalten sein. Ein zufällig generierter eindeutiger Wert wird in der Regel zur Verhinderung von CSRF-Angriffen (Cross-Site Request Forgery) verwendet. Der Status wird auch verwendet, um Informationen über den Zustand des Benutzers in der App vor der Authentifizierungsanforderung zu verschlüsseln, z. B. die Seite oder die Ansicht, auf der bzw. in der sie sich befunden haben.|
|prompt|Optional|Gibt den Typ der Benutzerinteraktion an, der erforderlich ist. Derzeit sind die einzigen zulässigen Werte „login“ und „none“.</br>- `prompt=login` zwingt den Benutzer, seine Anmeldeinformationen für diese Anforderung einzugeben und das einmalige Anmelden zu negieren. </br>- `prompt=none` stellt das Gegenteil dar. Es stellt sicher, dass dem Benutzer keinerlei interaktive Eingabeaufforderung präsentiert wird. Wenn die Anforderung nicht im Hintergrund über das einmalige Anmelden abgeschlossen werden kann, gibt AD FS einen interaction_required-Fehler zurück.|
|login_hint|Optional|Kann verwendet werden, um das Feld für Benutzername/E-Mail-Adresse der Anmeldeseite für den Benutzer vorab auszufüllen, wenn du seinen Benutzernamen vorab kennst. Häufig verwenden Apps diesen Parameter bei der erneuten Authentifizierung, nachdem sie den Benutzernamen bereits aus einer früheren Anmeldung mit dem `upn` -Anspruch aus `id_token` extrahiert haben.|
|domain_hint|Optional|Wenn es enthalten ist, überspringt es den domänenbasierten Ermittlungsprozess, den der Benutzer auf der Anmeldeseite durchläuft, was zu einer erhöhten Benutzerfreundlichkeit führt.|

An diesem Punkt wird der Benutzer aufgefordert, seine Anmeldeinformationen einzugeben und die Authentifizierung abzuschließen. Sobald sich der Benutzer authentifiziert hat, gibt der AD FS-Autorisierungsendpunkt eine Antwort an deine App am angegebenen redirect_uri (Umleitungs-URI) zurück, wobei die im Parameter „response_mode“ angegebene Methode verwendet wird.

### <a name="successful-response"></a>Erfolgreiche Antwort

Eine erfolgreiche Antwort unter Verwendung von `response_mode=fragment and response_type=id_token+token` sieht wie die folgende aus.

```
// Line breaks for legibility only

GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZEstZnl0aEV...
&token_type=Bearer
&expires_in=3599
&scope=openid
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZstZnl0aEV1Q...
&state=12345
```


|Parameter|Beschreibung|
|-----|-----|
|access_token|Enthalten, wenn response_type `token` enthält.|
|token_type|Enthalten, wenn response_type `token` enthält. Wird immer „Bearer“ sein.|
|expires_in| Enthalten, wenn response_type `token` enthält. Gibt die Anzahl der Sekunden an, in denen das Token für die Zwischenspeicherung gültig ist.|
|scope| Gibt die Bereiche an, für die das access_token gültig ist.|
|id_token|Enthalten, wenn response_type `id_token` enthält. Ein signiertes JSON-Webtoken (JWT). Die App kann die Segmente dieses Tokens entschlüsseln, um Informationen über den Benutzer, der sich angemeldet hat, anzufordern. Die App kann die Werte zwischenspeichern und anzeigen, aber sie sollte sich nicht auf sie verlassen, wenn es um Autorisierung oder Sicherheitsbegrenzungen geht.|
|state|Wenn ein state-Parameter in der Anforderung enthalten ist, sollte derselbe Wert in der Antwort angezeigt werden. Die App sollte bestätigen, dass die state-Werte in der Anforderung und der Antwort identisch sind.|

### <a name="refresh-tokens"></a>Aktualisierungstoken
Die implizite Gewährung stellt keine Aktualisierungstoken bereit. Sowohl `id_tokens` als auch `access_tokens` laufen nach kurzer Zeit ab, sodass deine App darauf vorbereitet sein muss, diese Token regelmäßig zu aktualisieren. Um beide Arten von Token zu aktualisieren, kannst du dieselbe versteckte iframe-Anforderung von oben ausführen, indem du den Parameter `prompt=none`  verwendest, um das Verhalten der Identitätsplattform zu steuern. Wenn du ein `new id_token` erhalten möchtest, dann verwende unbedingt `response_type=id_token`.

## <a name="authorization-code-grant-flow"></a>Gewährungsflow für Autorisierungscodes

Die OAuth 2. 0-Autorisierungscodegewährung kann in Web-Apps verwendet werden, um Zugriff auf geschützte Ressourcen wie Web-APIs zu erhalten. Der OAuth 2.0-Autorisierungscodeflow ist in [Abschnitt 4.1 der OAuth 2.0-Spezifikation](https://tools.ietf.org/html/rfc6749) beschrieben. Er wird zur Authentifizierung und Autorisierung in den meisten App-Typen verwendet, einschließlich Web-Apps und nativ installierter Apps. Der Flow ermöglicht Apps das sichere Abrufen von access_token, die für den Zugriff auf Ressourcen verwendet werden können, die dem AD FS vertrauen.

### <a name="protocol-diagram"></a>Protokolldiagramm

Allgemein sieht der Authentifizierungsflow für eine native Anwendung ein wenig wie folgt aus:

![Gewährungsflow für Autorisierungscodes](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>Anfordern eines Autorisierungscodes

Der Autorisierungscodeflow beginnt damit, dass der Client den Benutzer zum Endpunkt „/authorize“ leitet. In dieser Anforderung gibt der Client die Berechtigungen an, die er vom Benutzer abrufen muss:

```
// Line breaks for legibility only

https://adfs.contoso.com/adfs/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https://webapi.com/
&scope=openid
&state=12345
```

|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|response_type|Erforderlich| Muss den Code für den Autorisierungscodeflow enthalten.|
|redirect_uri|Erforderlich|Der `redirect_uri` deiner App, wohin Authentifizierungsantworten gesendet und von deiner App empfangen werden können. Er muss genau mit einem der Umleitungs-URIs übereinstimmen, die du im AD FS für den Client registriert hast.|
|resource|Optional|Die URL deiner Web-API.</br>Hinweis: Wenn die MSAL-Clientbibliothek verwendet wird, werden keine Ressourcenparameter gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichsparameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource hier oder im Bereich nicht übergeben wird, verwendet AD FS eine Standardressource: urn:microsoft:userinfo. Ressourcenrichtlinien für Benutzerinformationen wie MFA, Ausstellungs- oder Autorisierungsrichtlinien können nicht angepasst werden.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|
|response_mode|Optional|Gibt die Methode an, die verwendet werden soll, um das resultierende Token an deine App zurückzusenden. Kann eines der folgenden Elemente sein: </br>- query </br>- fragment </br>- form_post</br>`query` stellt den Code als Abfragezeichenfolgenparameter für deinen Umleitungs-URI zur Verfügung. Wenn du den Code anforderst, kannst du query, fragment oder form_post verwenden. `form_post` führt einen POST-Vorgang aus, der den Code an deinen Umleitungs-URI enthält.|
|state|Optional|Ein in der Anforderung enthaltener Wert, der auch in der Tokenantwort zurückgegeben wird. Es kann eine Zeichenfolge mit beliebigen gewünschten Inhalten sein. Ein zufällig generierter eindeutiger Wert wird in der Regel zur Verhinderung von CSRF-Angriffen (Cross-Site Request Forgery) verwendet. Der Wert kann auch Informationen über den Zustand des Benutzers in der App vor der Authentifizierungsanforderung verschlüsseln, z. B. die Seite oder die Ansicht, auf der bzw. in der sie sich befunden haben.|
|prompt|Optional|Gibt den Typ der Benutzerinteraktion an, der erforderlich ist. Derzeit sind die einzigen zulässigen Werte „login“ und „none“.</br>- `prompt=login` zwingt den Benutzer, seine Anmeldeinformationen für diese Anforderung einzugeben und das einmalige Anmelden zu negieren. </br>- `prompt=none` stellt das Gegenteil dar. Es stellt sicher, dass dem Benutzer keinerlei interaktive Eingabeaufforderung präsentiert wird. Wenn die Anforderung nicht im Hintergrund über das einmalige Anmelden abgeschlossen werden kann, gibt AD FS einen interaction_required-Fehler zurück.|
|login_hint|Optional|Kann verwendet werden, um das Feld für Benutzername/E-Mail-Adresse der Anmeldeseite für den Benutzer vorab auszufüllen, wenn du seinen Benutzernamen vorab kennst. Häufig verwenden Apps diesen Parameter bei der erneuten Authentifizierung, nachdem sie den Benutzernamen bereits aus einer früheren Anmeldung mit dem `upn`-Anspruch aus `id_token` extrahiert haben.|
|domain_hint|Optional|Wenn es enthalten ist, überspringt es den domänenbasierten Ermittlungsprozess, den der Benutzer auf der Anmeldeseite durchläuft, was zu einer erhöhten Benutzerfreundlichkeit führt.|
|code_challenge_method|Optional|Die zum Verschlüsseln von code_verifier für den code_challenge-Parameter verwendete Methode. Folgenden Werte sind möglich: </br>- plain </br>- S256 </br>Wenn ausgeschlossen, wird code_challenge als Klartext angenommen, wenn `code_challenge`  enthalten ist. AD FS unterstützt sowohl „plain“ als auch „S256“. Weitere Informationen findest du unter [PKCE RFC](https://tools.ietf.org/html/rfc7636).|
|code_challenge|Optional| Dient zur Sicherung von Autorisierungscodegewährungen über Proof Key for Code Exchange (PKCE) von einem nativen Client. Erforderlich, wenn `code_challenge_method` enthalten ist. Weitere Informationen findest du unter [PKCE RFC](https://tools.ietf.org/html/rfc7636).|

An diesem Punkt wird der Benutzer aufgefordert, seine Anmeldeinformationen einzugeben und die Authentifizierung abzuschließen. Sobald sich der Benutzer authentifiziert hat, gibt der AD FS eine Antwort an deine App am angegebenen `redirect_uri` zurück, wobei die im Parameter `response_mode` angegebene Methode verwendet wird.

### <a name="successful-response"></a>Erfolgreiche Antwort

Eine erfolgreiche Antwort mit „response_mode=query“ sieht wie folgt aus:

```
GET https://adfs.contoso.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```


|Parameter|Beschreibung|
|-----|-----|
|code|Der von der App angeforderte `authorization_code`. Die App kann mithilfe des Autorisierungscodes ein Zugriffstoken für die Zielressource anfordern. Authorization_codes sind kurzlebig, in der Regel laufen sie nach etwa 10 Minuten ab.|
|state|Wenn ein `state`-Parameter in der Anforderung enthalten ist, sollte derselbe Wert in der Antwort angezeigt werden. Die App sollte bestätigen, dass die state-Werte in der Anforderung und der Antwort identisch sind.|

### <a name="request-an-access-token"></a>Anfordern eines Zugriffstokens

Nachdem du nun einen `authorization_code` abgerufen und die Berechtigung des Benutzers erhalten hast, kannst du den Code für einen `access_token` bei der gewünschten Ressource einlösen. Dazu sendest du eine POST-Anforderung an den „/token“-Endpunkt:

```
// Line breaks for legibility only

POST /adfs/oauth2/token HTTP/1.1
Host: https://adfs.contoso.com/
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for confidential clients (web apps)
```

|Parameter|Erforderlich/Optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|grant_type|Erforderlich|Muss `authorization_code` für den Autorisierungscodeflow sein.|
|code|Erforderlich|Der `authorization_code`, den du im ersten Abschnitt des Flows abgerufen hast.|
|redirect_uri|Erforderlich|Derselbe `redirect_uri`-Wert, der zum Abrufen des `authorization_code` verwendet wurde.|
|client_secret|Erforderlich für Web-Apps|Das Anwendungsgeheimnis, das du während der Registrierung der App im AD FS erstellt hast. Du solltest das Anwendungsgeheimnis nicht in einer nativen App verwenden, da client_secrets nicht zuverlässig auf Geräten gespeichert werden können. Es wird für Web-Apps und Web-APIs benötigt, die in der Lage sind, das client_secret sicher auf der Serverseite zu speichern. Der geheime Clientschlüssel muss vor dem Senden mit einer URL codiert werden. Diese Apps können auch eine schlüsselbasierte Authentifizierung verwenden, indem sie ein JWT signieren und dies als client_assertion-Parameter hinzufügen.|
|code_verifier|Optional|Derselbe `code_verifier`, der zum Erhalten des authorisation_code verwendet wurde. Erforderlich, wenn PKCE in der Anforderung zur Gewährung des Autorisierungscodes verwendet wurde. Weitere Informationen findest du unter [PKCE RFC](https://tools.ietf.org/html/rfc7636).</br>Hinweis: Gilt für Active Directory-Verbunddienste (AD FS) 2019 und höher|

### <a name="successful-response"></a>Erfolgreiche Antwort

Eine erfolgreiche Tokenantwort wird wie folgt aussehen:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "refresh_token_expires_in": 28800,
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```


|Parameter|Beschreibung|
|-----|-----|
|access_token|Das angeforderte Zugriffstoken. Die App kann dieses Token für die Authentifizierung mit der gesicherten Ressource (Web-API) verwenden.|
|token_type|Gibt den Wert des Tokentyps an. Der einzige von AD FS unterstützte Typ ist „Bearer“.
|expires_in|Die Gültigkeitsdauer des Zugriffstokens (in Sekunden).
|refresh_token|Ein OAuth 2.0-Aktualisierungstoken. Die App kann dieses Token verwenden, um weitere Zugriffstoken abzurufen, nachdem das aktuelle Zugriffstoken abgelaufen ist. Refresh_token sind langlebig und können verwendet werden, um den Zugriff auf Ressourcen über längere Zeiträume zu erhalten.|
|refresh_token_expires_in|Die Gültigkeitsdauer des Aktualisierungstokens (in Sekunden).|
|id_token|Ein JSON-Webtoken (JWT). Die App kann die Segmente dieses Tokens entschlüsseln, um Informationen über den Benutzer, der sich angemeldet hat, anzufordern. Die App kann die Werte zwischenspeichern und anzeigen, aber sie sollte sich nicht auf sie verlassen, wenn es um Autorisierung oder Sicherheitsbegrenzungen geht.|

### <a name="use-the-access-token"></a>Verwenden des Zugriffstokens

```
GET /v1.0/me/messages
Host: https://webapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
 ```

### <a name="refresh-token-grant-flow"></a>Gewährungsflow für Aktualisierungstoken
 
Access_token sind kurzlebig und sie müssen nach Ablauf der Gültigkeitsdauer aktualisiert werden, um weiterhin auf Ressourcen zugreifen zu können. Du kannst dazu eine weitere POST-Anforderung an den `/token` -Endpunkt übermitteln, wobei dieses Mal das refresh_token anstelle des Codes bereitgestellt wird. Aktualisierungstoken sind für alle Berechtigungen gültig, für die dein Client bereits ein Zugriffstoken erhalten hat.

Aktualisierungstoken haben keine festgelegte Lebensdauer. Die Lebensdauer von Aktualisierungstoken ist in der Regel relativ lang. In einigen Fällen laufen die Aktualisierungstoken jedoch ab, werden widerrufen oder es fehlen ausreichende Berechtigungen für die gewünschte Aktion. Die Anwendung muss Fehler, die vom Tokenausstellungsendpunkt zurückgegeben werden, erwarten und ordnungsgemäß behandeln.

Obwohl Aktualisierungstoken nicht widerrufen werden, wenn sie zum Abrufen neuer Zugriffstoken verwendet werden, wird von dir erwartet, dass du das alte Aktualisierungstoken verwirfst. Die OAuth 2.0-Spezifikation besagt Folgendes: „Der Autorisierungsserver KANN ein neues Aktualisierungstoken ausgeben. In diesem Fall MUSS der Client das alte Aktualisierungstoken verwerfen und durch das neue Aktualisierungstoken ersetzen. Der Autorisierungsserver KANN das alte Aktualisierungstoken zurücknehmen, nachdem er ein neues Aktualisierungstoken an den Client ausgegeben hat.“ AD FS gibt das Aktualisierungstoken aus, wenn die Lebensdauer des neuen Aktualisierungstokens länger als die des vorherigen Aktualisierungstokens ist.  Weitere Informationen zur Lebensdauer von Aktualisierungstoken in AD FS findest du unter [AD FS: Einstellungen für einmaliges Anmelden](../operations/ad-fs-single-sign-on-settings.md).

```
// Line breaks for legibility only

POST /adfs/oauth2/token HTTP/1.1
Host: https://adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for confidential clients (web apps)
```


|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|grant_type|Erforderlich|Muss `refresh_token` für diesen Teil des Autorisierungscodeflows sein.|
|resource|Optional|Die URL deiner Web-API.</br>Hinweis: Wenn die MSAL-Clientbibliothek verwendet wird, werden keine Ressourcenparameter gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichsparameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource hier oder im Bereich nicht übergeben wird, verwendet AD FS eine Standardressource: urn:microsoft:userinfo. Ressourcenrichtlinien für Benutzerinformationen wie MFA, Ausstellungs- oder Autorisierungsrichtlinien können nicht angepasst werden.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|
|refresh_token|Erforderlich|Das refresh_token, das du im zweiten Abschnitt des Flows abgerufen hast.|
|client_secret|Erforderlich für Web-Apps| Das Anwendungsgeheimnis, das du im App-Registrierungsportal für deine App erstellt hast. Es sollte nicht in einer nativen App verwendet werden, da client_secrets nicht zuverlässig auf Geräten gespeichert werden können. Es wird für Web-Apps und Web-APIs benötigt, die in der Lage sind, das client_secret sicher auf der Serverseite zu speichern. Diese Apps können auch eine schlüsselbasierte Authentifizierung verwenden, indem sie ein JWT signieren und dies als client_assertion-Parameter hinzufügen.|

### <a name="successful-response"></a>Erfolgreiche Antwort
Eine erfolgreiche Tokenantwort wird wie folgt aussehen:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "refresh_token_expires_in": 28800,
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
|Parameter|Beschreibung|
|-----|-----|
|access_token|Das angeforderte Zugriffstoken. Die App kann dieses Token für die Authentifizierung mit der gesicherten Ressource (z. B. einer Web-API) verwenden.|
|token_type|Gibt den Wert des Tokentyps an. Der einzige von AD FS unterstützte Typ ist „Bearer“.|
|expires_in|Die Gültigkeitsdauer des Zugriffstokens (in Sekunden).|
|scope|Die Bereiche, für die das access_token gültig ist.|
|refresh_token|Ein OAuth 2.0-Aktualisierungstoken. Die App kann dieses Token verwenden, um weitere Zugriffstoken abzurufen, nachdem das aktuelle Zugriffstoken abgelaufen ist. Refresh_token sind langlebig und können verwendet werden, um den Zugriff auf Ressourcen über längere Zeiträume zu erhalten.|
|refresh_token_expires_in|Die Gültigkeitsdauer des Aktualisierungstokens (in Sekunden).|
|id_token|Ein JSON-Webtoken (JWT). Die App kann die Segmente dieses Tokens entschlüsseln, um Informationen über den Benutzer, der sich angemeldet hat, anzufordern. Die App kann die Werte zwischenspeichern und anzeigen, aber sie sollte sich nicht auf sie verlassen, wenn es um Autorisierung oder Sicherheitsbegrenzungen geht.|

## <a name="on-behalf-of-flow"></a>On-Behalf-Of-Flow

Der OAuth 2.0 On-Behalf-Of-Flow (OBO) dient dem Anwendungsfall, dass eine Anwendung eine Dienst-/Web-API aufruft, die wiederum eine andere Dienst-/Web-API aufrufen muss. Die Idee besteht darin, die delegierte Benutzeridentität und die Berechtigungen durch die Anforderungskette zu verteilen. Damit der Dienst der mittleren Ebene authentifizierte Anforderungen an den Downstreamdienst stellen kann, muss er im Auftrag des Benutzers ein Zugriffstoken vom AD FS sichern.

### <a name="protocol-diagram"></a>Protokolldiagramm
Nehmen wir an, dass der Benutzer bei einer Anwendung mit dem oben beschriebenen Gewährungsflow für den OAuth 2.0-Autorisierungscode authentifiziert wurde. An diesem Punkt verfügt die Anwendung über ein Zugriffstoken für API A (Token A) mit den Ansprüchen und der Zustimmung des Benutzers zum Zugriff auf die Web-API der mittleren Ebene (API A). Stelle sicher, dass der Client im Token den Bereich „user_impersonation“ anfordert. Jetzt muss API A eine authentifizierte Anforderung an die Downstream-Web-API (API B) stellen.

Die folgenden Schritte bilden den OBO-Flow und werden mithilfe des folgenden Diagramms erläutert.

![On-Behalf-Of-Flow](media/adfs-scenarios-for-developers/obo.png)

  1. Die Clientanwendung stellt eine Anforderung an API A mit Token A. Hinweis: Stelle bei der Konfiguration des OBO-Flows im AD FS sicher, dass in der Anforderung der Bereich `user_impersonation` ausgewählt ist und der Client den Bereich `user_impersonation` anfordert.
  2. API A authentifiziert sich gegenüber dem AD FS-Tokenausstellungsendpunkt und fordert ein Token für den Zugriff auf API B an: Stelle bei der Konfiguration dieses Flows im AD FS sicher, dass API A auch als Serveranwendung registriert wird, wobei „clientID“ denselben Wert hat wie die Ressourcen-ID in API A.
  3. Der AD FS-Tokenausstellungsendpunkt überprüft die Anmeldeinformationen von API A mit Token A und stellt das Zugriffstoken für API B (Token B) aus.
  4. Token B wird im Autorisierungsheader der Anforderung für API B festgelegt.
  5. Daten von der gesicherten Ressource werden von API B zurückgegeben.

### <a name="service-to-service-access-token-request"></a>Anforderung von Zugriffstoken zwischen Diensten

Um ein Zugriffstoken anzufordern, führe einen HTTP POST-Vorgang an den AD FS-Tokenendpunkt mit den folgenden Parametern aus.


### <a name="first-case-access-token-request-with-a-shared-secret"></a>Erster Fall: Anforderung eines Zugriffstokens mit einem gemeinsamen Geheimnis

Bei Verwendung eines gemeinsamen Geheimnisses enthält eine Dienst-zu-Dienst-Zugriffstokenanforderung die folgenden Parameter:


|Parameter|Erforderlich/Optional|BESCHREIBUNG|
|-----|-----|-----|
|grant_type|Erforderlich|Der Typ der Tokenanforderung. Bei einer Anforderung mit einem JWT muss der Wert „urn:ietf:params:oauth:grant-type:jwt-bearer“ sein.|
|client_id|Erforderlich|Die Client-ID, die du bei der Registrierung deiner ersten Web-API als Server-App (App auf mittlerer Ebene) konfigurierst. Diese sollte dieselbe sein wie die Ressourcen-ID, die im ersten Abschnitt verwendet wird, d. h. die URL der ersten Web-API.|
|client_secret|Erforderlich|Das Anwendungsgeheimnis, das du während der Registrierung der Server-App im AD FS erstellt hast.|
|assertion|Erforderlich|Der Wert des in der Anforderung verwendeten Tokens.|
|requested_token_use|Erforderlich|Gibt an, wie die Anforderung verarbeitet werden soll. Im OBO-Flow muss der Wert auf „on_behalf_of“ festgelegt werden.|
|resource|Erforderlich|Die Ressourcen-ID, die bei der Registrierung der ersten Web-API als Server-App (App auf mittlerer Ebene) bereitgestellt wurde. Die Ressourcen-ID sollte die URL der zweiten Web-API der App auf mittlerer Ebene sein, die im Auftrag des Clients aufgerufen wird.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen für die Tokenanforderung.|

#### <a name="example"></a>Beispiel

Der folgende `HTTP POST` fordert ein Zugriffstoken und ein Aktualisierungstoken an.

```
//line breaks for legibility only

POST /adfs/oauth2/token HTTP/1.1
Host: adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer
&client_id=https://webapi.com/
&client_secret=BYyVnAt56JpLwUcyo47XODd
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIm…
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope=openid
```

### <a name="second-case-access-token-request-with-a-certificate"></a>Zweiter Fall: Anforderung eines Zugriffstokens mit einem Zertifikat

Eine Dienst-zu-Dienst-Zugriffstokenanforderung mit einem Zertifikat enthält die folgenden Parameter:


|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----|
|grant_type|Erforderlich|Der Typ der Tokenanforderung. Bei einer Anforderung mit einem JWT muss der Wert „urn:ietf:params:oauth:grant-type:jwt-bearer“ sein. |
|client_id|Erforderlich|Die Client-ID, die du bei der Registrierung deiner ersten Web-API als Server-App (App auf mittlerer Ebene) konfigurierst. Diese sollte dieselbe sein wie die Ressourcen-ID, die im ersten Abschnitt verwendet wird, d. h. die URL der ersten Web-API.|
|client_assertion_type|Erforderlich|Der Wert muss „urn:ietf:params:oauth:client-assertion-type:jwt-bearer“ sein.|
|client_assertion|Erforderlich|Eine Assertion (ein JSON-Webtoken), die du mit dem Zertifikat, das als Berechtigungsnachweis für deine Anwendung registriert wurde, erstellen und signieren musst.|
|assertion|Erforderlich|Der Wert des in der Anforderung verwendeten Tokens.|
|requested_token_use|Erforderlich|Gibt an, wie die Anforderung verarbeitet werden soll. Im OBO-Flow muss der Wert auf „on_behalf_of“ festgelegt werden.|
|resource|Erforderlich|Die Ressourcen-ID, die bei der Registrierung der ersten Web-API als Server-App (App auf mittlerer Ebene) bereitgestellt wurde. Die Ressourcen-ID sollte die URL der zweiten Web-API der App auf mittlerer Ebene sein, die im Auftrag des Clients aufgerufen wird.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen für die Tokenanforderung.|


Es ist zu beachten, dass die Parameter fast dieselben sind wie im Fall der Anforderung durch gemeinsames Geheimnis, außer dass der Parameter „client_secret“ durch zwei Parameter ersetzt wird: „client_assertion_type“ und „client_assertion“.

#### <a name="example"></a>Beispiel
Der folgende HTTP POST-Vorgang fordert ein Zugriffstoken für die Web-API mit einem Zertifikat an.

```
// line breaks for legibility only

POST /adfs/oauth2/token HTTP/1.1
Host: https://adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id= https://webapi.com/
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNS…
&resource=https://secondwebapi.com/
&requested_token_use=on_behalf_of
&scope= openid
```

### <a name="service-to-service-access-token-response"></a>Zugriffstokenantwort zwischen Diensten

Eine erfolgreiche Antwort enthält eine JSON OAuth 2.0-Antwort mit den folgenden Parametern.


|Parameter|BESCHREIBUNG|
|-----|-----|
|token_type|Gibt den Wert des Tokentyps an. Der einzige von AD FS unterstützte Typ ist „Bearer“. |
|scope|Der durch das Token gewährte Zugriffsbereich.|
|expires_in|Die Zeitspanne in Sekunden, in der das Zugriffstoken gültig ist.|
|access_token|Das angeforderte Zugriffstoken. Der aufrufende Dienst kann dieses Token verwenden, um die Authentifizierung für den empfangenden Dienst durchzuführen.|
|id_token|Ein JSON-Webtoken (JWT). Die App kann die Segmente dieses Tokens entschlüsseln, um Informationen über den Benutzer, der sich angemeldet hat, anzufordern. Die App kann die Werte zwischenspeichern und anzeigen, aber sie sollte sich nicht auf sie verlassen, wenn es um Autorisierung oder Sicherheitsbegrenzungen geht.|
|refresh_token|Das Aktualisierungstoken für das angeforderte Zugriffstoken. Der aufrufende Dienst kann dieses Token verwenden, um nach Ablauf des aktuellen Zugriffstokens ein weiteres Zugriffstoken anzufordern.|
|Refresh_token_expires_in|Die Zeitspanne in Sekunden, in der das Aktualisierungstoken gültig ist.

### <a name="success-response-example"></a>Beispiel für eine Erfolgsantwort

Das folgende Beispiel zeigt eine Erfolgsantwort auf eine Anforderung nach einem Zugriffstoken für die Web-API.

```
{
  "token_type": "Bearer",
  "scope": openid,
  "expires_in": 3269,
  "access_token": "eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1t"
  "id_token": "aWRfdG9rZW49ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKU1V6STFOa"
  "refresh_token": "OAQABAAAAAABnfiG…"
  "refresh_token_expires_in": 28800,
}
```


Verwende das Zugriffstoken, um auf die gesicherte Ressource zuzugreifen. Jetzt kann der Dienst auf mittlerer Ebene das oben abgerufene Token verwenden, um authentifizierte Anforderungen an die Downstream-Web-API zu stellen, indem das Token im Autorisierungsheader festgelegt wird.

#### <a name="example"></a>Beispiel
```
GET /v1.0/me HTTP/1.1
Host: https://secondwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ…
```

## <a name="client-credentials-grant-flow"></a>Gewährungsflow für Clientanmeldeinformationen

Du kannst die in [RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4) angegebene Gewährung der OAuth 2.0-Clientanmeldeinformationen verwenden, um unter Verwendung der Identität einer Anwendung auf im Web gehostete Ressourcen zuzugreifen. Diese Art von Gewährung wird häufig für Interaktionen zwischen Servern verwendet, die ohne unmittelbare Interaktion mit einem Benutzer im Hintergrund ausgeführt werden müssen. Diese Anwendungstypen werden oft als Daemon oder Dienstkonten bezeichnet.

Über den Gewährungsflow für OAuth 2.0-Clientanmeldeinformationen können Webdienste (d. h. vertrauenswürdige Clients) ihre eigenen Anmeldeinformationen für die Authentifizierung beim Aufrufen anderer Webdienste verwenden, anstatt die Identität eines Benutzers anzunehmen. In diesem Szenario ist der Client normalerweise ein Webdienst der mittleren Ebene, ein Daemondienst oder eine Website. Für ein höheres Maß an Sicherheit erlaubt der AD FS dem aufrufenden Dienst auch die Verwendung eines Zertifikats (anstelle eines gemeinsamen Geheimnisses) als Anmeldeinformation.

### <a name="protocol-diagram"></a>Protokolldiagramm

Das folgende Diagramm zeigt den Gewährungsflow für Clientanmeldeinformationen.

![Clientanmeldeinformationen](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>Anfordern eines Tokens

Sende eine `POST`-Anforderung an den AD FS-Endpunkt „/token“, um ein Token unter Verwendung der Clientanmeldeinformationen abzurufen:

### <a name="first-case-access-token-request-with-a-shared-secret"></a>Erster Fall: Anforderung eines Zugriffstokens mit einem gemeinsamen Geheimnis

```
POST /adfs/oauth2/token HTTP/1.1
//Line breaks for clarity

Host: https://adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865
&client_secret=qWgdYAmab0YSkuL1qKv5bPX
&grant_type=client_credentials
```

|Parameter|Erforderlich/Optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen, denen der Benutzer zustimmen soll.|
|client_secret|Erforderlich|Der geheime Clientschlüssel, den du für deine App im App-Registrierungsportal generiert hast. Der geheime Clientschlüssel muss vor dem Senden mit einer URL codiert werden.|
|grant_type|Erforderlich|Muss auf `client_credentials` festgelegt werden.|

### <a name="second-case-access-token-request-with-a-certificate"></a>Zweiter Fall: Anforderung eines Zugriffstokens mit einem Zertifikat

```
POST /adfs/oauth2/token HTTP/1.1

// Line breaks for clarity

Host: https://adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&grant_type=client_credentials
```

|Parameter|Erforderlich/Optional|Beschreibung|
|-----|-----|-----|
|client_assertion_type|Erforderlich|Der Wert muss auf „urn:ietf:params:oauth:client-assertion-type:jwt-bearer“ festgelegt sein.|
|client_assertion|Erforderlich|Eine Assertion (ein JSON-Webtoken), die du mit dem Zertifikat, das als Berechtigungsnachweis für deine Anwendung registriert wurde, erstellen und signieren musst.|
|grant_type|Erforderlich|Muss auf `client_credentials` festgelegt werden.|
|client_id|Optional|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde. Dies ist Teil von client_assertion, sodass es hier nicht übergeben werden muss.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen, denen der Benutzer zustimmen soll.|

### <a name="use-a-token"></a>Verwenden eines Tokens

Nachdem du jetzt ein Token abgerufen hast, stelle die Anforderungen an die Ressource mit dem Token. Wenn das Token abläuft, wiederholst du die Anforderung an den „/token“-Endpunkt, um ein neues Zugriffstoken zu erhalten.

```
GET /v1.0/me/messages
Host: https://webapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>Gewährungsflow für Kennwortanmeldeinformationen des Ressourcenbesitzers (nicht empfohlen)

Die Gewährung von Ressourcenbesitzer-Kennwortanmeldeinformationen ermöglicht es einer Anwendung, den Benutzer durch direkte Verarbeitung seines Kennworts anzumelden. Der Flow für Kennwortanmeldeinformationen des Ressourcenbesitzers erfordert ein hohes Maß an Vertrauen und potenzieller Benutzergefährdung, und du solltest diesen Flow nur verwenden, wenn andere, sicherere Flows nicht verwendet werden können.

### <a name="protocol-diagram"></a>Protokolldiagramm

Das folgende Diagramm zeigt den Flow für Kennwortanmeldeinformationen des Ressourcenbesitzers.

![ROPC-Flow (Resource Owner Password Credential)](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>Autorisierungsanforderung
Der ROPC-Flow ist eine einzelne Anforderung. Er sendet die Client-ID und die Anmeldeinformationen des Benutzers an den IDP und empfängt dann im Gegenzug entsprechende Token. Der Client muss vorher die E-Mail-Adresse (UPN) und das Kennwort des Benutzers anfordern. Unmittelbar nach einer erfolgreichen Anforderung muss der Client die Anmeldeinformationen des Benutzers sicher aus dem Arbeitsspeicher freigeben. Er darf sie niemals speichern.

```
// Line breaks and spaces are for legibility only.

POST /adfs/oauth2/token HTTP/1.1
Host: https://adfs.contoso.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope= openid
&username=myusername@contoso.com
&password=SuperS3cret
&grant_type=password
```


|Parameter|Erforderlich/Optional|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Client-ID|
|grant_type|Erforderlich|Muss auf „password“ festgelegt werden.|
|username|Erforderlich|Dies ist die E-Mail-Adresse des Benutzers.|
|password|Erforderlich|Das Kennwort des Benutzers.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|

### <a name="successful-authentication-response"></a>Erfolgreiche Authentifizierungsantwort.
Das folgende Beispiel stellt eine erfolgreiche Tokenantwort dar:

```
{
    "token_type": "Bearer",
    "scope": "openid",
    "expires_in": 3599,
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn...",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "refresh_token_expires_in": 28800,
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDR..."
}
```


|Parameter|BESCHREIBUNG|
|-----|-----|
|token_type|Immer auf „Bearer“ festgelegt.|
|scope|Wenn ein Zugriffstoken zurückgegeben wurde, listet dieser Parameter die Bereiche auf, für die das Zugriffstoken gültig ist.|
|expires_in|Anzahl der Sekunden, für die das enthaltene Zugriffstoken gültig ist.|
|access_token|Ausgestellt für die angeforderten Bereiche.|
|id_token|Ein JSON-Webtoken (JWT). Die App kann die Segmente dieses Tokens entschlüsseln, um Informationen über den Benutzer, der sich angemeldet hat, anzufordern. Die App kann die Werte zwischenspeichern und anzeigen, aber sie sollte sich nicht auf sie verlassen, wenn es um Autorisierung oder Sicherheitsbegrenzungen geht.|
|refresh_token_expires_in|Anzahl der Sekunden, für die das enthaltene Aktualisierungstoken gültig ist.|
|refresh_token|Wird ausgegeben, wenn der ursprüngliche Bereichsparameter offline_access enthalten hat.|

Du kannst das Aktualisierungstoken verwenden, um neue Zugriffstoken abzurufen und Token zu aktualisieren, indem du denselben Flow verwendest, der oben im Abschnitt über die Gewährung von Authentifizierungscode beschrieben ist.

## <a name="device-code-flow"></a>Gerätecodeflow

Durch die Gewährung von Gerätecode kann sich der Benutzer an Geräten mit beschränkten Eingabemöglichkeiten anmelden, z. B. Smart-TV, IoT-Gerät oder Drucker. Um diesen Flow zu ermöglichen, lässt das Gerät den Benutzer eine Webseite in seinem Browser auf einem anderen Gerät besuchen, um sich anzumelden. Nach der Anmeldung des Benutzers ist das Gerät in der Lage, Zugriffstoken zu erhalten und die Token bei Bedarf zu aktualisieren.

### <a name="protocol-diagram"></a>Protokolldiagramm

Der gesamte Gerätecodeflow sieht ähnlich wie im nächsten Diagramm aus. Wir beschreiben jeden dieser Schritte später in diesem Artikel.

![Gerätecodefluss](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>Geräteautorisierungsanforderung
Der Client muss zunächst mit dem Authentifizierungsserver nach einem Gerät und einem Benutzercode suchen, die zum Einleiten der Authentifizierung verwendet werden. Der Client erfasst diese Anforderung vom „/devicecode“-Endpunkt. In dieser Anforderung sollte der Client auch die Berechtigungen einbeziehen, die er vom Benutzer abrufen muss. Von dem Moment an, an dem diese Anforderung gesendet wird, hat der Benutzer nur 15 Minuten Zeit, um sich anzumelden (der übliche Wert für expires_in), also sollte diese Anforderung nur dann gestellt werden, wenn der Benutzer angegeben hat, dass er bereit ist, sich anzumelden.

```
// Line breaks are for legibility only.

POST https://adfs.contoso.com/adfs/oauth2/devicecode
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
scope=openid
```


|Parameter|Bedingung|Beschreibung|
|-----|-----|-----|
|client_id|Erforderlich|Die Anwendungs-ID (Client), die deiner App vom AD FS zugewiesen wurde.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|

### <a name="device-authorization-response"></a>Geräteautorisierungsantwort
Eine erfolgreiche Antwort wird ein JSON-Objekt sein, das die erforderlichen Informationen enthält, um dem Benutzer die Anmeldung zu ermöglichen.


|Parameter|Beschreibung|
|-----|-----|
|device_code|Eine lange Zeichenfolge, die zur Überprüfung der Sitzung zwischen dem Client und dem Autorisierungsserver verwendet wird. Der Client verwendet diesen Parameter, um das Zugriffstoken vom Autorisierungsserver anzufordern.|
|user_code|Eine kurze, dem Benutzer angezeigte Zeichenfolge, die zur Identifizierung der Sitzung auf einem sekundären Gerät verwendet wird.|
|verification_uri|Der URI, zu dem der Benutzer mit dem user_code wechseln sollte, um sich anzumelden.|
|verification_uri_complete|Der URI, zu dem der Benutzer mit dem user_code wechseln sollte, um sich anzumelden. Dieser ist mit user_code vorab ausgefüllt, sodass der Benutzer keinen user_code eingeben muss.|
|expires_in|Die Anzahl der Sekunden, bevor device_code und user_code ablaufen.|
|interval|Die Anzahl der Sekunden, die der Client zwischen den Abfrageanforderungen warten soll.|
|message|Eine von Menschen lesbare Zeichenfolge mit Anweisungen für den Benutzer. Dies kann lokalisiert werden, indem ein Abfrageparameter in die Anforderung der Form „?mkt=xx-XX“ einbezogen wird, wobei der entsprechende Sprachkulturcode ausgefüllt wird.

### <a name="authenticating-the-user"></a>Authentifizieren des Benutzers
Nachdem der Client den user_code und verification_uri erhalten hat, zeigt er diese dem Benutzer an und weist ihn an, sich mit seinem Mobiltelefon oder PC-Browser anzumelden. Zusätzlich kann der Client einen QR-Code oder einen ähnlichen Mechanismus verwenden, um verification_uri_complete anzuzeigen, der den Schritt der Eingabe des user_code für den Benutzer übernimmt.
Während sich der Benutzer am verification_uri authentifiziert, sollte der Client den /token-Endpunkt mit dem device_code nach dem angeforderten Token abfragen.

```
POST https://adfs.contoso.com /adfs/oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type: urn:ietf:params:oauth:grant-type:device_code
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8
```


|Parameter|Erforderlich|BESCHREIBUNG|
|-----|-----|-----|
|grant_type|Erforderlich|Muss „urn:ietf:params:oauth:grant-type:device_code“ sein.|
|client_id|Erforderlich|Muss mit der in der ursprünglichen Anforderung verwendeten client_id übereinstimmen.|
|code|Erforderlich|Der in der Geräteautorisierungsanforderung zurückgegebene device_code.|

### <a name="successful-authentication-response"></a>Erfolgreiche Authentifizierungsantwort.
Eine erfolgreiche Tokenantwort sieht wie folgt aus:


|Parameter|BESCHREIBUNG|
|-----|-----|
|token_type|Dies ist immer „Bearer“.|
|scope|Wenn ein Zugriffstoken zurückgegeben wurde, listet dies die Bereiche auf, für die das Zugriffstoken gültig ist.|
|expires_in|Anzahl der Sekunden, bevor das enthaltene Zugriffstoken gültig ist.|
|access_token|Ausgestellt für die angeforderten Bereiche.|
|id_token|Wird ausgegeben, wenn der ursprüngliche Bereichsparameter den openid-Bereich enthalten hat.|
|refresh_token|Wird ausgegeben, wenn der ursprüngliche Bereichsparameter offline_access enthalten hat.|
|refresh_token_expires_in|Anzahl der Sekunden, bevor das enthaltene Aktualisierungstoken gültig ist.|


## <a name="related-content"></a>Verwandte Themen
Die vollständige Liste der Artikel mit exemplarischen Vorgehensweisen ist in [AD FS-Entwicklung](../AD-FS-Development.md) verfügbar, worin schrittweise Anweisungen zur Verwendung der entsprechenden Flows bereitgestellt werden.
