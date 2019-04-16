---
ms.assetid: 8a64545b-16bd-4c13-a664-cdf4c6ff6ea0
title: "AD FS-Szenarien für Entwickler"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 753b2b235cb1d73ab47588f8f229410c1f81db40
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-scenarios-for-developers"></a>AD FS-Szenarien für Entwickler

>Gilt für: Windows Server 2016

AD FS unter Windows Server 2016 [AD FS 2016] können Sie hinzufügen Industry standard OpenID Connect und OAuth 2.0-basierte Authentifizierung und Autorisierung für Anwendungen, die Sie entwickeln und diese Anwendungen, die Benutzer direkt mit AD FS zu authentifizieren.    
  
AD FS 2016 unterstützt auch das WS-Federation, WS-Trust und SAML Protokolle und -Profilen, wir haben in früheren Versionen unterstützt.  Wenn Sie für diese Protokolle Entwicklerleitfaden interessiert sind, finden Sie im Artikel hier.  In diesem Artikel geht verwenden, und profitieren Sie von der Unterstützung für neuere Protokolle.  
  
## <a name="why-modern-authentication"></a>Warum moderne Authentifizierung  
Können Sie zwar weiterhin mit AD FS für die Anmeldung auf WS-Federation, verfügen Sie über WS-Trust und SAML-Protokolle wie, bevor mit der neueren Protokollen Bereich Sie die folgenden Vorteile erhalten:  
  
* **Einfachheit und Konsistenz**  
    * Verwenden Sie den gleichen Satz von APIs und Muster, um anmelden für zu aktivieren:   
        *   mehrere Typen von Anwendungen (Server, Desktop, Mobile, Browser)  
        *   mehrere Plattformen (android, iOS, Windows)  
        *   Anwendungen innerhalb des Unternehmensnetzwerks oder in der Cloud gehostet  
    * Verwenden Sie den gleichen Satz von Bibliotheken, die Sie bereits zum Authentifizieren von Benutzern bei Azure AD verwenden können  
* **Flexibilität**  
    * Aktivieren Sie zusätzlich zur Autorisierung Standardbenutzern z. B. komplexere Szenarien:      
        * ? 3-Abschnitten anmelden Flüsse, die in denen ein Benutzer autorisiert, einer Web-Anwendung oder einem Dienst auf Ressourcen zugreifen, die mit einem anderen Web-app oder Dienst befinden.    
        * ? Server-zu-Server-Flüsse, die in denen Mid-Tier-Dienst ein Back-End-API-zugreift  
        * ? JavaScript-basierte Einzelseiten-Anwendungen (SPA)  
* **Unterstützung**  
    * OAuth 2.0 und OpenID Connect genießen Breite Auslastung gesamten Branche zusammen, damit Kenntnisse in dieser Muster eine Authentifizierung und Autorisierung außerhalb einer Active Directory-Umgebung unterstützen  
  
## <a name="how-it-works-the-basics"></a>Funktionsweise: Grundlagen  
Sie können moderne AD FS-Authentifizierung hinzufügen, der Anwendung mit den gleichen Satz von Tools und Bibliotheken, die Sie bereits zum Authentifizieren von Benutzern bei Azure AD verwenden können.   
  
In AD FS-Szenarien, ist es AD FS und kein Azure AD, der als Identitätsanbieter herzustellen und Autorisierung dient Server.  Andernfalls die Konzepte sind identisch: Benutzer ihre Anmeldeinformationen eingeben und Abrufen von Token, entweder direkt oder über ein Vermittler, für den Zugriff auf Ressourcen.  
  
Das einfachste Szenario besteht aus einem Benutzer oder "Ressourcenbesitzer", die Interaktion mit einem Browser, um eine Webanwendung zugreifen:  
  
![AD FS für Entwickler](media/ADFS_DEV_1.png)  
  
Die Web-Anwendung wird ein "Client" aufgerufen, da es die Anforderung an die autorisierungsserver (AD FS) für ein Zugriffstoken mit der Ressource initiiert.  Die Ressource kann von der Web-app selbst gehostet werden oder kann als Web-API-Netzwerk oder Internet zugegriffen werden.   Der Benutzer oder der "Besitzer der Ressource" wird die Client-Web-app das Zugriffstoken zu erhalten, durch die Bereitstellung von Anmeldeinformationen an den autorisierungsserver autorisiert.    
  
