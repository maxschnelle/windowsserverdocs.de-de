---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: AD FS-Szenarien für Entwickler
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb1bc5776ea4d24f274c79563d9e346b104de6d9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444221"
---
# <a name="ad-fs-scenarios-for-developers"></a>AD FS-Szenarien für Entwickler


AD FS unter Windows Server 2016 [AD FS 2016] können Sie hinzufügen Industry standard OpenID Connect und OAuth 2.0-basierte Authentifizierung und Autorisierung für Anwendungen, die Sie entwickeln, und diese Anwendungen direkt in AD FS authentifizieren.    
  
AD FS 2016 unterstützt auch die WS-Verbund, WS-Trust, und die SAML-Protokolle und Profile, wir haben in früheren Versionen unterstützt.  Wenn Sie die Anleitung für Entwickler für diesen Protokollen interessiert sind, finden Sie unter diesem Artikel.  In diesem Artikel liegt der Schwerpunkt auf und aus dem neueren Protokoll Support profitieren.  
  
## <a name="why-modern-authentication"></a>Warum moderner Authentifizierung  
Während Sie mit AD FS für die Anmeldung unter mit dem WS-Verbund-fortsetzen zu können, haben WS-Trust und SAML-Protokolle, wie Sie vor, mit der neueren Protokolle, Bereich erhalten Sie die folgenden Vorteile:  
  
* **Einfachheit und Konsistenz**  
    * Verwenden Sie den gleichen Satz von APIs und Muster, um anmelden zu aktivieren, für die:   
        *   mehrere Typen von Anwendungen ("Server", "Desktop", "Mobile", "Browser")  
        *   mehrere Plattformen (android, iOS, Windows)  
        *   Anwendungen innerhalb des Unternehmensnetzwerks oder in der Cloud gehostet werden  
    * Verwenden Sie den gleichen Satz von Bibliotheken, die Sie bereits, zum Authentifizieren von Benutzern für Azure AD verwenden können  
* **Flexibilität**  
    * Aktivieren Sie neben der Autorisierung für Standardbenutzer z. B. komplexere Szenarien:      
        * ? 3 Abschnitten anmelden Flows, die in denen sich ein Benutzer autorisiert, eine Webanwendung oder Dienst, den Zugriff auf Ressourcen, die mit einer anderen Web-app oder -Dienst befinden.    
        * ? Server-zu-Server-Flows, die in denen ein Mid-Tier-Dienst ein Back-End-API zugreift  
        * ? JavaScript-basierte Single-Page-Anwendungen (SPA)  
* **Branchenweite Unterstützung**  
    * OAuth 2.0 und OpenID Connect profitieren große Auslastung in der Branche, sodass Kenntnisse dieser Muster Sie die Authentifizierung und Autorisierung außerhalb einer Active Directory-Umgebung auch aktivieren können  
  
## <a name="how-it-works-the-basics"></a>So funktioniert es: Die Grundlagen  
Sie können die moderne Authentifizierung von AD FS für Ihre Anwendung mit den gleichen Satz von Tools und Bibliotheken, die Sie bereits, zum Authentifizieren von Benutzern für Azure AD verwenden können hinzufügen.   
  
In AD FS-Szenarien, es ist AD FS und nicht in Azure AD, die als die Identitätsanbieter und die Autorisierung fungiert Server.  Andernfalls die Konzepte sind identisch: Benutzer ihre Anmeldeinformationen bereitstellen und Abrufen von Token, entweder direkt oder über einen Vermittler, für den Zugriff auf Ressourcen.  
  
Das grundlegende Szenario besteht aus einer Benutzer- oder "Resource Owner", die Interaktion mit einem Browser auf eine Webanwendung zuzugreifen:  
  
![AD FS für Entwickler](media/ADFS_DEV_1.png)  
  
Die Webanwendung wird einen "Client" aufgerufen werden, da er die Anforderung an den autorisierungsserver (AD FS) für ein Zugriffstoken für die Ressource initiiert.  Die Ressource kann von der Web-app selbst gehostet werden oder als eine Web-API an einer beliebigen Stelle auf das Netzwerk oder das Internet zugänglich sein.   Der Benutzer oder "Besitzer der Ressource" Act autorisiert die Client-Web-app, um das Zugriffstoken zu erhalten, durch die Bereitstellung von Anmeldeinformationen für den autorisierungsserver.    
  
