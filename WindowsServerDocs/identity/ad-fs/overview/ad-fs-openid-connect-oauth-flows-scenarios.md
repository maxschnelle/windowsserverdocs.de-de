---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS OpenID Connect/OAuth-Flows und Anwendungsszenarien
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e1e0235e50945fadd09fe9dd5ffeaf6d7119e482
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385601"
---
# <a name="ad-fs-openid-connectoauth-flows-and-application-scenarios"></a>AD FS OpenID Connect/OAuth-Flows und Anwendungsszenarien
Gilt für AD FS 2016 und höher


|Szenario|Exemplarische Vorgehensweise mit Beispielen|OAuth 2,0 Fluss/Gewährung|Clienttyp|
|-----|-----|-----|-----|
|Einseitige App</br> | &bull; [Beispiel mit Adal](../development/Single-Page-Application-with-AD-FS.md)|[Verzerrungen](#implicit-grant-flow)|Public| 
|Web-App, die Benutzer anmeldet</br> | &bull; [Beispiel mit owin](../development/enabling-openid-connect-with-ad-fs.md)|[Autorisierungs Code](#authorization-code-grant-flow)|Öffentlich, vertraulich|  
|Native App Ruft Web-API auf</br>|&bull; [Beispiel mit msal](../development/msal/adfs-msal-native-app-web-api.md)</br>&bull; [Beispiel mit Adal](../development/native-client-with-ad-fs.md)|[Autorisierungs Code](#authorization-code-grant-flow)|Public|   
|Web-App Ruft Web-API auf</br>|&bull; [Beispiel mit msal](../development/msal/adfs-msal-web-app-web-api.md)</br>&bull; [Beispiel mit Adal](../development/enabling-oauth-confidential-clients-with-ad-fs.md)|[Autorisierungs Code](#authorization-code-grant-flow)|Vertraulich| 
|Die Web-API ruft eine andere Web-API im Namen von (OBO) des Benutzers auf.</br>|&bull; [Beispiel mit msal](../development/msal/adfs-msal-web-api-web-api.md)</br>&bull; [Beispiel mit Adal](../development/ad-fs-on-behalf-of-authentication-in-windows-server.md)|[Im Auftrag von](#on-behalf-of-flow)|Die Web-App fungiert als vertraulich.| 
|Daemon-App Ruft Web-API auf||[Client Anmelde Informationen](#client-credentials-grant-flow)|Vertraulich| 
|Web-App Ruft Web-API mithilfe von Benutzer-Anmelde-apps||[Kenn Wort Anmelde Informationen des Ressourcen Besitzers](#resource-owner-password-credentials-grant-flow-not-recommended)|Öffentlich, vertraulich| 
|Browser lose App Ruft Web-API auf||[Geräte Code](#device-code-flow)|Öffentlich, vertraulich| 

## <a name="implicit-grant-flow"></a>Impliziter Datenfluss 
 
Für Single-Page-Anwendungen (angularjs, Ember. js, "reagieren. js" usw.) unterstützt AD FS den impliziten OAuth 2,0-Grant-Flow. Der implizite Fluss wird in der [OAuth 2,0-Spezifikation](https://tools.ietf.org/html/rfc6749#section-4.2)beschrieben. Der Hauptvorteil besteht darin, dass die APP Token aus AD FS erhalten kann, ohne dass ein Back-End-Server Anmelde Informationsaustausch durchgeführt werden muss. Dies ermöglicht es der APP, den Benutzer anzumelden, die Sitzung beizubehalten und Token für andere Web-APIs zu erhalten, die sich im JavaScript-Code des Clients befinden. Es gibt einige wichtige Sicherheitsaspekte, die Sie berücksichtigen sollten, wenn Sie den impliziten Fluss speziell im Hinblick auf den [Client](https://tools.ietf.org/html/rfc6749#section-10.3)verwenden.  
 
Wenn Sie den impliziten Fluss und AD FS verwenden möchten, um der JavaScript-App Authentifizierung hinzuzufügen, führen Sie die folgenden allgemeinen Schritte aus.  
  
### <a name="protocol-diagram"></a>Protokoll Diagramm

Das folgende Diagramm zeigt, wie der gesamte implizite Anmeldungs Fluss aussieht, und in den folgenden Abschnitten werden die einzelnen Schritte ausführlicher beschrieben.  

![Implizite Anmeldung](media/adfs-scenarios-for-developers/implicit.png)

### <a name="request-id-token-and-access-token"></a>Anforderungs-ID-Token und Zugriffs Token 
 
Um den Benutzer anfänglich bei Ihrer APP zu signieren, können Sie eine OpenID Connect-Authentifizierungsanforderung senden und id_token und Zugriffs Token vom AD FS Endpunkt abrufen.  
 
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
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.| 
|response_type|Erforderlich|Muss `id_token` für die OpenID Connect-Anmeldung enthalten. Sie kann auch die response_type `token`enthalten. Wenn Sie das Token hier verwenden, kann Ihre APP ein Zugriffs Token direkt vom Autorisierungs Endpunkt empfangen, ohne dass eine zweite Anforderung an den tokenendpunkt gesendet werden muss.| 
|redirect_uri|Erforderlich|Der redirect_uri Ihrer APP, in dem Authentifizierungs Antworten gesendet und von Ihrer APP empfangen werden können. Er muss genau mit einem der redirect_uris übereinstimmen, die Sie in AD FS konfiguriert haben.| 
|Nonce|Erforderlich|Ein in der Anforderung enthaltener Wert, der von der APP generiert wird und in der resultierenden id_token als Anspruch enthalten ist. Die APP kann diesen Wert dann überprüfen, um Token-Replay-Angriffe zu verringern. Der Wert ist in der Regel eine zufällige, eindeutige Zeichenfolge, die verwendet werden kann, um den Ursprung der Anforderung zu identifizieren. Nur erforderlich, wenn eine id_token angefordert wird.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen. Für OpenID Connect muss der Bereich `openid`enthalten sein.|
|Ressource|Optional|Die URL Ihrer Web-API.</br>Hinweis – Wenn Sie die msal-Client Bibliothek verwenden, wird der Ressourcen Parameter nicht gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichs Parameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource nicht an dieser Stelle oder im Bereich verwendet wird, verwendet ADFS einen Standard Ressourcen-urn: Microsoft: userinfo. userinfo-Ressourcen Richtlinien (z. b. MFA, Ausstellung oder Autorisierungs Richtlinie) können nicht angepasst werden.| 
|response_mode|Optional| Gibt die Methode an, die zum Senden des resultierenden Tokens an Ihre APP verwendet werden soll. Wird standardmäßig auf `fragment` festgelegt.| 
|state|Optional|Ein in der Anforderung enthaltener Wert, der auch in der tokenantwort zurückgegeben wird. Dabei kann es sich um eine Zeichenfolge eines beliebigen Inhalts handeln, den Sie wünschen. Ein zufällig generierter eindeutiger Wert wird normalerweise verwendet, um Website übergreifende Anforderungs Fälschungs Angriffe zu verhindern. Der Status wird auch verwendet, um Informationen über den Status des Benutzers in der APP zu codieren, bevor die Authentifizierungsanforderung aufgetreten ist, z. b. die Seite oder Ansicht, auf der Sie sich befanden.| 
|prompt|Optional|Gibt den Typ der erforderlichen Benutzerinteraktion an. Zu diesem Zeitpunkt sind die einzigen gültigen Werte "Login" und "None".</br>- `prompt=login` erzwingen, dass der Benutzer seine Anmelde Informationen für diese Anforderung eingibt, wobei einmaliges Anmelden nicht mehr möglich ist. </br>- `prompt=none` ist das Gegenteil. es wird sichergestellt, dass dem Benutzer keine interaktive Eingabeaufforderung angezeigt wird. Wenn die Anforderung nicht über einmaliges Anmelden im Hintergrund abgeschlossen werden kann, wird AD FS interaction_required Fehler zurückgegeben.| 
|login_hint|Optional|Kann verwendet werden, um das Feld Benutzername/e-Mail-Adresse auf der Anmeldeseite vorab für den Benutzer auszufüllen, wenn Sie Ihren Benutzernamen im Voraus kennen. Apps verwenden diesen Parameter häufig während der erneuten Authentifizierung, indem Sie den Benutzernamen bereits aus einer vorherigen Anmeldung mithilfe des `upn` -Anspruchs von `id_token`extrahiert haben.| 
|domain_hint|Optional|Wenn Sie enthalten ist, wird der Domänen basierte Ermittlungs Vorgang übersprungen, den der Benutzer auf der Anmeldeseite durchläuft, was zu einem etwas optimierten Benutzererlebnis führt.| 

An diesem Punkt wird der Benutzer aufgefordert, seine Anmelde Informationen einzugeben und die Authentifizierung abzuschließen. Nachdem sich der Benutzer authentifiziert hat, gibt der AD FS Autorisierungs Endpunkt eine Antwort an die APP an der angegebenen redirect_uri zurück. dabei wird die im response_mode-Parameter angegebene Methode verwendet.  
 
### <a name="successful-response"></a>Erfolgreiche Antwort 
 
Eine erfolgreiche Antwort mit `response_mode=fragment and response_type=id_token+token` sieht wie folgt aus:  
 
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
|access_token|Enthalten, wenn response_type `token`enthält.|
|token_type|Enthalten, wenn response_type `token`enthält. Wird immer Bearer.| 
|expires_in| Enthalten, wenn response_type `token`enthält. Gibt die Anzahl der Sekunden an, die das Token für die Zwischenspeicherung gültig ist.| 
|scope| Gibt die Bereiche an, für die das access_token gültig ist.|  
|id_token|Enthalten, wenn response_type `id_token`enthält. Ein signiertes JSON Web Token (JWT). Die APP kann die Segmente dieses Tokens decodieren, um Informationen über den angemeldeten Benutzer anzufordern. Die APP kann die Werte Zwischenspeichern und anzeigen, aber Sie sollte für Autorisierungs-oder Sicherheitsgrenzen nicht darauf basieren.| 
|state|Wenn ein Status Parameter in der Anforderung enthalten ist, sollte der gleiche Wert in der Antwort angezeigt werden. Die APP sollte überprüfen, ob die Statuswerte in der Anforderung und in der Antwort identisch sind.|

### <a name="refresh-tokens"></a>Token aktualisieren 
Die implizite Gewährung stellt keine Aktualisierungs Token bereit. Sowohl `id_tokens` als auch `access_tokens` laufen nach kurzer Zeit ab. Ihre APP muss daher darauf vorbereitet sein, diese Token in regelmäßigen Abständen zu aktualisieren. Zum Aktualisieren beider Tokentypen können Sie dieselbe ausgeblendete IFRAME-Anforderung ausführen, indem Sie den `prompt=none` -Parameter verwenden, um das Verhalten der Identitäts Plattform zu steuern. Wenn Sie einen `new id_token`erhalten möchten, achten Sie darauf, dass Sie `response_type=id_token`verwenden. 

## <a name="authorization-code-grant-flow"></a>Autorisierungs Code-Zuweisungs Fluss 
 
Die OAuth 2,0-Autorisierungs Code Gewährung kann in Web-Apps verwendet werden, um Zugriff auf geschützte Ressourcen wie Web-APIs zu erhalten. Der OAuth 2,0-Autorisierungs Code Fluss wird in [Abschnitt 4,1 der OAuth 2,0-Spezifikation](https://tools.ietf.org/html/rfc6749)beschrieben. Sie wird verwendet, um die Authentifizierung und Autorisierung in den meisten App-Typen auszuführen, einschließlich Web-Apps und nativ installierten apps. Mit dem Flow können apps access_tokens sicher abrufen, die für den Zugriff auf Ressourcen verwendet werden können, die AD FS Vertrauen.  
 
### <a name="protocol-diagram"></a>Protokoll Diagramm 
 
Auf hoher Ebene sieht der Authentifizierungs Ablauf für eine native Anwendung etwas so aus:

![Autorisierungs Code-Zuweisungs Fluss](media/adfs-scenarios-for-developers/authorization.png)

### <a name="request-an-authorization-code"></a>Anfordern eines Autorisierungscodes 
 
Der Autorisierungs Code Fluss beginnt damit, dass der Client den Benutzer an den/Authorize-Endpunkt-Endpunkt weiterleitet. In dieser Anforderung gibt der Client die Berechtigungen an, die er vom Benutzer abrufen muss: 
 
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
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.|  
|response_type|Erforderlich| Muss Code für den Autorisierungs Code Fluss enthalten.| 
|redirect_uri|Erforderlich|Der `redirect_uri` Ihrer APP, in dem Authentifizierungs Antworten gesendet und von Ihrer APP empfangen werden können. Er muss genau mit einem der redirect_uris übereinstimmen, die Sie in der AD FS für den Client registriert haben.|  
|Ressource|Optional|Die URL Ihrer Web-API.</br>Hinweis – Wenn Sie die msal-Client Bibliothek verwenden, wird der Ressourcen Parameter nicht gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichs Parameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource nicht an dieser Stelle oder im Bereich verwendet wird, verwendet ADFS einen Standard Ressourcen-urn: Microsoft: userinfo. userinfo-Ressourcen Richtlinien (z. b. MFA, Ausstellung oder Autorisierungs Richtlinie) können nicht angepasst werden.| 
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|
|response_mode|Optional|Gibt die Methode an, die zum Senden des resultierenden Tokens an Ihre APP verwendet werden soll. Kann einen der folgenden Werte annehmen: </br>-Abfrage </br>-Fragment </br>-form_post</br>`query` stellt den Code als Abfrage Zeichenfolgen-Parameter für den Umleitungs-URI bereit. Wenn Sie den Code anfordern, können Sie Abfragen, Fragmente oder form_post verwenden. `form_post` führt einen Beitrag aus, der den Code für den Umleitungs-URI enthält.|
|state|Optional|Ein in der Anforderung enthaltener Wert, der auch in der tokenantwort zurückgegeben wird. Dabei kann es sich um eine Zeichenfolge eines beliebigen Inhalts handeln, den Sie wünschen. Ein zufällig generierter eindeutiger Wert wird normalerweise verwendet, um Website übergreifende Anforderungs Fälschungs Angriffe zu verhindern. Der Wert kann auch Informationen über den Status des Benutzers in der APP codieren, bevor die Authentifizierungsanforderung aufgetreten ist, z. b. die Seite oder Ansicht, auf der Sie sich befanden.|
|prompt|Optional|Gibt den Typ der erforderlichen Benutzerinteraktion an. Zu diesem Zeitpunkt sind die einzigen gültigen Werte "Login" und "None".</br>- `prompt=login` erzwingen, dass der Benutzer seine Anmelde Informationen für diese Anforderung eingibt, wobei einmaliges Anmelden nicht mehr möglich ist. </br>- `prompt=none` ist das Gegenteil. es wird sichergestellt, dass dem Benutzer keine interaktive Eingabeaufforderung angezeigt wird. Wenn die Anforderung nicht über einmaliges Anmelden im Hintergrund abgeschlossen werden kann, wird AD FS interaction_required Fehler zurückgegeben.|
|login_hint|Optional|Kann verwendet werden, um das Feld Benutzername/e-Mail-Adresse auf der Anmeldeseite für den Benutzer vorab auszufüllen, wenn Sie Ihren Benutzernamen im Voraus kennen. Apps verwenden diesen Parameter häufig während der erneuten Authentifizierung, indem Sie den Benutzernamen bereits aus einer vorherigen Anmeldung mithilfe des `upn`-Anspruchs von `id_token`extrahiert haben.|
|domain_hint|Optional|Wenn Sie enthalten ist, wird der Domänen basierte Ermittlungs Vorgang übersprungen, den der Benutzer auf der Anmeldeseite durchläuft, was zu einem etwas optimierten Benutzererlebnis führt.|
|code_challenge_method|Optional|Die Methode, die zum Codieren der code_verifier für den code_challenge-Parameter verwendet wird. Kann einer der folgenden Werte sein: </br>-Plain </br>- S256 </br>Wenn Sie ausgeschlossen ist, wird code_challenge als Klartext angenommen, wenn `code_challenge` eingeschlossen ist. AD FS unterstützt sowohl Plain als auch S256. Weitere Informationen finden Sie unter [pkce RFC](https://tools.ietf.org/html/rfc7636).|
|code_challenge|Optional| Dient zum Sichern von Autorisierungs Code Zuweisungen über den Prüfschlüssel für Code Austausch (pkce) von einem Native Client. Erforderlich, wenn `code_challenge_method` eingeschlossen ist. Weitere Informationen finden Sie unter [pkce RFC](https://tools.ietf.org/html/rfc7636) .|

An diesem Punkt wird der Benutzer aufgefordert, seine Anmelde Informationen einzugeben und die Authentifizierung abzuschließen. Nachdem sich der Benutzer authentifiziert hat, gibt der AD FS eine Antwort an die APP an der angegebenen `redirect_uri`zurück. dabei wird die im `response_mode` Parameter angegebene Methode verwendet.  
 
### <a name="successful-response"></a>Erfolgreiche Antwort 
 
Eine erfolgreiche Antwort mit response_mode = Abfrage sieht wie folgt aus: 
 
```
GET https://adfs.contoso.com/common/oauth2/nativeclient? 
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq... 
&state=12345  
```


|Parameter|Beschreibung|
|-----|-----|
|code|Der `authorization_code`, den die APP angefordert hat. Die APP kann den Autorisierungs Code zum Anfordern eines Zugriffs Tokens für die Ziel Ressource verwenden. Authorization_codes sind kurzlebig, Sie laufen in der Regel nach ungefähr 10 Minuten ab.|
|state|Wenn ein `state` Parameter in der Anforderung enthalten ist, sollte der gleiche Wert in der Antwort angezeigt werden. Die APP sollte überprüfen, ob die Statuswerte in der Anforderung und in der Antwort identisch sind.|

### <a name="request-an-access-token"></a>Anfordern eines Zugriffs Tokens 
 
Nachdem Sie nun eine `authorization_code` abgerufen und die Berechtigung vom Benutzer erhalten haben, können Sie den Code für eine `access_token` der gewünschten Ressource einlösen. Senden Sie hierzu eine Post-Anforderung an den/Token-Endpunkt:  
 
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
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.| 
|grant_type|Erforderlich|Muss für den Autorisierungs Code Fluss `authorization_code` sein.| 
|code|Erforderlich|Die `authorization_code`, die Sie im ersten Abschnitt des Flows abgerufen haben.| 
|redirect_uri|Erforderlich|Derselbe `redirect_uri` Wert, der zum Abrufen des `authorization_code`verwendet wurde.| 
|client_secret|erforderlich für Web-Apps|Der geheime Anwendungs Schlüssel, den Sie bei der APP-Registrierung in AD FS erstellt haben. Sie sollten den geheimen Anwendungs Schlüssel nicht in einer nativen App verwenden, da client_secrets nicht zuverlässig auf Geräten gespeichert werden können. Dies ist für Web-Apps und Web-APIs erforderlich, die die client_secret sicher auf der Serverseite speichern können. Der geheime Client Schlüssel muss vor dem Senden URL-codiert sein. Diese Apps können auch eine Schlüssel basierte Authentifizierung verwenden, indem ein JWT signiert und als client_assertion-Parameter hinzugefügt wird.| 
|code_verifier|Optional|Dieselbe `code_verifier`, die zum Abrufen des authorization_code verwendet wurde. Erforderlich, wenn pkce in der Anforderung zum Erteilen von Autorisierungscodes verwendet wurde. Weitere Informationen finden Sie unter [pkce RFC](https://tools.ietf.org/html/rfc7636).</br>Hinweis – gilt für AD FS 2019 und höher| 

### <a name="successful-response"></a>Erfolgreiche Antwort 
 
Eine erfolgreiche tokenantwort sieht wie folgt aus: 
 
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
|access_token|Das angeforderte Zugriffs Token. Die APP kann dieses Token verwenden, um sich bei der gesicherten Ressource (Web-API) zu authentifizieren.| 
|token_type|Gibt den Tokentyp Wert an. Der einzige Typ, den AD FS unterstützt, ist Bearer.
|expires_in|Gibt an, wie lange das Zugriffs Token gültig ist (in Sekunden).
|refresh_token|Ein OAuth 2,0-Aktualisierungs Token. Die APP kann dieses Token verwenden, um zusätzliche Zugriffs Token zu erhalten, nachdem das aktuelle Zugriffs Token abgelaufen ist. Refresh_tokens sind langlebig und können verwendet werden, um den Zugriff auf Ressourcen für längere Zeit beizubehalten.| 
|refresh_token_expires_in|Gibt an, wie lange das Aktualisierungs Token gültig ist (in Sekunden).| 
|id_token|Eine JSON Web Token (JWT). Die APP kann die Segmente dieses Tokens decodieren, um Informationen über den angemeldeten Benutzer anzufordern. Die APP kann die Werte Zwischenspeichern und anzeigen, aber Sie sollte für Autorisierungs-oder Sicherheitsgrenzen nicht darauf basieren.|

### <a name="use-the-access-token"></a>Verwenden des Zugriffs Tokens 
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q... 
 ```

### <a name="refresh-the-access-token"></a>Aktualisieren des Zugriffs Tokens 
 
Access_tokens sind kurzlebig, und Sie müssen Sie nach Ablauf aktualisieren, damit Sie weiterhin auf Ressourcen zugreifen können. Hierzu können Sie eine andere Post-Anforderung an den `/token` -Endpunkt senden. dieses Mal wird der refresh_token anstelle des Codes bereitgestellt. Aktualisierungs Token sind für alle Berechtigungen gültig, für die der Client bereits Zugriffs Token erhalten hat. 
 
Aktualisierungs Token verfügen nicht über die angegebene Lebensdauer. Die Lebensdauer von Aktualisierungs Token ist in der Regel relativ lang. In einigen Fällen laufen Aktualisierungs Token jedoch ab, werden gesperrt oder verfügen nicht über ausreichende Berechtigungen für die gewünschte Aktion. Die Anwendung muss vom tokenausstellungs-Endpunkt zurückgegebene Fehler erwarten und behandeln.  
 
Obwohl Aktualisierungs Token nicht widerrufen werden, wenn Sie zum Abrufen neuer Zugriffs Token verwendet werden, wird davon ausgegangen, dass Sie das alte Aktualisierungs Token verwerfen. Die OAuth 2,0-Spezifikation besagt: "der autorisierungsserver gibt möglicherweise ein neues Aktualisierungs Token aus. in diesem Fall muss der Client das alte Aktualisierungs Token verwerfen und durch das neue Aktualisierungs Token ersetzen. Der autorisierungsserver kann das alte Aktualisierungs Token widerrufen, nachdem ein neues Aktualisierungs Token für den Client ausgegeben wurde. " 
 
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
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.| 
|grant_type|Erforderlich|Muss für diesen Abschnitt des Autorisierungs Code Flusses `refresh_token` sein.| 
|Ressource|Optional|Die URL Ihrer Web-API.</br>Hinweis – Wenn Sie die msal-Client Bibliothek verwenden, wird der Ressourcen Parameter nicht gesendet. Stattdessen wird die Ressourcen-URL als Teil des Bereichs Parameters gesendet: `scope = [resource url]//[scope values e.g., openid]`</br>Wenn die Ressource nicht an dieser Stelle oder im Bereich verwendet wird, verwendet ADFS einen Standard Ressourcen-urn: Microsoft: userinfo. userinfo-Ressourcen Richtlinien (z. b. MFA, Ausstellung oder Autorisierungs Richtlinie) können nicht angepasst werden.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.| 
|refresh_token|Erforderlich|Die refresh_token, die Sie im zweiten Abschnitt des Flows abgerufen haben.| 
|client_secret|erforderlich für Web-Apps| Der geheime Anwendungs Schlüssel, den Sie im App-Registrierungs Portal für Ihre APP erstellt haben. Er sollte nicht in einer nativen App verwendet werden, da client_secrets nicht zuverlässig auf Geräten gespeichert werden können. Dies ist für Web-Apps und Web-APIs erforderlich, die die client_secret sicher auf der Serverseite speichern können. Diese Apps können auch eine Schlüssel basierte Authentifizierung verwenden, indem ein JWT signiert und als client_assertion-Parameter hinzugefügt wird.|

### <a name="successful-response"></a>Erfolgreiche Antwort 
Eine erfolgreiche tokenantwort sieht wie folgt aus: 
 
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
|access_token|Das angeforderte Zugriffs Token. Die APP kann dieses Token verwenden, um sich bei der gesicherten Ressource (z. b. einer Web-API) zu authentifizieren.| 
|token_type|Gibt den Tokentyp Wert an. Der einzige Typ, den AD FS unterstützt, ist Bearer|
|expires_in|Gibt an, wie lange das Zugriffs Token gültig ist (in Sekunden).|
|scope|Die Bereiche, für die der access_token gültig ist.| 
|refresh_token|Ein OAuth 2,0-Aktualisierungs Token. Die APP kann dieses Token verwenden, um zusätzliche Zugriffs Token zu erhalten, nachdem das aktuelle Zugriffs Token abgelaufen ist. Refresh_tokens sind langlebig und können verwendet werden, um den Zugriff auf Ressourcen für längere Zeit beizubehalten.| 
|refresh_token_expires_in|Gibt an, wie lange das Aktualisierungs Token gültig ist (in Sekunden).| 
|id_token|Eine JSON Web Token (JWT). Die APP kann die Segmente dieses Tokens decodieren, um Informationen über den angemeldeten Benutzer anzufordern. Die APP kann die Werte Zwischenspeichern und anzeigen, aber Sie sollte für Autorisierungs-oder Sicherheitsgrenzen nicht darauf basieren.|

## <a name="on-behalf-of-flow"></a>"Im Auftrag von"-Ablauf 
 
Der "im Auftrag von"-Flow (OBO) von OAuth 2,0 stellt den Anwendungsfall dar, in dem eine Anwendung eine Dienst-/Web-API aufruft, die wiederum eine andere Dienst-oder Web-API aufrufen muss. Die Idee besteht darin, die Delegierte Benutzeridentität und die Berechtigungen über die Anforderungs Kette weiterzugeben. Damit der Dienst der mittleren Ebene authentifizierte Anforderungen an den Downstreamdienst senden kann, muss er im Auftrag des Benutzers ein Zugriffs Token vom AD FS sichern.  
 
### <a name="protocol-diagram"></a>Protokoll Diagramm 
Nehmen Sie an, dass der Benutzer in einer Anwendung authentifiziert wurde, indem Sie den oben beschriebenen OAuth 2,0 Authorization Code Grant-Datenfluss verwenden. An diesem Punkt verfügt die Anwendung über ein Zugriffs Token für API a (Token a) mit den Ansprüchen des Benutzers und der Zustimmung für den Zugriff auf die Web-API der mittleren Ebene (API a). Stellen Sie sicher, dass der Client user_impersonation Gültigkeitsbereich im Token anfordert. API a muss nun eine authentifizierte Anforderung an die downstreamweb-API (API B) senden. 

Die folgenden Schritte bilden den OBO-Flow und werden anhand des folgenden Diagramms erläutert. 

!["Im Auftrag von"-Ablauf](media/adfs-scenarios-for-developers/obo.png)

  1. Die Client Anwendung sendet eine Anforderung an API a mit Token a.  
  Hinweis: beim Konfigurieren von OBO Flow in AD FS Sie sicherstellen, dass der Bereich `user_impersonation` ausgewählt ist, und der Client fordert `user_impersonation` Bereich in der Anforderung an. 
  2. API a authentifiziert sich beim Endpunkt der AD FS Tokenausstellung und fordert ein Token für den Zugriff auf API B an. Hinweis: beim Konfigurieren dieses Flows in AD FS stellen Sie sicher, dass API a auch als Serveranwendung registriert ist, bei der ClientID den gleichen Wert wie die Ressourcen-ID in API A hat. Weitere Informationen finden Sie im Namen von Sample here Add Link.  
  3. Der AD FS tokenausstellungs-Endpunkt überprüft die Anmelde Informationen von API A mit Token a und gibt das Zugriffs Token für API B (Token b) aus. 
  4. Token b wird im Autorisierungs Header der Anforderung an API B festgelegt. 
  5. Daten aus der gesicherten Ressource werden von API B zurückgegeben. 

### <a name="service-to-service-access-token-request"></a>Dienst-zu-Dienst-zugriffstokenanforderung 
 
Um ein Zugriffs Token anzufordern, erstellen Sie eine HTTP POST-Anforderung mit den folgenden Parametern an den AD FS tokenendpunkt.  


### <a name="first-case-access-token-request-with-a-shared-secret"></a>Erster Fall: zugriffstokenanforderung mit einem gemeinsamen geheimen Schlüssel 
 
Bei Verwendung eines gemeinsamen geheimen Schlüssels enthält eine Dienst-zu-Dienst-zugriffstokenanforderung die folgenden Parameter: 


|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----| 
|grant_type|Erforderlich|Der Typ der Tokenanforderung. Bei einer Anforderung mit einem JWT muss der Wert urn: IETF: Parameter: OAuth: Grant-Type: JWT-Träger sein.|  
|client_id|Erforderlich|Die Client-ID, die Sie konfigurieren, wenn Sie Ihre erste Web-API als Server-App registrieren (app der mittleren Ebene). Dies sollte mit der im ersten Abschnitt verwendeten Ressourcen-ID identisch sein, also mit der URL der ersten Web-API.| 
|client_secret|Erforderlich|Der geheime Anwendungs Schlüssel, den Sie bei der Registrierung der Server-app in AD FS erstellt haben.| 
|Assertion|Erforderlich|Der Wert des in der Anforderung verwendeten Tokens.|  
|requested_token_use|Erforderlich|Gibt an, wie die Anforderung verarbeitet werden soll. Im OBO-Flow muss der Wert auf festgelegt werden on_behalf_of| 
|Ressource|Erforderlich|Die Ressourcen-ID, die beim Registrieren der ersten Web-API als Server-app (mittlere Ebene-APP) bereitgestellt wird. Die Ressourcen-ID sollte die URL der zweiten Web-API-APP der mittleren Ebene sein, die im Auftrag des Clients aufruft.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen für die Tokenanforderung.| 

#### <a name="example"></a>Beispiel 
 
Der folgende `HTTP POST` fordert ein Zugriffs Token und ein Aktualisierungs Token an. 
 
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

### <a name="second-case-access-token-request-with-a-certificate"></a>Zweiter Fall: zugriffstokenanforderung mit einem Zertifikat 
 
Eine Dienst-zu-Dienst-zugriffstokenanforderung mit einem Zertifikat enthält die folgenden Parameter: 


|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----| 
|grant_type|Erforderlich|Der Typ der Tokenanforderung. Bei einer Anforderung mit einem JWT muss der Wert urn: IETF: Parameter: OAuth: Grant-Type: JWT-Träger sein. |
|client_id|Erforderlich|Die Client-ID, die Sie konfigurieren, wenn Sie Ihre erste Web-API als Server-App registrieren (app der mittleren Ebene). Dies sollte mit der im ersten Abschnitt verwendeten Ressourcen-ID identisch sein, also mit der URL der ersten Web-API.|  
|client_assertion_type|Erforderlich|Der Wert muss "urn: IETF: parameams: OAuth: Client-Assert-Type: JWT-bearername" lauten.| 
|client_assertion|Erforderlich|Eine-Bestätigung (ein JSON-webtoken), die Sie erstellen und mit dem Zertifikat signieren müssen, das Sie als Anmelde Informationen für Ihre Anwendung registriert haben.|  
|Assertion|Erforderlich|Der Wert des in der Anforderung verwendeten Tokens.| 
|requested_token_use|Erforderlich|Gibt an, wie die Anforderung verarbeitet werden soll. Im OBO-Flow muss der Wert auf festgelegt werden on_behalf_of| 
|Ressource|Erforderlich|Die Ressourcen-ID, die beim Registrieren der ersten Web-API als Server-app (mittlere Ebene-APP) bereitgestellt wird. Die Ressourcen-ID sollte die URL der zweiten Web-API-APP der mittleren Ebene sein, die im Auftrag des Clients aufruft.|
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen für die Tokenanforderung.|


Beachten Sie, dass die Parameter fast identisch sind, wie bei der Anforderung nach einem gemeinsamen geheimen Schlüssel, mit dem Unterschied, dass der client_secret Parameter durch zwei Parameter ersetzt wird: client_assertion_type und client_assertion. 

#### <a name="example"></a>Beispiel 
Der folgende HTTP Post fordert ein Zugriffs Token für die Web-API mit einem Zertifikat an.

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

### <a name="service-to-service-access-token-response"></a>Antwort auf Dienst-zu-Dienst-Zugriffs Token 
 
Eine Erfolgs Antwort ist eine JSON OAuth 2,0-Antwort mit den folgenden Parametern. 


|Parameter|Beschreibung|
|-----|-----| 
|token_type|Gibt den Tokentyp Wert an. Der einzige Typ, den AD FS unterstützt, ist Bearer. | 
|scope|Der im Token gewährte Zugriffs Bereich.| 
|expires_in|Die Zeitspanne in Sekunden, für die das Zugriffs Token gültig ist.| 
|access_token|Das angeforderte Zugriffs Token. Der aufrufende Dienst kann dieses Token verwenden, um sich beim empfangenden Dienst zu authentifizieren.| 
|id_token|Eine JSON Web Token (JWT). Die APP kann die Segmente dieses Tokens decodieren, um Informationen über den angemeldeten Benutzer anzufordern. Die APP kann die Werte Zwischenspeichern und anzeigen, aber Sie sollte für Autorisierungs-oder Sicherheitsgrenzen nicht darauf basieren.| 
|refresh_token|Das Aktualisierungs Token für das angeforderte Zugriffs Token. Der aufrufende Dienst kann dieses Token verwenden, um ein anderes Zugriffs Token anzufordern, nachdem das aktuelle Zugriffs Token abläuft.|
|Refresh_token_expires_in|Die Zeitspanne in Sekunden, für die das Aktualisierungs Token gültig ist. 

### <a name="success-response-example"></a>Beispiel für eine Erfolgs Antwort 
 
Das folgende Beispiel zeigt eine erfolgreiche Antwort auf eine Anforderung für ein Zugriffs Token für die Web-API. 

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
 
 
Verwenden Sie das Zugriffs Token für den Zugriff auf die gesicherte Ressource. nun kann der Dienst der mittleren Ebene das oben erhaltene Token verwenden, um authentifizierte Anforderungen an die Downstream-Web-API zu senden, indem das Token im Autorisierungs Header festgelegt wird.  

#### <a name="example"></a>Beispiel 
``` 
GET /v1.0/me HTTP/1.1 
Host: https://secondwebapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQ… 
``` 

## <a name="client-credentials-grant-flow"></a>Flow zum Gewähren von Client Anmelde Informationen 
 
Sie können die in [RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4)angegebene Gewährung von OAuth 2,0-Client Anmelde Informationen verwenden, um mithilfe der Identität einer Anwendung auf im Internet gehostete Ressourcen zuzugreifen. Diese Art von Gewährung wird häufig für Interaktionen zwischen Servern verwendet, die ohne unmittelbare Interaktion mit einem Benutzer im Hintergrund ausgeführt werden müssen. Diese Anwendungs Typen werden oft als Daemons oder Dienst Konten bezeichnet. 

Der Flow zum Gewähren von OAuth 2,0-Client Anmelde Informationen ermöglicht einem Webdienst (vertraulicher Client), seine eigenen Anmelde Informationen zu verwenden, anstatt die Identität eines Benutzers anzunehmen, um sich beim Aufrufen eines anderen Webdiensts zu authentifizieren. In diesem Szenario ist der Client normalerweise ein Webdienst der mittleren Ebene, ein daemondienst oder eine Website. Ein höheres Maß an AD FS Sicherheit ermöglicht dem aufrufenden Dienst auch, ein Zertifikat (anstelle eines gemeinsamen geheimen Schlüssels) als Anmelde Informationen zu verwenden. 

### <a name="protocol-diagram"></a>Protokoll Diagramm 

Das folgende Diagramm zeigt den Datenfluss zur Gewährung von Client Anmelde Informationen. 

![Client Anmelde Informationen](media/adfs-scenarios-for-developers/credentials.png)

### <a name="request-a-token"></a>Anfordern eines Tokens 
 
Um ein Token mithilfe der Gewährung von Client Anmelde Informationen zu erhalten, senden Sie eine `POST` Anforderung an den/Token-AD FS Endpunkt:  
 
### <a name="first-case-access-token-request-with-a-shared-secret"></a>Erster Fall: zugriffstokenanforderung mit einem gemeinsamen geheimen Schlüssel 
 
```
POST /adfs/oauth2/token HTTP/1.1            
//Line breaks for clarity 
 
Host: https://adfs.contoso.com 
Content-Type: application/x-www-form-urlencoded 
 
client_id=535fb089-9ff3-47b6-9bfb-4f1264799865 
&client_secret=qWgdYAmab0YSkuL1qKv5bPX 
&grant_type=client_credentials 
```

|Parameter|Erforderlich/optional|Beschreibung|
|-----|-----|-----| 
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.| 
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen, denen der Benutzer zustimmen soll.| 
|client_secret|Erforderlich|Der geheime Client Schlüssel, den Sie für Ihre APP im App-Registrierungs Portal generiert haben. Der geheime Client Schlüssel muss vor dem Senden URL-codiert sein.| 
|grant_type|Erforderlich|Muss auf `client_credentials`festgelegt werden.|

### <a name="second-case-access-token-request-with-a-certificate"></a>Zweiter Fall: zugriffstokenanforderung mit einem Zertifikat 

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

|Parameter|Erforderlich/optional|Beschreibung| 
|-----|-----|-----|
|client_assertion_type|Erforderlich|Der Wert muss auf urn: IETF: biams: OAuth: Client-Assert-Type: JWT-Träger festgelegt werden.| 
|client_assertion|Erforderlich|Eine-Bestätigung (ein JSON-webtoken), die Sie erstellen und mit dem Zertifikat signieren müssen, das Sie als Anmelde Informationen für Ihre Anwendung registriert haben.|  
|grant_type|Erforderlich|Muss auf `client_credentials`festgelegt werden.|
|client_id|Optional|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS. Dies ist ein Teil client_assertion, daher muss er hier nicht übermittelt werden.| 
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen, denen der Benutzer zustimmen soll.| 

### <a name="use-a-token"></a>Token verwenden 
 
Nachdem Sie ein Token abgerufen haben, können Sie das Token verwenden, um Anforderungen an die Ressource zu senden. Wenn das Token abläuft, wiederholen Sie die Anforderung an den/Token-Endpunkt, um ein neues Zugriffs Token abzurufen.  
 
```
GET /v1.0/me/messages 
Host: https://webapi.com 
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...  
```

## <a name="resource-owner-password-credentials-grant-flow-not-recommended"></a>Datenfluss für Kenn Wort Anmelde Informationen für Ressourcen Besitzer (nicht empfohlen) 
 
Mithilfe der Berechtigung für den Ressourcen Besitzer Kennwort-Anmelde Informationsdienst (ropc) kann eine Anwendung den Benutzer anmelden, indem er sein Kennwort direkt verarbeitet. Der ropc-Flow erfordert ein hohes Maß an Vertrauenswürdigkeit und Benutzer Präsenz, und Sie sollten diesen Flow nur verwenden, wenn andere, sicherere, Flows nicht verwendet werden können.  
 
### <a name="protocol-diagram"></a>Protokoll Diagramm 
 
Das folgende Diagramm zeigt den ropc-Flow.

![Ropc-Flow](media/adfs-scenarios-for-developers/resource.png)

### <a name="authorization-request"></a>Autorisierungs Anforderung 
Der ropc-Flow ist eine einzelne Anforderung – er sendet die Client Identifikation und die Anmelde Informationen des Benutzers an den IDP und empfängt dann Token in der Rückgabe. Der Client muss die e-Mail-Adresse (UPN) und das Kennwort des Benutzers anfordern, bevor Sie dies tun. Unmittelbar nach einer erfolgreichen Anforderung sollte der Client die Anmelde Informationen des Benutzers sicher aus dem Arbeitsspeicher freigeben. Sie darf Sie niemals speichern.  

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


|Parameter|Erforderlich/optional|Beschreibung| 
|-----|-----|-----|
|client_id|Erforderlich|Client-ID| 
|grant_type|Erforderlich|Muss auf "Password" festgelegt werden.| 
|Benutzername|Erforderlich|Dies ist die E-Mail-Adresse des Benutzers.| 
|Kennwort|Erforderlich|Das Kennwort des Benutzers.| 
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|

### <a name="successful-authentication-response"></a>Erfolgreiche Authentifizierungs Antwort 
Das folgende Beispiel zeigt eine erfolgreiche tokenantwort: 

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


|Parameter|Beschreibung| 
|-----|-----|
|token_type|Immer auf bearerwert festgelegt.| 
|scope|Wenn ein Zugriffs Token zurückgegeben wurde, listet dieser Parameter die Bereiche auf, für die das Zugriffs Token gültig ist.| 
|expires_in|Die Anzahl der Sekunden, für die das enthaltene Zugriffs Token gültig ist.| 
|access_token|Wird für die angeforderten Bereiche ausgestellt.| 
|id_token|Eine JSON Web Token (JWT). Die APP kann die Segmente dieses Tokens decodieren, um Informationen über den angemeldeten Benutzer anzufordern. Die APP kann die Werte Zwischenspeichern und anzeigen, aber Sie sollte für Autorisierungs-oder Sicherheitsgrenzen nicht darauf basieren.| 
|refresh_token_expires_in|Die Anzahl der Sekunden, für die das enthaltene Aktualisierungs Token gültig ist.| 
|refresh_token|Wird ausgegeben, wenn der ursprüngliche Bereichs Parameter offline_access enthalten ist.|

Sie können das Aktualisierungs Token verwenden, um neue Zugriffs Token und Aktualisierungs Token zu erhalten. verwenden Sie dazu denselben Fluss, der im obigen Abschnitt zum Autorisierungs Code Grant beschrieben wird.   

## <a name="device-code-flow"></a>Geräte Code Fluss 
 
Geräte Code Gewährung ermöglicht es Benutzern, sich bei Geräten anzumelden, die auf die Eingabe beschränkt sind, z. b. ein smartTV, ein IOT-Gerät oder ein Drucker Zum Aktivieren dieses Flows kann der Benutzer auf dem Gerät eine Webseite auf einem anderen Gerät auf einem anderen Gerät besuchen, um sich anzumelden. Sobald sich der Benutzer anmeldet, kann das Gerät bei Bedarf Zugriffs Token und Aktualisierungs Token abrufen. 
 
### <a name="protocol-diagram"></a>Protokoll Diagramm 
 
Der gesamte Geräte Code Fluss ähnelt dem nächsten Diagramm. Wir beschreiben jeden der Schritte weiter unten in diesem Artikel. 
 
![Geräte Code Fluss](media/adfs-scenarios-for-developers/device.png)

### <a name="device-authorization-request"></a>Geräte Autorisierungs Anforderung 
Der Client muss zuerst eine Überprüfung des Authentifizierungs Servers für ein Gerät und einen Benutzercode durchsuchen, der zum Initiieren der Authentifizierung verwendet wird. Der Client sammelt diese Anforderung vom/devicecode-Endpunkt. In dieser Anforderung sollte der Client auch die Berechtigungen einschließen, die er vom Benutzer abrufen muss. Ab dem Zeitpunkt, an dem diese Anforderung gesendet wird, hat sich der Benutzer nur 15 Minuten Zeit, sich anzumelden (der übliche Wert für expires_in). Daher sollten Sie diese Anforderung nur dann vornehmen, wenn der Benutzer angegeben hat, dass er für die Anmeldung bereit ist. 

```
// Line breaks are for legibility only. 
 
POST https://adfs.contoso.com/adfs/oauth2/devicecode 
Content-Type: application/x-www-form-urlencoded 
 
client_id=6731de76-14a6-49ae-97bc-6eba6914391e 
scope=openid 
```


|Parameter|Bedingung|Beschreibung|
|-----|-----|-----| 
|client_id|Erforderlich|Die Anwendungs-ID (Client-ID), die der der APP zugewiesen AD FS.| 
|scope|Optional|Eine durch Leerzeichen getrennte Liste von Bereichen.|

### <a name="device-authorization-response"></a>Geräte Autorisierungs Antwort 
Eine erfolgreiche Antwort ist ein JSON-Objekt, das die erforderlichen Informationen enthält, damit sich der Benutzer anmelden kann. 


|Parameter|Beschreibung|
|-----|-----| 
|device_code|Eine lange Zeichenfolge, mit der die Sitzung zwischen dem Client und dem autorisierungsserver überprüft wird. Der Client verwendet diesen Parameter, um das Zugriffs Token vom autorisierungsserver anzufordern.| 
|user_code|Eine kurze Zeichenfolge, die dem Benutzer angezeigt wird, der zum Identifizieren der Sitzung auf einem sekundären Gerät verwendet wird.| 
|verification_uri|Der URI, an den der Benutzer mit dem user_code gelangen soll, um sich anzumelden.| 
|verification_uri_complete|Der URI, an den der Benutzer mit dem user_code gelangen soll, um sich anzumelden. Dies ist bereits mit user_code gefüllt, sodass der Benutzer keine Eingabe user_code| 
|expires_in|Die Anzahl der Sekunden, bevor die device_code und user_code ablaufen.| 
|Tri|Die Anzahl der Sekunden, die der Client zwischen Abruf Anforderungen warten soll.| 
|Nachricht|Eine lesbare Zeichenfolge mit Anweisungen für den Benutzer. Dies kann lokalisiert werden, indem Sie einen Abfrage Parameter in die Anforderung des Formulars einschließen? mkt = xx-xx und den entsprechenden Sprachkultur Code ausfüllen.  

### <a name="authenticating-the-user"></a>Authentifizieren des Benutzers 
Nach dem Empfang der user_code und verification_uri werden diese vom Client für den Benutzer angezeigt, und Sie werden angewiesen, sich mit Ihrem Mobiltelefon oder PC-Browser anzumelden. Außerdem kann der Client einen QR-Code oder einen ähnlichen Mechanismus verwenden, um die verfication_uri_complete anzuzeigen, die den Schritt der Eingabe der user_code für den Benutzer übernimmt. Während der Benutzer sich beim verification_uri authentifiziert, muss der Client den/Token-Endpunkt für das angeforderte Token mithilfe der device_code abrufen. 

```
POST https://adfs.contoso.com /adfs/oauth2/token 
Content-Type: application/x-www-form-urlencoded 
 
grant_type: urn:ietf:params:oauth:grant-type:device_code 
client_id: 6731de76-14a6-49ae-97bc-6eba6914391e 
device_code: GMMhmHCXhWEzkobqIHGG_EnNYYsAkukHspeYUk9E8 
```


|Parameter|Erforderlich|Beschreibung|
|-----|-----|-----| 
|grant_type|Erforderlich|Muss "urn: IETF: parameams: OAuth: Grant-Type: device_code| 
|client_id|Erforderlich|Muss mit der in der ursprünglichen Anforderung verwendeten client_id identisch sein.| 
|code|Erforderlich|Die device_code, die in der Geräte Autorisierungs Anforderung zurückgegeben wird.|

### <a name="successful-authentication-response"></a>Erfolgreiche Authentifizierungs Antwort 
Eine erfolgreiche tokenantwort sieht wie folgt aus:  


|Parameter|Beschreibung|
|-----|-----| 
|token_type|Immer "Träger.| 
|scope|Wenn ein Zugriffs Token zurückgegeben wurde, werden die Bereiche aufgelistet, für die das Zugriffs Token gültig ist.| 
|expires_in|Anzahl von Sekunden, bevor das enthaltene Zugriffs Token für gültig ist.| 
|access_token|Wird für die angeforderten Bereiche ausgestellt.| 
|id_token|Wird ausgegeben, wenn der ursprüngliche Bereichs Parameter den OpenID-Bereich enthielt.| 
|refresh_token|Wird ausgegeben, wenn der ursprüngliche Bereichs Parameter offline_access enthalten ist.| 
|refresh_token_expires_in|Anzahl von Sekunden, bevor das enthaltene Aktualisierungs Token für gültig ist.| 


## <a name="related-content"></a>Verwandte Themen  
Eine umfassende Liste mit exemplarischen Vorgehensweisen finden Sie unter [AD FS Entwicklung](../AD-FS-Development.md) . darin finden Sie schrittweise Anleitungen zur Verwendung der zugehörigen Flows. 