## <a name="how-it-works-components"></a>Funktionsweise: Komponenten  
OAuth 2.0 und OpenID Connect Szenarien in AD FS-Hersteller verwenden den gleichen Satz von Tools und Bibliotheken, die Sie verwenden, wenn es sich bei Azure AD der Identitätsanbieter ist.  Diese Komponenten sind:  
* Active Directory-Authentifizierung Library (ADAL): Client-Bibliotheken erleichtern, die Anmeldeinformationen des Benutzers sammeln, erstellen und übermitteln token anfordert und die resultierenden Token abrufen.    
* OWIN (Open Web Interface for .NET) Middleware: während OWIN ist ein communityprojekt basierend, Microsoft hat eine Reihe von Server Seite Bibliotheken, die für den Schutz von Webanwendungen und web-APIs mit OpenID Connect und OAuth 2.0  
  
Die Funktionen der folgenden Komponenten sind im folgenden Diagramm dargestellt:  
  
![AD FS für Entwickler](media/ADFS_DEV_2.png)  
  
## <a name="modeling-these-scenarios-in-ad-fs-2016"></a>Erstellen von diesen Szenarien in AD FS 2016  
  
### <a name="application-groups"></a>Anwendungsgruppen  
Um diese Szenarien in AD FS-Richtlinie darzustellen, haben wir ein neues Konzept namens Anwendungsgruppen eingeführt.  Eine Anwendungsgruppe kann eine beliebige Anzahl und Kombination der folgenden grundlegenden Typen der Anwendung enthalten:  
  
  
  
Anwendungsgruppe / Anwendung geben  |Beschreibung  |Rolle    
---------|---------|---------  
Systemeigene Anwendung     |  In einigen Fällen einen öffentlichen Client aufgerufen wird, ist dies soll eine Client-app, die auf einem pc oder Gerät und mit dem der Benutzer interagiert ausgeführt wird.       | Anforderungen Token vom autorisierungsserver (AD FS) für den Benutzerzugriff auf Ressourcen.  Sendet HTTP-Anforderungen auf geschützte Ressourcen, die das Token als HTTP-Header verwenden.        
Server-Anwendung     |   Eine Anwendung, die auf einem Server ausgeführt wird und in der Regel für Benutzer über einen Browser zugänglich ist.  Da es einen eigenen geheimen' ' oder Anmeldeinformationen verwalten kann, wird sie manchmal einen vertraulichen Client aufgerufen.      | Anforderungen Token vom autorisierungsserver (AD FS) für den Benutzerzugriff auf Ressourcen.  Sendet HTTP-Anforderungen auf geschützte Ressourcen, die das Token als HTTP-Header verwenden.               
Web-API     |  Der End-Ressourcen der Benutzer greift auf. Betrachten Sie diese als neue Darstellung von "vertrauende Seiten".| Nimmt Token abgerufen, indem clients  
  
### <a name="differences-from-ad-fs-2012-r2"></a>Unterschiede von AD FS 2012 R2  
Anwendungsgruppen kombinieren, als vertrauenswürdig einstufen und Autorisierung-Elemente, die AD FS 2012 R2 separat als vertrauende Seiten, Clients und Berechtigungen zur Verfügung gestellt.  
  
In den folgenden Tabellen werden die Methoden, mit der entsprechenden Anwendung Vertrauensstellung Objekte in AD FS 2012 R2 Vs AD FS 2016 erstellt wurden, verglichen:  
  
AD FS unter Windows Server 2012 R2|In PowerShell|AD FS-Verwaltung  
---------|---------|---------  
Native Client hinzufügen|Hinzufügen AdfsClient|NA  
Server-Anwendung als Client hinzu.|Hinzufügen AdfsClient|NA  
Hinzufügen von Web-API / Ressource|Hinzufügen AdfsRelyingPartyTrust|Erstellen Sie die Vertrauensstellung der vertrauenden Seite  
  
AD FS 2016|In PowerShell|AD FS-Verwaltung  
---------|---------|---------  
Native Client hinzufügen|Hinzufügen AdfsNativeClientApplication|Systemeigene Anwendung Gruppe hinzufügen  
Server-Anwendung als Client hinzu.|Hinzufügen AdfsServerApplication|Anwendung Servergruppe hinzufügen  
Hinzufügen von Web-API / Ressource|Hinzufügen AdfsWebApiApplication|Web-API-Anwendung Gruppe hinzufügen  
  