## <a name="how-it-works-components"></a>Funktionsweise: Komponenten  
OAuth 2.0 und OpenID Connect-Szenarien sind AD FS verwenden den gleichen Satz von Tools und Bibliotheken, die Sie verwenden, wenn es sich bei Azure AD des Identitätsanbieters erfolgt ist.  Diese Komponenten sind:  
* Active Directory-Authentifizierungsbibliothek (ADAL):-Clientbibliotheken erleichtern, die Sammeln von Benutzeranmeldeinformationen, erstellen und token-Anforderungen senden und Abrufen von den sich ergebenden Token.    
* OWIN (Open Web Interface für .NET)-Middleware: Obwohl OWIN basierten communityprojekt ist, hat Microsoft einen Satz von Bibliotheken der Seite, die erstellt für den Schutz von Webanwendungen und Web-APIs mit OpenID Connect und OAuth 2.0  
  
Die Rollen der diese Komponenten sind im folgenden Diagramm dargestellt:  
  
![AD FS für Entwickler](media/ADFS_DEV_2.png)  
  
## <a name="modeling-these-scenarios-in-ad-fs-2016"></a>Modellierung dieser Szenarien in AD FS 2016  
  
### <a name="application-groups"></a>Anwendungsgruppen  
Um dieser Szenarien für AD FS darzustellen, haben wir ein neues Konzept namens Anwendungsgruppen eingeführt.  Eine Anwendungsgruppe kann beliebiger Anzahl und die Kombination von der Anwendung die folgenden grundlegenden Typen enthalten:  
  
  
  
Anwendungsgruppe / Anwendungstyp  |Beschreibung  |Role-Eigenschaft    
---------|---------|---------  
Systemeigene Anwendung     |  Bezeichnet einen öffentlichen Client handelt, Dies dient eine Client-app sein, die ausgeführt wird, auf einem pc oder Gerät und mit denen der Benutzer interagiert.       | Anforderungen der Token vom autorisierungsserver (AD FS) für den Benutzerzugriff auf Ressourcen.  HTTP-Anforderungen auf geschützte Ressourcen, mit dem Token als HTTP-Header gesendet.        
Server-Anwendung     |   Eine Webanwendung, die auf einem Server ausgeführt und ist im Allgemeinen für Benutzer über einen Browser zugegriffen werden kann.  Da es kann einen eigenen Client "Secret" oder Anmeldeinformationen handelt, wird sie manchmal einen vertraulichen Client aufgerufen.      | Anforderungen der Token vom autorisierungsserver (AD FS) für den Benutzerzugriff auf Ressourcen.  HTTP-Anforderungen auf geschützte Ressourcen, mit dem Token als HTTP-Header gesendet.               
Web-API     |  Die End-Ressource der Benutzer greift auf. Stellen Sie sich diese als neue Darstellung des "vertrauende Seiten".| Nimmt Token, die von Clients abgerufen  
  
### <a name="differences-from-ad-fs-2012-r2"></a>Unterschiede zwischen AD FS 2012 R2  
Anwendungsgruppen kombinieren Trust- und -Autorisierung-Elemente, die AD FS 2012 R2 separat als vertrauende Seiten, Clients und Anwendungsberechtigungen verfügbar gemacht.  
  
In den folgenden Tabellen werden verglichen, die Methoden, die mit dem entsprechenden Anwendungsvertrauensstellungsobjekte in AD FS 2012 R2 und AD FS 2016 erstellt werden:  
  
AD FS in Windows Server 2012 R2|In PowerShell|AD FS-Verwaltung  
---------|---------|---------  
Native Client hinzufügen|Add-AdfsClient|Nicht verfügbar  
Fügen Sie Server-Anwendung als Client hinzu.|Add-AdfsClient|Nicht verfügbar  
Hinzufügen von Web-APIs / Ressourcen|Add-AdfsRelyingPartyTrust|Erstellen der Vertrauensstellung der vertrauenden Seite  
  
