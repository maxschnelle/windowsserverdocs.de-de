---
title: Anpassen des HTTP-Antwort-Sicherheitsheader mit AD FS
description: Dieses Dokument Descirbes Security-Header zum Schutz vor Sicherheitsrisiken anpassen.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 231c8783032f51f607565922d90ea7f7eb877cfd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444691"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>Anpassen des HTTP-Antwort-Sicherheitsheader mit AD FS-2019 
 
Zum Schutz vor allgemeinen Sicherheitsrisiken und bieten Administratoren die Möglichkeit, den neuesten Entwicklungen in browserbasierten Schutzmechanismen nutzen, hinzugefügt AD FS-2019 die Funktionalität zum Anpassen der HTTP-Antwort-Sicherheitsheader gesendet von AD FS. Dies erfolgt durch die Einführung von zwei neue Cmdlets: `Get-AdfsResponseHeaders` und `Set-AdfsResponseHeaders`.  
 
In diesem Dokument erörterten häufig wird verwendet, Security-Antwort-Header veranschaulicht, wie Sie von AD FS-2019 gesendeten Header anpassen.   
 
>[!NOTE]
>Das Dokument wird davon ausgegangen, dass AD FS-2019 installiert wurde.  

 
Bevor wir Header erläutern, wir sehen uns nun einige Szenarien notwendig für Administratoren zum Anpassen der Security-Header 
 