### <a name="application-permissions-and-consent"></a>Berechtigungen und die Zustimmung  
Standardmäßig sind die Clients in einer Anwendungsgruppe zulässig, Zugriff auf die Ressourcen in der gleichen Gruppe.  Der Administrator hat keinen bestimmten Berechtigungen zu konfigurieren.  Anwendungsgruppen ermöglichen Administratoren die Bereiche, die zulässig sind, z. B. Openid oder User_impersonation angeben.  Die folgenden szenariobeschreibungen angeben, genau welche Bereiche für die einzelnen Szenarien erforderlich sind.  
  
Da AD FS ein Modell der Administrator Zustimmung verwendet werden, sind Benutzer nicht zur Bestätigung aufgefordert, den Zugriff auf Ressourcen.  Konfigurieren Sie die Anwendungsgruppe, ermöglicht es dem Systemadministrator in Kraft Zustimmung für alle Anwendungsbenutzer.  
  
## <a name="supported-scenarios"></a>Unterstützte Szenarien  
Im folgenden Abschnitt werden die Szenarien, die wir noch ausführlicher unterstützen.  
  
### <a name="tokens-used"></a>Token verwendet  
Stellen Sie diese Szenarien von drei token verwenden:  
  
* **Id_token:** ein JWT-Token verwendet, um die Identität des Benutzers darzustellen. Der Anspruch 'Aud' oder Zielgruppe von der Id_token entspricht die Client-ID der Anwendung systemeigen oder Server.  
* **Access_token:** ein JWT-Token verwendet Oauth und OpenID connect-Szenarien und beabsichtigen, die von der Ressource genutzt werden.  Der Anspruch 'Aud' oder Zielgruppe dieses Token muss den Bezeichner der Ressource oder Web-API übereinstimmen.  
* **Refresh_token:** dieses Token wird übermittelt, anstatt das Sammeln von Benutzeranmeldeinformationen um ein einmaliges Anmelden Erfahrung zu bieten.  Dieses Token ist sowohl ausgestellt und von AD FS, verbraucht und kann nicht von Clients oder Ressourcen gelesen.    
  
### <a name="native-client-to-web-api"></a>Native Client Web-API  
Dieses Szenario kann der Benutzer eine systemeigene Clientanwendung eine AD FS 2016 geschützte Web-API aufrufen.  
* Die systemeigene Clientanwendung verwendet ADAL Autorisierung senden und Token Anforderungen für AD FS, Aufforderung zur Eingabe von Anmeldeinformationen des Benutzers nach Bedarf, und klicken Sie dann sendet das resultierende Token als einen HTTP-Header auf die Anforderung an die Web-API  
* [Dieser Teil dient nur zu Demonstrationszwecken] Die Web-API liest die Ansprüche aus dem ClaimsPrincipal-Objekt, das das Zugriffstoken, die vom Client gesendeten Ergebnisse und sendet sie an den Client zurück.  
  
![Beschreibung des Protokolls Fluss](media/ADFS_DEV_3.png)  
  
1.  Die systemeigene Clientanwendung initiiert den Ablauf mit einem Aufruf der ADAL-Bibliothek.  Dies führt dazu, eine browserbasierte HTTP GET, um die AD FS Endpunkt autorisieren:  
  
**Autorisierungsanforderung:**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
Parameter|Wert  
---------|---------  
response_type|"Code"  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id der einheitlichen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleiten von einheitlichen Anwendung in Anwendungsgruppe URI  
  
**Die Antwort auf Autorisierung:**  
Wenn der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.    
AD FS reagiert, indem Sie einen Autorisierungscode als Parameter "Code" in der Abfragekomponente von den Redirect_uri zurückgeben.  Beispiel: HTTP/1.1 302 gefundenen Ort: **Http://redirect_uri:80 /? Code =&lt;Code&gt;.**  
  
2.  Der native Client sendet dann den Code mit den folgenden Parametern, zum Endpunkt AD FS-token:  
  