AD FS 2016|In PowerShell|AD FS-Verwaltung  
---------|---------|---------  
Native Client hinzufügen|Add-AdfsNativeClientApplication|Systemeigene Anwendung zu Anwendung-Gruppe hinzufügen  
Fügen Sie Server-Anwendung als Client hinzu.|Add-AdfsServerApplication|Servergruppe für die Anwendung zu Anwendung hinzufügen  
Hinzufügen von Web-APIs / Ressourcen|Add-AdfsWebApiApplication|Web-API-Anwendung zu Anwendung Gruppe hinzufügen  
  
### <a name="application-permissions-and-consent"></a>Anwendungsberechtigungen und Zustimmung  
Standardmäßig sind die Clients in einer Anwendungsgruppe den Zugriff auf die Ressourcen in der gleichen Gruppe zulässig.  Der Administrator keine Berechtigungen für bestimmte Anwendung zu konfigurieren.  Mit Anwendungsgruppen können auch Administratoren, die Bereiche, die zulässig sind, z. B. Openid oder "user_impersonation" anzugeben.  Geben Sie die folgenden szenariobeschreibungen genau die Bereiche für welches Szenario erforderlich sind.  
  
Da AD FS ein Modell der Zustimmung des Administrators verwendet werden, werden Benutzer beim Zugriff auf Ressourcen nicht zur Zustimmung aufgefordert.  Konfigurieren Sie die Anwendungsgruppe, stellt der Administrator in Kraft Zustimmung im Auftrag aller Anwendungsbenutzer bereit.  
  
## <a name="supported-scenarios"></a>Unterstützte Szenarien  
Der folgende Abschnitt beschreibt die Szenarien, die wir im Detail zu unterstützen.  
  
### <a name="tokens-used"></a>Token verwendet  
Diese Szenarien ist der drei Tokentypen verwenden:  
  
* **id_token:** Ein JWT-Token verwendet, um die Identität des Benutzers darstellen. Der Anspruch "Aud" oder die Zielgruppe des ID-Tokens entspricht die Client-ID der einheitlichen Modus oder Anwendung.  
* **access_token:** Ein JWT-Token verwendet, in Oauth und OpenID connect, Szenarien und von der Ressource verwendet werden soll.  Der Anspruch "Aud" oder die Zielgruppe des Tokens muss die ID der Ressource oder des Web-API übereinstimmen.  
* **refresh_token:** Dieses Token wird übermittelt, anstelle von Sammeln von Benutzeranmeldeinformationen, um einen einmaligen Erfahrung bereitzustellen.  Dieses Token wird sowohl ausgegeben und AD FS, genutzt und ist nicht von Clients oder Ressourcen gelesen werden.    
  
### <a name="native-client-to-web-api"></a>Native Client-Web-API  
Dieses Szenario ermöglicht es, dem Benutzer von einer nativen Clientanwendung zum Aufrufen einer Web-API von AD FS 2016 geschützt werden.  
* Die systemeigene Clientanwendung verwendet die ADAL zum Senden von Autorisierung und Token-Anforderungen an AD FS, Aufforderung zur Eingabe von Anmeldeinformationen des Benutzers nach Bedarf, und sendet dann das resultierende Token als HTTP-Header in der Anforderung an die Web-API  
* [Dieser Teil ist nur zu Demonstrationszwecken] Die Web-API liest die Ansprüche aus den "ClaimsPrincipal"-Objekt, das resultiert aus der das Zugriffstoken, die vom Client gesendet werden, und sendet diese an den Client zurück.  
  
![Beschreibung des protokollflusses](media/ADFS_DEV_3.png)  
  
1.  Die systemeigene Clientanwendung initiiert den Flow mit einem Aufruf der ADAL-Bibliothek.  Dies löst eine browserbasierte HTTP GET, um die AD FS authorize-Endpunkt:  
  
**Genehmigungsanfrage:**  
ERHALTEN <https://fs.contoso.com/adfs/oauth2/authorize?>  
  
Parameter|Wert  
---------|---------  
response_type|"Code"  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der nativen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der nativen Anwendung in der Anwendungsgruppe  
  
**Anforderung-autorisierungsantwort:**  
Wenn sich der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.    
AD FS reagiert, indem Sie einen Autorisierungscode als Parameter "Code" in der Abfragekomponente von der umleitungs-URI zurückgeben.  Zum Beispiel: HTTP/1.1 302 gefunden, Position:  **<http://redirect_uri:80/?code=&lt;code&gt>;.**  
  