## <a name="scenarios"></a>Szenarien 
1. Administrator aktiviert hat [ **HTTP Strict-Transport-Security (HSTS)** ](#http-strict-transport-security-hsts) (erzwingt, dass alle Verbindungen über HTTPS-Verschlüsselung), die Benutzer zu schützen, die die Web-app mithilfe von HTTP über einen öffentlichen WLAN-Zugriffs zugreifen kann der Punkt, die gehackt werden kann. Sie möchten die Sicherheit weiter zu erhöhen, durch die Aktivierung von HSTS für untergeordnete Domänen.  
2. Administrator wurde konfiguriert. die [ **X-Frame-Options** ](#x-frame-options) Antwortheader (Rendern von jeder Webseite in einem iFrame verhindert) zu verhindern, dass die Webseiten Clickjacked wird. Allerdings muss er zum Anpassen des Headerwert aufgrund einer neuen geschäftlichen Anforderung zum Anzeigen von Daten (im iFrame) aus einer Anwendung mit einem anderen Ursprung (Domäne).
3. Administrator aktiviert hat [ **X-XSS-Protection** ](#x-xss-protection) (cross-scripting-Angriffe verhindert) zu bereinigen und blockieren die Seite aus, wenn Browser erkennt, cross-scripting-Angriffe. Allerdings muss sie zum Anpassen von Header an, um die Seite laden können einmal bereinigt.  
4. Administrator aktivieren muss [ **Cross Origin Resource Sharing (CORS)** ](#cross-origin-resource-sharing-cors-headers) und legen Sie den Ursprung (Domäne) in AD FS zu einer einseitigen Anwendung auf eine Web-API mit einer anderen Domäne zugreifen können.  
5. Administrator aktiviert hat [ **(Content Security Policy, CSP)** ](#content-security-policy-csp) -Header auf cross-Site scripting und Daten-Einschleusung zu verhindern, dass Angriffe, indem er die domänenübergreifende Anforderungen untersagt. Aufgrund einer neuen geschäftsanforderung muss er jedoch Anpassen des Headers, um die Webseite zum Laden von Bildern aus einem beliebigen Ursprung und Einschränken von Medien für vertrauenswürdige Anbieter zu ermöglichen.  

 
## <a name="http-security-response-headers"></a>HTTP-Antwort-Sicherheitsheader 
Die Header der Antwort sind in der ausgehenden HTTP-Antwort, die von AD FS gesendet wird, auf einen Webbrowser enthalten. Die Header können aufgeführt werden, mit der `Get-AdfsResponseHeaders` Cmdlet wie unten dargestellt.  

![Headerantwort](media/customize-http-security-headers-ad-fs/header1.png)

Die `ResponseHeaders` -Attribut im obigen Screenshot identifiziert den Security-Header, die von AD FS in jeder HTTP-Antwort enthalten sind. Die Header der Antwort gesendet wird, nur wenn `ResponseHeadersEnabled` nastaven NA hodnotu `True` (Standardwert). Der Wert kann festgelegt werden, um `False` um AD FS, einschließlich der Security-Header in der HTTP-Antwort zu verhindern. Dies ist jedoch nicht empfohlen.  Verwenden Sie hierzu Folgendes:

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```
 
### <a name="http-strict-transport-security-hsts"></a>HTTP Strict-Transport-Security (HSTS) 
HSTS ist ein Web-Richtlinie Sicherheitsmechanismus wodurch zu verringern, Protokoll Downgrade-Angriffe und Cookie-Hijacking für Dienste, die HTTP- und HTTPS-Endpunkte haben. Sie können Webserver deklarieren, dass der Webbrowser (oder anderen leitete Benutzer-Agents) nur mithilfe von HTTPS und nie über das HTTP-Protokoll interagieren müssen.  
 
Alle AD FS-Endpunkte für die Authentifizierung von Webverkehr werden ausschließlich über HTTPS geöffnet. AD FS werden daher effektiv die Risiken, die HTTP Strict Transport Security richtlinienmechanismus bereitstellt (es wird standardmäßig kein Downgrade auf HTTP da es sich um keine Listener in HTTP). Der Header kann angepasst werden, indem Sie die folgenden Parameter festlegen 
 
- **Max-Age =&lt;ablaufen Kompilierzeit&gt;**  – die Ablaufzeit (in Sekunden) gibt an, wie lange die Website ist nur möglich sollten über HTTPS. Standardmäßige und empfohlene Wert ist 31536000 Sekunden (1 Jahr).  
- **IncludeSubDomains** – Dies ist ein optionaler Parameter. Wenn angegeben, gilt die Regel HSTS alle Unterdomänen ebenfalls ab.  
 
#### <a name="hsts-customization"></a>HSTS Anpassung 
Der Header ist standardmäßig aktiviert und `max-age` auf 1 Jahr festgelegt; allerdings können Administratoren ändern den `max-age` (Verringern der Max-Age-Wert wird nicht empfohlen) oder aktivieren Sie HSTS für untergeordnete Domänen über die `Set-AdfsResponseHeaders` Cmdlet.  
 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains" 
``` 

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains" 
 ```

Standardmäßig befindet sich die Header in der `ResponseHeaders` Attribut, jedoch können Administratoren den Header über Entfernen der `Set-AdfsResponseHeaders` Cmdlet.  
 
```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security" 
```

### <a name="x-frame-options"></a>X-Frame-Optionen 
AD FS standardmäßig erlaubt keine externe Anwendungen, die beim Ausführen einer interaktiver Anmeldungen iFrames verwendet. Dies erfolgt, um bestimmte Stil Phishing-Angriffe zu verhindern. Beachten Sie, dass nicht interaktiven Anmeldungen über iFrame aufgrund von vorherigen Sitzung-Sicherheit auf Zeilenebene ausgeführt werden können, das eingerichtet wurde.  
 
In seltenen Fällen können Sie jedoch eine bestimmte Anwendung vertrauen, die iFrame-fähige interaktive AD FS-Anmeldeseite erforderlich sind. Der Header "X-Frame-Options" wird für diesen Zweck verwendet.  
 
Diese HTTP-Antwortheader Sicherheit wird verwendet, um dem Browser mitteilen kann, ob er eine Seite rendern kann eine &lt;Frame&gt;/&lt;Iframe&gt;. Der Header kann auf einen der folgenden Werte festgelegt werden: 
 
- **Verweigern** : die Seite in einem Frame wird nicht angezeigt werden. Dies ist der standardmäßige und empfohlene Einstellung.  
- **Sameorigin** : die Seite wird nur im Rahmen angezeigt werden, wenn der Ursprung der Ursprung der Webseite identisch ist. Die Option ist nicht sehr nützlich, es sei denn, alle mittelbar übergeordneten Knoten in der gleichen Ursprungs ebenfalls enthalten sind.  
- **Zulassen von <specified origin>**  -Seite wird nur im Rahmen angezeigt werden, wenn der Ursprung (z.B. https://www. ". com) stimmt mit den besonderen Ursprung in der Kopfzeile. 

#### <a name="x-frame-options-customization"></a>X-Frame-Options-Anpassung  
Standardmäßig wird-Header festgelegt werden, um verweigern; Administratoren können jedoch den Wert durch Ändern der `Set-AdfsResponseHeaders` Cmdlet.  
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>" 
 ```

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com" 
 ```

Standardmäßig befindet sich die Header in der `ResponseHeaders` Attribut, jedoch können Administratoren den Header über Entfernen der `Set-AdfsResponseHeaders` Cmdlet.  

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options" 
```

### <a name="x-xss-protection"></a>X-XSS-Protection 
Diese HTTP-Antwort-Sicherheitsheader wird zum Beenden von Webseiten aus geladen werden, wenn Angriffe Cross-Site-scripting (XSS) vom Browser erkannt werden. Dies wird als XSS-Filter bezeichnet. Der Header kann auf einen der folgenden Werte festgelegt werden 
 
- **0** – deaktiviert die XSS-Filter. Nicht empfohlen.  
- **1** – ermöglicht XSS-Filter. Wenn XSS-Angriff erkannt wird, wird die Browser die Seite bereinigen.   
- **1 Modus = Block** – ermöglicht XSS-Filter. XSS-Angriff erkannt wird, wird Browser Rendern der Seite verhindert. Dies ist der standardmäßige und empfohlene Einstellung.  

#### <a name="x-xss-protection-customization"></a>X-XSS-Protection-Anpassung 
Standardmäßig wird der Header auf 1 festgelegt werden. Modus = Block Administratoren können jedoch den Wert durch Ändern der `Set-AdfsResponseHeaders` Cmdlet.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>" 
``` 

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1" 
 ```

Standardmäßig befindet sich die Header in der `ResponseHeaders` Attribut, jedoch können Administratoren den Header über Entfernen der `Set-AdfsResponseHeaders` Cmdlet. 

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection" 
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>Cross-Origin Resource Sharing (CORS)-Header 
Webbrowsersicherheit wird verhindert, dass eine Webseite, die Cross-Origin-Anforderungen, die von innerhalb von Skripts initiiert. Jedoch sollten Sie auch Zugriff auf Ressourcen in anderen Quellen (Domänen). CORS ist ein W3C-standard, der einem Server zu lockern die Richtlinie des gleichen Ursprungs ermöglicht. Mit CORS kann ein Server explizit einige ursprungsübergreifende Anforderungen zulassen und andere ablehnen.  
 
Zum besseren Verständnis der CORS-Anforderung muss wir exemplarischen Vorgehensweise ein Szenario, in denen eine einzelne Anwendung (SPA) Seite, eine Web-API mit einer anderen Domäne aufrufen. Darüber hinaus sehen Sie sich, dass sowohl SPA-API in AD FS 2019 konfiguriert sind und AD FS hat die Aktivierung von CORS z. B. AD FS CORS-Header in der HTTP-Anforderung zu identifizieren, überprüfen Sie die Headerwerte und entsprechenden CORS-Header in der Antwort enthalten können (Informationen zum Aktivieren und Konfigurieren von CORS in AD FS 2019 in CORS-Anpassung Abschnitt weiter unten). Beispiel-Ablauf: 

1. Benutzer greift auf SPA durch Clientbrowser und zur AD FS-Auth-Endpunkt zur Authentifizierung umgeleitet. Da die SPA für implizite Gewährung konfiguriert ist, fordern Sie gibt, die ein Zugriff und die ID-Token an den Browser nach erfolgreicher Authentifizierung.  
2. Nach der Benutzerauthentifizierung macht der Front-End-JavaScript-Code in die SPA enthalten eine Anforderung an die Web-API zugreifen. Die Anforderung wird an AD FS mit der folgenden Header umgeleitet.
    - "Optionen" – beschreibt die Kommunikation für die Zielressource 
    - Ursprung – umfasst den Ursprung der Web-API
    - Access-Control-Request-Method – gibt die HTTP-Methode (z.B. "DELETE") verwendet werden, wenn die tatsächliche Anforderung erfolgt ist 
    - Access-Control-Request-Headers - identifiziert die HTTP-Header verwendet werden, wenn die tatsächliche Anforderung erfolgt ist 
    
   >[!NOTE]
   >CORS-Anforderung ähnelt einer standard-HTTP-Anforderung, jedoch das Vorhandensein von einen Origin-Header signalisiert, dass die eingehende Anforderung CORS verknüpft ist. 
3. AD FS stellt sicher, dass es sich bei der Web-API-Ursprung in der Kopfzeile enthalten in der vertrauenswürdige Ursprünge, die in AD FS (Details zum Ändern der vertrauenswürdige Ursprünge im nachstehenden Abschnitt der CORS-Anpassung) konfiguriert aufgeführt ist. AD FS antwortet dann mit folgenden Header.  
    - Access-Control-Allow-Origin-Wert gleich wie in der Origin-Header 
    - Access-Control-ermöglichen-Method – denselben Wert, wie in der Access-Control-Request-Method-Header 
    - Access-Control-Allow-Headers - Wert denselben wie in der Access-Control-Request-Headers-header 
4. Browser sendet die tatsächliche Anforderung, einschließlich der folgenden Header 
    - HTTP-Methode (z. B., löschen) 
    - Ursprung – umfasst den Ursprung der Web-API 
    - Alle Header in der Access-Control-Allow-Headers-Antwortheader 
5. Nach der Überprüfung genehmigt AD FS die Anforderung mit der Web-API-Domäne (Ursprung) in der Access-Control-Allow-Origin-Antwortheader.  
6. Die Einbeziehung der Access-Control-Allow-Origin-Header können den Browser, um mit der die angeforderte API aufruft, fortfahren.

#### <a name="cors-customization"></a>CORS-Anpassung 
Standardmäßig werden die CORS-Funktion nicht aktiviert werden; Administratoren können jedoch die Funktionalität über das Cmdlet "Set-AdfsResponseHeaders" aktivieren.  

```PowerShell 
Set-AdfsResponseHeaders -EnableCORS $true 
 ```

Eine aktiviert, Administratoren werden in der Lage, eine Liste der vertrauenswürdigen Ursprünge, die mithilfe des gleichen Cmdlets aufzulisten. Z. B. der folgende Befehl können CORS-Anforderungen über die Ursprünge **Https&#58;//example1.com** und **Https&#58;//example1.com**. 
 
```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com 
 ```

> [!NOTE]
> Administratoren können CORS-Anforderungen von einem beliebigen Ursprung mit "*" in der Liste der vertrauenswürdigen Ursprünge, obwohl dieser Ansatz nicht, aufgrund von Schwachstellen des Sicherheit und eine Warnmeldung empfohlen wird wird bereitgestellt, wenn Sie dies. 

### <a name="content-security-policy-csp"></a>Content Security Policy (CSP) 
Diese HTTP-Antwort-Sicherheitsheader wird zum websiteübergreifendes scripting, Clickjacking und andere Data-Injection-Angriffe zu verhindern, indem Sie verhindern, dass Browser ausführen versehentlich böswillige Inhalte verwendet. Browsern, die mit Unterstützung für CSP nicht einfach ignoriert die CSP-Antwortheader.  
 
#### <a name="csp-customization"></a>CSP-Anpassung 
Anpassung des CSP-Headers umfasst das Ändern der Sicherheitsrichtlinie, die definiert, den Ressourcen-Browser für die Webseite geladen werden darf. Die Standardsicherheitsrichtlinie ist  
 
`Content-Security-Policy: default-src ‘self’ ‘unsafe-inline’ ‘’unsafe-eval’; img-src ‘self’ data:;` 
 
Die **Standard-Src** Direktive wird verwendet, um ändern [- Src-Direktiven](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) ohne jede Anweisung explizit auflisten. Im Beispiel unten die Richtlinie ist 1 z. B. die Richtlinie 2 entspricht.  

Richtlinie 1 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'" 
```
 
Richtlinie 2
```PowerShell 
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self’; img-src ‘self’; font-src 'self';  
frame-src 'self'; manifest-src 'self'; media-src 'self';" 
```

Wenn eine Richtlinie explizit aufgeführt wird, überschreibt der angegebene Wert vom Wert für die Standard-Src an. Im folgenden Beispiel wird das Img-Src-nehmen Sie den Wert als "*" (Images von einem beliebigen Ursprung geladen werden können), während andere - Src-Anweisungen den Wert annehmen, werden als "Self" (an denselben Ursprung, wie die Webseite einschränken).  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self’; img-src *" 
```
Folgende Quellen kann für die Standard-Src-Richtlinie definiert werden 
 
- 'self': durch diese Angabe beschränkt, den Ursprung des Inhalts, die an den Ursprung der Webseite zu laden. 
- 'unsafe-Inline': Angabe in der Richtlinie ermöglicht die Verwendung von Inline-JavaScript und CSS 
- "unsafe-eval" – ermöglicht die Angabe dieser in der Richtlinie für die Verwendung von Text, der JavaScript-Mechanismen wie eval 
- Durch diese Angabe 'none': den Inhalt einschränkt, von einem beliebigen Ursprung laden 
- Daten:-angeben: URIs kann Inhaltsersteller kleine Dateien Inline in Dokumente einbetten. Die Verwendung nicht empfohlen.  
 
>[!NOTE]
>AD FS verwendet JavaScript, bei der Authentifizierung und ermöglicht daher die JavaScript durch Einschließen der "unsafe-Inline-" und "unsafe-eval" in Quellen Richtlinie.  

### <a name="custom-headers"></a>Benutzerdefinierte Header 
Zusätzlich zu den obigen aufgeführten Antwortheader Security (HSTS, CSP, X-Frame-Options "," X-XSS-Protection "und" CORS), AD FS-2019 bietet die Möglichkeit, neue Header festgelegt.  
 
Beispiel: Um einen neuen Header "TestHeader" mit Wert als "TestHeaderValue" festzulegen. 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue" 
 ```

Nach dem festlegen, wird der neue Kopf in der AD FS-Antwort (Fiddler Codeausschnitt unten) gesendet.  
 
![Fiddler](media/customize-http-security-headers-ad-fs/header2.png)

## <a name="web-browswer-compatibility"></a>Web Browswer-Kompatibilität
Verwenden Sie die folgende Tabelle und die folgenden Links, um zu bestimmen, welche Webbrowser mit jedem der Antwortheader Sicherheit kompatibel sind.

|HTTP-Antwort-Sicherheitsheader|Browserkompatibilität|
|-----|-----|
|HTTP Strict-Transport-Security (HSTS)|[HSTS Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X-Frame-Optionen|[X-Frame-Options-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)| 
|X-XSS-Protection|[X-XSS-Protection Browserkompatibilität](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)| 
|Cross-Origin Resource Sharing (CORS)|[CORS-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility) 
|Content Security Policy (CSP)|[CSP-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility) 

## <a name="next"></a>Nächste

- [Verwenden Sie AD FS-Hilfe Troublehshooting Leitfäden](https://aka.ms/adfshelp/troubleshooting )
- [Behandeln von AD FS-Problemen](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