**Tokenanforderung:**  
POST https://fs.contoso.com/adfs/oauth2/Token  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code" 
Code|Autorisierungscode von 1  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id der einheitlichen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleiten von einheitlichen Anwendung in Anwendungsgruppe URI  
  
**Tokenanforderung Antwort:**  
AD FS antwortet mit einer HTTP-200 mit Access_token, Refresh_token und Id_token im Textkörper.  
  
3.  Klicken Sie dann auf die ursprüngliche Anwendung sendet die Access_token Teil der oben genannten Antwort als Autorisierungsheader in der HTTP-Anforderung an die Web-API.  
  
### <a name="single-sign-on-behavior"></a>Das Verhalten für einmaliges Anmelden  
Nachfolgende Clientanforderungen innerhalb von 1 Stunde (standardmäßig) die Access_token weiterhin gültig im Cache, und eine neue Anforderung, Datenverkehr zu AD FS wird nicht ausgelöst.  Die Access_token wird von ADAL automatisch aus dem Cache abgerufen werden.  
  
Nachdem das Zugriffstoken abgelaufen ist, sendet ADAL automatisch eine Aktualisierung token Basis-Anforderung an den Endpunkt der AD FS-token (die autorisierungsanforderung automatisch überspringen).  
**Aktualisieren Sie tokenanforderung:**  
POST https://fs.contoso.com/adfs/oauth2/Token
   

Parameter|Wert|
---------|---------
grant_type|"Refresh_token"|
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe|
client_id|Client-Id der einheitlichen Anwendung in der Anwendungsgruppe
refresh_token|Das Aktualisierungstoken von AD FS in Reaktion auf die erste Anforderung token ausgestellt

  
  
**Aktualisieren Sie die Antwort auf token:**  
Wenn das Aktualisierungstoken innerhalb von < SSO_period > ist, führt die Anforderung ein neues Zugriffstoken. Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert.  Weitere Informationen zu SSO-Einstellungen finden Sie unter [AD FS einzelne Zeichen auf-Einstellungen](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)  
  
Wenn das Aktualisierungstoken abgelaufen ist, führt die Anforderung mit Fehler "Invalid_grant" und "Error_description" HTTP 401 "MSIS9615: das Aktualisierungstoken erhalten im Refresh_token-Parameter ist abgelaufen". In diesem Fall fordert die ADAL automatisch neue Autorisierung, die genau wie #1 oben aussieht.    
  
### <a name="web-browser-to-web-app"></a>Webbrowser, um Web-App   
In diesem Szenario muss ein Benutzer mit einem Browser Zugriff auf Ressourcen, die von einer Webanwendung gehostet werden.    
Es gibt zwei Szenarien, die dies zu erreichen.  
  
#### <a name="oauth-confidential-client"></a>Vertrauliche OAuth-client  
Dieses Szenario ähnelt der vorstehenden ergibt sich eine autorisierungsanforderung, gefolgt von einem Code für den tokenaustausch.  Die Web-app (modelliert als Server-Anwendung in AD FS) initiiert die autorisierungsanforderung über den Browser und tauscht den Code für das Token (durch die direkte Verbindung mit AD FS)  
  
![Beschreibung des Protokolls Fluss](media/ADFS_DEV_4.png)  
  
1.  Die Web-App initiiert eine Genehmigung anfordern, über den Browser, sendet eine HTTP GET an der AD FS autorisieren Endpunkt  
**Autorisierungsanforderung**:  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
Parameter|Wert  
---------|---------  
response_type|"Code"  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id der einheitlichen Anwendung in der Anwendungsgruppe  
redirect_uri|Umleiten der URI des Web-app (Server-Anwendung) in "Anwendungsserver"  
  
Die Antwort auf Autorisierung:  
Wenn der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.  
AD FS reagiert, indem Sie einen Autorisierungscode z. B. als "Code"-Parameter in der Abfragekomponente von den Redirect_uri zurückgeben: HTTP/1.1 302 gefundenen Ort: https://webapp.contoso.com/?code=&lt;Code&gt;.  
  
2.  Aufgrund der oben genannten 302 Browser initiiert eine HTTP GET an die Web-app, zum Beispiel: GET Http://redirect_uri:80 /? Code =&lt;Code&gt;.   
  