2. Der native Client sendet dann den Code, zusammen mit den folgenden Parametern an die AD FS-token-Endpunkt:  
  
**Token anfordern:**  
POST https://fs.contoso.com/adfs/oauth2/token  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code" 
code|Autorisierungscode von 1  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der nativen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der nativen Anwendung in der Anwendungsgruppe  
  
**Token-Anforderung-Antwort:**  
AD FS reagiert mit HTTP 200 mit dem Zugriffstoken, Aktualisierungstoken und ID-Token im Text.  
  
3. Klicken Sie dann die systemeigene Anwendung sendet den Access_token-Teil der obigen Antwort als dem Autorisierungsheader in der HTTP-Anforderung an die Web-API.  
  
### <a name="single-sign-on-behavior"></a>SSO-Verhalten  
Nachfolgende Client fordert innerhalb 1 Stunde (standardmäßig) das Zugriffstoken weiterhin gültige im Cache, und eine neue Anforderung wird kein Datenverkehr an AD FS ausgelöst.  Das Zugriffstoken wird automatisch aus dem Cache von ADAL abgerufen werden.  
  
Nachdem das Zugriffstoken abgelaufen ist, sendet ADAL automatisch eine Refresh-token-Basis-Anforderung an die AD FS-token-Endpunkt (überspringen die autorisierungsanforderung automatisch).  
**Aktualisieren Sie die Anforderung eines Zugriffstokens:**  
POST https://fs.contoso.com/adfs/oauth2/token
   

Parameter|Wert|
---------|---------
grant_type|"refresh_token"|
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe|
client_id|Client-Id der nativen Anwendung in der Anwendungsgruppe
refresh_token|Das Aktualisierungstoken, das von AD FS als Reaktion auf die anfängliche tokenanforderung ausgestellten

  
  
**Aktualisieren Sie die token Anforderungsantwort:**  
Wenn das Aktualisierungstoken, das innerhalb von < SSO_period > ist, führt die Anforderung eines neuen Zugriffstokens. Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert.  Weitere Informationen zu SSO-Einstellungen finden Sie unter [AD FS Single Sign On Settings](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)  
  
Wenn das Aktualisierungstoken abgelaufen ist, führt die Anforderung ein HTTP 401 mit Fehler "Invalid_grant" und ""error_description "" "MSIS9615: Das Aktualisierungstoken, das im Aktualisierungstoken Parameter empfangen ist abgelaufen". In diesem Fall sendet ADAL automatisch eine neue autorisierungsanforderung an, die genau wie #1 oben aussieht.    
  
### <a name="web-browser-to-web-app"></a>Webbrowser zu Webanwendung   
In diesem Szenario muss ein Benutzer mit einem Browser den Zugriff auf Ressourcen, die von einer Webanwendung gehostet wird.    
Es gibt zwei Szenarien, die dies zu erreichen.  
  
#### <a name="oauth-confidential-client"></a>Vertraulicher OAuth-client  
Dieses Szenario ist ähnlich wie das oben, dass eine autorisierungsanforderung, gefolgt von einem Code für den tokenaustausch vorhanden ist.  Die Web-app (modelliert als Serveranwendung in AD FS) initiiert die autorisierungsanforderung über den Browser und tauscht den Code für das Token (durch die direkte Verbindung mit AD FS)  
  
![Beschreibung des protokollflusses](media/ADFS_DEV_4.png)  
  
1. Die Web-App initiiert eine autorisierungsanforderung, über den Browser, der eine HTTP GET-Anforderung für den AD FS sendet authorize-Endpunkt  
   **Autorisierungsanforderung**:  
   ERHALTEN <https://fs.contoso.com/adfs/oauth2/authorize?>  
  
Parameter|Wert  
---------|---------  
response_type|"Code"  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der nativen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der Web-app (Server-Anwendung) in der Anwendungsgruppe  
  
Anforderung-autorisierungsantwort:  
Wenn sich der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.  
AD FS reagiert, indem Sie einen Autorisierungscode z. B. als Parameter "Code" in der Abfragekomponente von der umleitungs-URI zurückgibt: HTTP/1.1 302 gefunden, Position: <https://webapp.contoso.com/?code=&lt;code&gt>;.  
  
2. Aufgrund der oben genannten 302 initiiert der Browser HTTP GET für die Web-app, z. B.: ERSTE <http://redirect_uri:80/?code=&lt;code&gt>;.   
  
3. An diesem Punkt initiiert die Web-app erhalten haben den Code, eine Anforderung an den AD FS-token-Endpunkt, senden die folgenden  
   **Token anfordern:**  
   POST https://fs.contoso.com/adfs/oauth2/token  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code"  
code|Autorisierungscode aus 2 oben  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der Web-app (Server-Anwendung) in der Anwendungsgruppe  
client_secret|Geheime Schlüssel der Web-app (Server-Anwendung) in der Anwendungsgruppe. **Hinweis: Anmeldeinformationen für den Client muss nicht "client_secret" werden.  AD FS unterstützt die Möglichkeit, Zertifikate oder die integrierte Windows-Authentifizierung verwenden.**  
  
**Token-Anforderung-Antwort:**  
AD FS reagiert mit HTTP 200 mit dem Zugriffstoken, Aktualisierungstoken und ID-Token im Text.  
Ansprüche  
4. Die Web-Anwendung, und klicken Sie dann entweder nutzt den Access_token-Teil der obigen Antwort (in dem Fall, in dem die Web-app selbst die Ressource hostet) oder auf andere sendet sie als den Authorization-Header in der HTTP-Anforderung an, an die Web-API.  
  
#### <a name="single-sign-on-behavior"></a>SSO-Verhalten  
Während das Zugriffstoken weiterhin gültig für eine Stunde (standardmäßig) in den Cache des Clients befinden, Sie denken möglicherweise, dass die zweite Anforderung funktioniert wie im obigen - native Clientszenario, dass eine neue Anforderung Datenverkehr an AD FS nicht ausgelöst wird, wie das Zugriffstoken automatisch abgerufen Sie aus dem Cache werden, von ADAL.  Allerdings ist es möglich, dass die Web-app unterschiedliche Autorisierungs- und tokenanforderungen; der erste Wert über unterschiedliche URL-Link, wie in unserem Beispiel senden kann.  
  
In diesem Fall ist es das AD FS-Browser-SSO-Cookie, das AD FS, um einen neuen Autorisierungscode ausgeben, ohne dass der Benutzer zur Eingabe von Anmeldeinformationen ermöglicht. Die Web-app ruft dann für AD FS, um den neuen Autorisierungscode gegen ein neues Zugriffstoken auszutauschen.  Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert.  
  
Andernfalls ist die Web-app intelligente ausreichend zu wissen, wenn der Benutzer bereits authentifiziert ist, der autorisierungsanforderung übersprungen werden kann und entweder:  
* des zwischengespeicherten Zugriffstokens, wenn nicht abgelaufen ist, abgerufen und verwendet wird, oder   
* eine Anforderung basierend-tokenanforderung kann an den AD FS-token-Endpunkt gesendet werden, wie unten beschrieben  
  
**Aktualisieren Sie die Anforderung eines Zugriffstokens:**  
POST https://fs.contoso.com/adfs/oauth2/token
   
Parameter|Wert  
---------|---------  
grant_type|"refresh_token"  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der Web-app (Server-Anwendung) in der Anwendungsgruppe  
refresh_token|Aktualisieren von AD FS als Reaktion auf die anfängliche tokenanforderung ausgestellten token  
client_secret|Geheimen Schlüssel der Web-app (Server-Anwendung) in der Anwendungsgruppe  
  
**Aktualisieren Sie die token Anforderungsantwort:**  
Wenn das Aktualisierungstoken, das innerhalb von < SSO_period > ist, führt die Anforderung eines neuen Zugriffstokens. Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert. Weitere Informationen zu SSO-Einstellungen finden Sie unter [AD FS Single Sign On Settings](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)   
  
Wenn das Aktualisierungstoken abgelaufen ist, führt die Anforderung ein HTTP 401 mit Fehler "Invalid_grant" und ""error_description "" "MSIS9615: Das Aktualisierungstoken, das im Aktualisierungstoken Parameter empfangen ist abgelaufen". In diesem Fall sendet ADAL automatisch eine neue autorisierungsanforderung an, die genau wie #1 oben aussieht.    
  