3.  An diesem Punkt wird eine Anforderung an den AD FS-token-Endpunkt, senden die folgenden initiiert die Web-app, die den Code erhalten haben  
**Tokenanforderung:**  
POST https://fs.contoso.com/adfs/oauth2/Token  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code"  
Code|Autorisierungscode von 2 oben  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id für die Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleiten der URI des Web-app (Server-Anwendung) in "Anwendungsserver"  
client_secret|Die geheimen Schlüssel der Web-App (Server-Anwendung) in der Anwendungsgruppe. **Hinweis: Die Client-Anmeldeinformationen muss kein Client_secret werden.  AD FS unterstützt die Möglichkeit, Zertifikate oder integrierte Windows-Authentifizierung verwenden.**  
  
**Tokenanforderung Antwort:**  
AD FS antwortet mit einer HTTP-200 mit Access_token, Refresh_token und Id_token im Textkörper.  
Ansprüche  
4.  Die Web-Anwendung, und klicken Sie dann entweder die Access_token Teil der oben genannten Antwort (in der Fall, in dem die Web-app selbst die Ressource hostet) verwendet oder auf andere Weise sendet er als Autorisierungsheader in der HTTP-Anforderung an die Web-API.  
  
#### <a name="single-sign-on-behavior"></a>Das Verhalten für einmaliges Anmelden  
Während das Zugriffstoken noch gültig für 1 Stunde (standardmäßig) im Cache des Clients enthalten sind, denken Sie vielleicht, dass die zweite Anforderung funktioniert wie in der oben genannten - native Client-Szenario, dass eine neue Anforderung sämtlicher Datenverkehr, der AD FS nicht ausgelöst wird, wie das Zugriffstoken wird durch ADAL automatisch aus dem Cache abgerufen werden.  Es ist jedoch möglich, dass die Web-app kann unterschiedliche Autorisierung und tokenanforderungen sendet, die erste über eindeutige URL verknüpfen, wie Sie in unserem Beispiel.  
  
In diesem Fall ist es das AD FS-Browser-SSO-Cookie, das AD FS einen neuen Autorisierungscode ausgestellt werden, ohne dass der Benutzer zur Eingabe von Anmeldeinformationen ermöglicht. Die Web-app ruft dann zu AD FS zum Austausch von des neuen Autorisierungscodes für ein neues Zugriffstoken.  Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert.  
  
Andernfalls ist die Web-app smart genug, um zu wissen, wenn der Benutzer bereits authentifiziert ist, die zum Autorisieren Anforderung übersprungen werden kann und entweder:  
* das zwischengespeicherte Zugriffstoken, wenn nicht abgelaufen ist, abgerufen und verwendet wird, oder   
* eine Anforderung token Basis-Anforderung kann der AD FS-token-Endpunkt, gesendet werden, wie unten beschrieben  
  
**Aktualisieren Sie tokenanforderung:**  
POST https://fs.contoso.com/adfs/oauth2/Token
   
Parameter|Wert  
---------|---------  
grant_type|"Refresh_token"  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id für die Web-app (Server-Anwendung) in der Anwendungsgruppe  
refresh_token|Aktualisieren von AD FS in Reaktion auf die erste token Anforderung ausgestellte token  
client_secret|Geheimen Schlüssel der Web-App (Server-Anwendung) in der Anwendungsgruppe  
  
**Aktualisieren Sie die Antwort auf token:**  
Wenn das Aktualisierungstoken innerhalb von < SSO_period > ist, führt die Anforderung ein neues Zugriffstoken. Der Benutzer wird nicht zur Eingabe von Anmeldeinformationen aufgefordert. Weitere Informationen zu SSO-Einstellungen finden Sie unter [AD FS einzelne Zeichen auf-Einstellungen](../../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)   
  
Wenn das Aktualisierungstoken abgelaufen ist, führt die Anforderung mit Fehler "Invalid_grant" und "Error_description" HTTP 401 "MSIS9615: das Aktualisierungstoken erhalten im Refresh_token-Parameter ist abgelaufen". In diesem Fall fordert die ADAL automatisch neue Autorisierung, die genau wie #1 oben aussieht.    
  