#### <a name="openid-connect-hybrid-flow"></a>OpenID Connect: Hybridflow  
Dieses Szenario ist ähnlich wie oben, gibt es eine autorisierungsanforderung durch die Web-app über den Browser umleiten und einen Code für den Austausch von der Web-app mit AD FS token initiiert wird.  Der Unterschied in diesem Szenario besteht darin, dass AD FS ein ID-Token als Teil der ersten Autorisierung Anforderung-Antwort gibt.  
  
![Beschreibung des protokollflusses](media/ADFS_DEV_5.png)  
  
1.  Die Web-App initiiert eine autorisierungsanforderung, über den Browser, der eine HTTP GET-Anforderung für den AD FS sendet authorize-Endpunkt  
  
**Genehmigungsanfrage:**  
ERHALTEN <https://fs.contoso.com/adfs/oauth2/authorize?>  
  
Parameter|Wert  
---------|---------  
response_type|"code+id_token"  
response_mode|"form_post"  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der Web-app (Server-Anwendung) in der Anwendungsgruppe  
  
**Anforderung-autorisierungsantwort:**  
Wenn sich der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.  
AD FS antwortet mit einer HTTP 200 und das Formular mit den unten als ausgeblendete Elemente:  
* Code: des Autorisierungscodes  
* "id_token": ein JWT-Token mit Ansprüchen, beschreibt die Benutzerauthentifizierung  
* Das Formular sendet automatisch auf der umleitungs-URI der Web-app, den Code und das ID-Token an die Web-app senden.  
  
3. An diesem Punkt initiiert die Web-app erhalten haben den Code, eine Anforderung an den AD FS-token-Endpunkt, senden die folgenden  
  
**Token anfordern:**  
POST https://fs.contoso.com/adfs/oauth2/token
  
  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code"  
code|Autorisierungscode oben  
Ressource|RP-ID (ID) der Web-API in der Anwendungsgruppe  
client_id|Client-Id der Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleitungs-URI der Web-app (Server-Anwendung) in der Anwendungsgruppe  
client_secret|Geheimen Schlüssel der Web-app (Server-Anwendung) in der Anwendungsgruppe  
  
**Token-Anforderung-Antwort:**  
AD FS reagiert mit HTTP 200 mit dem Zugriffstoken, Aktualisierungstoken und ID-Token im Text.  
  
4. Die Web-Anwendung, und klicken Sie dann entweder nutzt den Access_token-Teil der obigen Antwort (in dem Fall, in dem die Web-app selbst die Ressource hostet) oder auf andere sendet sie als den Authorization-Header in der HTTP-Anforderung an, an die Web-API.  
  
#### <a name="single-sign-on-behavior"></a>SSO-Verhalten  
Der SSO-Verhalten entspricht derjenigen der obige Ablauf der Oauth 2.0 vertraulicher Client.  
  
### <a name="on-behalf-of"></a>Im Auftrag von  
In diesem Szenario verwendet eine Web-app das ursprüngliche Zugriffstoken von einem Benutzer anfordern, und rufen Sie ein neues Zugriffstoken für eine andere Web-API, die die Web-app klicken Sie dann als Endbenutzer zugreifen.  Dies ist einen Fluss "im Auftrag von" bezeichnet.  
  
![Beschreibung des protokollflusses](media/ADFS_DEV_6.png)  
  
Schritt 1 und 2 funktionieren genau wie die Schritte 3 und 4 im vorherigen Datenfluss.  
In Schritt 3 ist die wichtigste Anforderung, dass der Parameter für "client_id", die Client-ID der Web-app 2, die RP-ID der Web-API a entsprechen muss  Das heißt, muss die Zielgruppe des Zugriffstokens, die für das neue Token ausgetauscht werden, die Client-ID der Entität, die das neue Token anfordert übereinstimmen.  

## <a name="related-content"></a>Verwandte Themen  
Finden Sie unter [AD FS-Entwicklung](../AD-FS-Development.md) für die vollständige Liste von Artikeln mit exemplarischen, enthalten die schrittweise Anleitungen zur Verwendung der dazugehörige Flows. 