#### <a name="openid-connect-hybrid-flow"></a>OpenID Connect: Hybrid-Fluss  
Dieses Szenario ist ähnlich wie die oben genannten, gibt es eine autorisierungsanforderung durch die Web-app über den Browser-Umleitung sowie einen Code token Exchange über die Web-app für den AD FS initiiert wird.  Der Unterschied in diesem Szenario besteht darin, dass AD FS ein Id_token als Teil der Antwort auf die erste Anforderung ausstellt.  
  
![Beschreibung des Protokolls Fluss](media/ADFS_DEV_5.png)  
  
1.  Die Web-App initiiert eine Genehmigung anfordern, über den Browser, sendet eine HTTP GET an der AD FS autorisieren Endpunkt  
  
**Autorisierungsanforderung:**  
GET https://fs.contoso.com/adfs/oauth2/authorize?  
  
Parameter|Wert  
---------|---------  
response_type|"Code + Id_token"  
response_mode|"Form_post"  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id für die Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleiten der URI des Web-app (Server-Anwendung) in der Anwendungsgruppe  
  
**Die Antwort auf Autorisierung:**  
Wenn der Benutzer nicht angemeldet hat, bevor der Benutzer zur Eingabe von Anmeldeinformationen aufgefordert wird.  
AD FS antwortet mit einem HTTP-200 und Formular mit den unten als ausgeblendete Elemente:  
* Code: den Autorisierungscode  
* Id_token: ein JWT-Token mit Ansprüchen beschreiben die Benutzerauthentifizierung  
2.  Das Formular wird automatisch an den Redirect_uri Web-App, die den Code und die Id_token an die Web-app senden.  
  
3.  An diesem Punkt wird eine Anforderung an den AD FS-token-Endpunkt, senden die folgenden initiiert die Web-app, die den Code erhalten haben  
  
**Tokenanforderung:**  
POST https://fs.contoso.com/adfs/oauth2/Token
  
  
  
Parameter|Wert  
---------|---------  
grant_type|"Authorization_code"  
Code|Autorisierungscode von oben  
Ressource|RP-ID (ID) des Web-API in Anwendungsgruppe  
client_id|Client-Id für die Web-app (Server-Anwendung) in der Anwendungsgruppe  
redirect_uri|Umleiten der URI des Web-app (Server-Anwendung) in "Anwendungsserver"  
client_secret|Geheimen Schlüssel der Web-App (Server-Anwendung) in der Anwendungsgruppe  
  
**Tokenanforderung Antwort:**  
AD FS antwortet mit einer HTTP-200 mit Access_token, Refresh_token und Id_token im Textkörper.  
  
4.  Die Web-Anwendung, und klicken Sie dann entweder die Access_token Teil der oben genannten Antwort (in der Fall, in dem die Web-app selbst die Ressource hostet) verwendet oder auf andere Weise sendet er als Autorisierungsheader in der HTTP-Anforderung an die Web-API.  
  
#### <a name="single-sign-on-behavior"></a>Das Verhalten für einmaliges Anmelden  
Das Verhalten für einmaliges Anmelden ist identisch mit denen für die Steuerung der Oauth 2.0-vertrauliche Client oben.  
  
### <a name="on-behalf-of"></a>Im Auftrag von  
In diesem Szenario verwendet eine Web-app das ursprüngliche Zugriffstoken eines Benutzers anfordern und erhalten einen anderen Zugriffstoken für einen anderen Web-API, die die Web-app dann als der Benutzer zugreifen.  Dies ist ein Fluss "im Auftrag von" bezeichnet.  
  
![Beschreibung des Protokolls Fluss](media/ADFS_DEV_6.png)  
  
Schritte 1 und 2 funktioniert genau wie die Schritte 3 und 4 im vorherigen Fluss.  
In Schritt 3 ist die wichtigste Anforderung, dass der Client_id-Parameter, die Client-ID der Web-App 2, die RP-ID der Web-API A. übereinstimmen müssen Anders ausgedrückt, muss die Zielgruppe des Zugriffstokens, die für das neue Token ausgetauscht werden die Client-ID der Entität, die neue Token anfordert übereinstimmen.  

## <a name="related-content"></a>Verwandte Inhalte  
Finden Sie unter [AD FS-Entwicklung](../AD-FS-Development.md) für die vollständige Liste der exemplarischen Vorgehensweise Artikel, die eine schrittweise Anleitung zur Verwendung von verwandten Flüsse bereitstellen. 
