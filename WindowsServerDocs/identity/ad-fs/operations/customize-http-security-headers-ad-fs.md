---
title: Anpassen von http-Sicherheits Antwort Headern mit AD FS
description: In diesem Dokument wird beschrieben, wie Sicherheits Header angepasst werden, um Schutz vor Sicherheitsrisiken zu schützen.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: akgoel23
ms.date: 02/19/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7fd06c06a2ea7af93b87c471f77b788ac51bddac
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949216"
---
# <a name="customize-http-security-response-headers-with-ad-fs-2019"></a>Anpassen von http-Sicherheits Antwort Headern mit AD FS 2019 
 
Um vor allgemeinen Sicherheitsrisiken zu schützen und Administratoren die Möglichkeit zu bieten, die neuesten Verbesserungen in browserbasierten Schutzmechanismen zu nutzen, wurde AD FS 2019 die Funktionalität zum Anpassen der http-Sicherheits Antwortheader hinzugefügt. gesendet von AD FS. Dies wird durch die Einführung von zwei neuen Cmdlets erreicht: `Get-AdfsResponseHeaders` und `Set-AdfsResponseHeaders`.  

>[!NOTE]
>Die Funktionalität zum Anpassen der http-Sicherheits Antwortheader (mit Ausnahme von cors-Headern) mithilfe von Cmdlets: `Get-AdfsResponseHeaders` und `Set-AdfsResponseHeaders` wurde auf AD FS 2016 zurückportiert. Sie können die Funktionalität Ihrer AD FS 2016 hinzufügen, indem Sie [KB4493473](https://support.microsoft.com/help/4493473/windows-10-update-kb4493473) und [KB4507459](https://support.microsoft.com/help/4507459/windows-10-update-kb4507459)installieren. 

In diesem Dokument werden häufig verwendete Sicherheits Antwortheader erläutert, um zu veranschaulichen, wie von AD FS 2019 gesendete Header angepasst werden.   
 
>[!NOTE]
>In diesem Dokument wird davon ausgegangen, dass AD FS 2019 installiert wurde.  

 
Bevor wir Header erörtern, betrachten wir einige Szenarien, in denen die Notwendigkeit von Administratoren zum Anpassen von Sicherheits Headern erläutert wird. 
 
## <a name="scenarios"></a>Szenarien 
1. Der Administrator hat [**http Strict-Transport-Security (hsts)** ](#http-strict-transport-security-hsts) aktiviert (erzwingt alle Verbindungen über die HTTPS-Verschlüsselung), um die Benutzer, die möglicherweise auf die Web-App zugreifen, über HTTP von einem öffentlichen WLAN-Zugriffspunkt zu schützen, der möglicherweise gehackt ist Sie möchte die Sicherheit durch Aktivieren von hsts für Unterdomänen weiter erhöhen.  
2. Der Administrator hat den Antwortheader " [**X-Frame-Options**](#x-frame-options) " konfiguriert (verhindert das Rendern von Webseiten in einem IFRAME), um die Webseiten vor der klistung zu schützen. Allerdings muss Sie den Header Wert aufgrund einer neuen geschäftlichen Anforderung anpassen, um Daten (in iframe) aus einer Anwendung mit einem anderen Ursprung (Domäne) anzuzeigen.
3. Der Administrator hat [**X-XSS-Protection**](#x-xss-protection) aktiviert (verhindert Kreuz Skript Angriffe), die Seite zu bereinigen und zu blockieren, wenn der Browser Kreuz Skript Angriffe erkennt. Allerdings muss der Header angepasst werden, damit die Seite nach dem Bereinigen geladen werden kann.  
4. Der Administrator muss [**cors (Cross Origin Resource Sharing)** ](#cross-origin-resource-sharing-cors-headers) aktivieren und den Ursprung (Domäne) auf AD FS festlegen, damit eine Einzelseiten Anwendung auf eine Web-API mit einer anderen Domäne zugreifen kann.  
5. Der Administrator hat den Header der [**Inhalts Sicherheitsrichtlinie (Content Security Policy, CSP)** ](#content-security-policy-csp) aktiviert, um Site übergreifende Skripts und Daten einschleusungs Angriffe zu verhindern. Aufgrund einer neuen geschäftlichen Anforderung muss Sie jedoch den Header so anpassen, dass die Webseite das Laden von Bildern von einem beliebigen Ursprung und das Einschränken von Medien auf vertrauenswürdige Anbieter zulässt.  

 
## <a name="http-security-response-headers"></a>HTTP-Sicherheits Antwortheader 
Die Antwortheader sind in der ausgehenden HTTP-Antwort enthalten, die von AD FS an einen Webbrowser gesendet wird. Die Header können wie unten gezeigt mithilfe des `Get-AdfsResponseHeaders`-Cmdlets aufgelistet werden.  

![Header Antwort](media/customize-http-security-headers-ad-fs/header1.png)

Das `ResponseHeaders`-Attribut im obigen Screenshot identifiziert die Sicherheits Header, die in jeder HTTP-Antwort in AD FS eingeschlossen werden. Die Antwortheader werden nur gesendet, wenn `ResponseHeadersEnabled` auf `True` (Standardwert) festgelegt ist. Der Wert kann auf `False` festgelegt werden, um zu verhindern, dass AD FS einschließlich der Sicherheits Header in der HTTP-Antwort ist. Dies wird jedoch nicht empfohlen.  Verwenden Sie hierzu Folgendes:

```PowerShell
Set-AdfsResponseHeaders -EnableResponseHeaders $false
```
 
### <a name="http-strict-transport-security-hsts"></a>HTTP Strict-Transport-Security (hsts) 
Hsts ist ein Mechanismus für die Websicherheits Richtlinie, mit dem Angriffe herab Stufungs Angriffe und Cookie-Hijacking für Dienste mit http-und HTTPS-Endpunkten minimiert werden können. Auf diese Weise können Webserver deklarieren, dass Webbrowser (oder andere Benutzer-Agents) nur mit HTTPS und nie über das HTTP-Protokoll interagieren sollen.  
 
Alle AD FS Endpunkte für den Webauthentifizierungs Datenverkehr werden exklusiv über HTTPS geöffnet. Demzufolge werden von AD FS effektiv die Bedrohungen verringert, die der http-Mechanismus für die strikte Transport Sicherheit bietet (Standardmäßig gibt es kein Downgrade auf http, da keine Listener in http vorhanden sind). Der Header kann angepasst werden, indem die folgenden Parameter festgelegt werden:
 
- **max-age =&lt;** Ablaufzeit&gt;– die Ablaufzeit (in Sekunden) gibt an, wie lange der Zugriff auf den Standort nur über HTTPS erfolgen soll. Der standardmäßige und empfohlene Wert ist 31536000 Sekunden (1 Jahr).  
- **includesubdomains** – Dies ist ein optionaler Parameter. Wenn angegeben, gilt die hsts-Regel auch für alle Unterdomänen.  
 
#### <a name="hsts-customization"></a>Hsts-Anpassung 
Standardmäßig ist der-Header aktiviert und `max-age` auf 1 Jahr festgelegt. Allerdings können Administratoren die `max-age` ändern (der Wert "max-age verringern" wird nicht empfohlen), oder Sie können hsts für Unterdomänen über das `Set-AdfsResponseHeaders`-Cmdlet aktivieren.  
 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=<seconds>; includeSubDomains" 
``` 

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Strict-Transport-Security" -SetHeaderValue "max-age=31536000; includeSubDomains" 
 ```

Standardmäßig ist der-Header im `ResponseHeaders`-Attribut enthalten. Allerdings können Administratoren die Kopfzeile über das `Set-AdfsResponseHeaders`-Cmdlet entfernen.  
 
```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "Strict-Transport-Security" 
```

### <a name="x-frame-options"></a>X-Frame-Optionen 
Bei der Ausführung interaktiver Anmeldungen ist es AD FS standardmäßig nicht zulässig, dass externe Anwendungen iframes verwenden. Dadurch wird eine bestimmte Art von Phishingangriffen verhindert. Beachten Sie, dass nicht interaktive Anmeldungen über IFRAME ausgeführt werden können, da die zuvor festgelegte Sicherheit auf Sitzungs Ebene aufgetreten ist.  
 
In bestimmten seltenen Fällen können Sie jedoch eine bestimmte Anwendung als vertrauenswürdig einstufen, die iframe-fähige interaktive AD FS Anmeldeseite erfordert. Zu diesem Zweck wird der X-Frame-Options-Header verwendet.  
 
Dieser http-Sicherheits Antwortheader wird verwendet, um mit dem Browser zu kommunizieren, ob er eine Seite in einem &lt;Frame&gt;/&lt;IFRAME-&gt;Rendering kann. Der Header kann auf einen der folgenden Werte festgelegt werden: 
 
- **Deny** – die Seite in einem Frame wird nicht angezeigt. Dies ist die Standardeinstellung und die empfohlene Einstellung.  
- **sameorigin** – die Seite wird nur im Frame angezeigt, wenn der Ursprung mit dem Ursprung der Webseite identisch ist. Die Option ist nicht sehr nützlich, es sei denn, alle Vorgänger befinden sich ebenfalls im selben Ursprung.  
- **Allow-from <specified origin>** : die Seite wird nur im Frame angezeigt, wenn der Ursprung (z. b. https://www. ". com) entspricht dem spezifischen Ursprung in der Kopfzeile. 

#### <a name="x-frame-options-customization"></a>Anpassung der X-Frame-Optionen  
Standardmäßig wird der Header auf verweigern festgelegt. Administratoren können den Wert jedoch über das Cmdlet "`Set-AdfsResponseHeaders`" ändern.  
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "<deny/sameorigin/allow-from<specified origin>>" 
 ```

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-Frame-Options" -SetHeaderValue "allow-from https://www.example.com" 
 ```

Standardmäßig ist der-Header im `ResponseHeaders`-Attribut enthalten. Allerdings können Administratoren die Kopfzeile über das `Set-AdfsResponseHeaders`-Cmdlet entfernen.  

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-Frame-Options" 
```

### <a name="x-xss-protection"></a>X-XSS-Schutz 
Dieser http-Sicherheits Antwortheader wird verwendet, um das Laden von Webseiten zu beenden, wenn XSS-Angriffe (Cross-Site Scripting) von Browsern erkannt werden. Dies wird als XSS-Filterung bezeichnet. Der Header kann auf einen der folgenden Werte festgelegt werden:
 
- **0** – deaktiviert die XSS-Filterung. Nicht empfehlenswert.  
- **1** – aktiviert das Filtern von XSS. Wenn ein XSS-Angriff erkannt wird, wird die Seite von Browser bereinigt.   
- **1; Mode = Block** – aktiviert die XSS-Filterung. Wenn ein XSS-Angriff erkannt wird, verhindert der-Browser das Rendern der Seite. Dies ist die Standardeinstellung und die empfohlene Einstellung.  

#### <a name="x-xss-protection-customization"></a>Anpassung des X-XSS-Schutzes 
Standardmäßig wird der-Header auf 1 festgelegt. Mode = Block; Administratoren können den Wert jedoch über das Cmdlet "`Set-AdfsResponseHeaders`" ändern.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "<0/1/1; mode=block/1; report=<reporting-uri>>" 
``` 

Beispiel: 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "X-XSS-Protection" -SetHeaderValue "1" 
 ```

Standardmäßig ist der-Header im `ResponseHeaders`-Attribut enthalten. Administratoren können die Kopfzeile jedoch über das `Set-AdfsResponseHeaders`-Cmdlet entfernen. 

```PowerShell
Set-AdfsResponseHeaders -RemoveHeaders "X-XSS-Protection" 
```

### <a name="cross-origin-resource-sharing-cors-headers"></a>Cross-Origin Resource Sharing (cors)-Header 
Die Webbrowser Sicherheit verhindert, dass eine Webseite Ursprungs übergreifende Anforderungen aus Skripts initiiert. Manchmal möchten Sie jedoch möglicherweise auf Ressourcen in anderen Ursprüngen (Domänen) zugreifen. Cors ist ein W3C-Standard, der es einem Server ermöglicht, die Richtlinie für denselben Ursprung zu lockern. Mit CORS kann ein Server explizit einige ursprungsübergreifende Anforderungen zulassen und andere ablehnen.  
 
Um die cors-Anforderung besser zu verstehen, betrachten wir ein Szenario, in dem eine Single-Page-Anwendung (Spa) eine Web-API mit einer anderen Domäne aufruft. Beachten Sie außerdem, dass sowohl Spa als auch API auf ADFS 2019 konfiguriert sind AD FS und dass cors aktiviert ist, d. h. AD FS cors-Header in der HTTP-Anforderung identifizieren, Header Werte validieren und entsprechende cors-Header in der Antwort einschließen (Details zum Aktivieren von und). Konfigurieren Sie cors auf AD FS 2019 in cors-Anpassungs Abschnitt weiter unten). Beispiel Fluss: 

1. Der Benutzer greift über den Client Browser auf Spa zu und wird zur Authentifizierung an AD FS Authentifizierungs Endpunkt umgeleitet. Da die Spa für den impliziten Zuweisungs Fluss konfiguriert ist, gibt die Anforderung nach erfolgreicher Authentifizierung ein Zugriffs-und ID-Token an den Browser zurück.  
2. Nach der Benutzerauthentifizierung sendet das Front-End-JavaScript, das in Spa enthalten ist, eine Anforderung für den Zugriff auf die Web-API. Die Anforderung wird mit den folgenden Headern an AD FS umgeleitet:
    - Optionen – beschreibt die Kommunikationsoptionen für die Ziel Ressource. 
    - Ursprung – schließt den Ursprung der Web-API ein.
    - Access-Control-Request-Method – identifiziert die HTTP-Methode (z. b. Delete), die bei der tatsächlichen Anforderung verwendet werden soll. 
    - Access-Control-Request-Headers: identifiziert die HTTP-Header, die verwendet werden sollen, wenn die tatsächliche Anforderung erfolgt. 
    
   >[!NOTE]
   >Eine cors-Anforderung ähnelt einer Standard-HTTP-Anforderung. das vorhanden sein eines Ursprungs Headers signalisiert jedoch, dass die eingehende Anforderung mit cors verknüpft ist. 
3. AD FS überprüft, ob der in der Kopfzeile enthaltene Web-API-Ursprung in den in AD FS konfigurierten vertrauenswürdigen Ursprüngen aufgeführt ist (Ausführliche Informationen zum Ändern von vertrauenswürdigen Ursprüngen im Abschnitt cors-Anpassung weiter unten). AD FS antwortet dann mit den folgenden Headern:  
    - Access-Control-Allow-Origin – Wert identisch mit dem Wert im Ursprungs Header 
    - Access-Control-Allow-Method – Wert identisch mit dem Wert im Access-Control-Request-Method-Header 
    - Access-Control-Allow-Headers-Wert identisch mit dem Wert im Access-Control-Request-Headers-Header 
4. Der Browser sendet die tatsächliche Anforderung einschließlich der folgenden Header:
    - HTTP-Methode (z. b. Delete) 
    - Ursprung – schließt den Ursprung der Web-API ein. 
    - Alle Header im Antwortheader "Access-Control-Allow-Headers" 
5. Nach der Überprüfung AD FS die Anforderung durch einschließen der Web-API-Domäne (Ursprung) in den Antwortheader "Access-Control-Allow-Origin" genehmigt.  
6. Durch die Einbindung des Headers Access-Control-Allow-Origin kann der Browser mit dem Aufrufen der angeforderten API fortfahren.

#### <a name="cors-customization"></a>Cors-Anpassung 
Standardmäßig wird die cors-Funktionalität nicht aktiviert. Administratoren können die Funktionalität jedoch über das Cmdlet "Set-adfsresponseheaders" aktivieren.  

```PowerShell 
Set-AdfsResponseHeaders -EnableCORS $true 
 ```

Eine aktivierte, Administratoren können mit demselben Cmdlet eine Liste vertrauenswürdiger Ursprünge auflisten. Beispielsweise können mit dem folgenden Befehl cors-Anforderungen von den Ursprüngen **https&#58;//example1.com** und **https&#58;//example1.com**zugelassen werden. 
 
```PowerShell
Set-AdfsResponseHeaders -CORSTrustedOrigins https://example1.com,https://example2.com 
 ```

> [!NOTE]
> Administratoren können cors-Anforderungen von einem beliebigen Ursprung aus zulassen, indem Sie "*" in die Liste der vertrauenswürdigen Ursprünge einschließen, obwohl dieser Ansatz aufgrund von Sicherheitsrisiken nicht empfohlen wird und eine Warnmeldung bereitgestellt wird, wenn Sie sich entscheiden. 

### <a name="content-security-policy-csp"></a>Inhalts Sicherheitsrichtlinie (CSP) 
Dieser http-Sicherheits Antwortheader wird verwendet, um Site übergreifende Skripts, Clickjacking und andere Daten einschleusungs Angriffe zu verhindern, indem verhindert wird, dass die Browser versehentlich bösartige Inhalte ausführen. Browser, die CSP nicht unterstützen, ignorieren einfach die CSP-Antwortheader.  
 
#### <a name="csp-customization"></a>CSP-Anpassung 
Die Anpassung des CSP-Headers umfasst das Ändern der Sicherheitsrichtlinie, die definiert, welche Ressourcen Browser für die Webseite geladen werden dürfen. Die Standard Sicherheitsrichtlinie lautet  
 
`Content-Security-Policy: default-src ‘self' ‘unsafe-inline' ‘'unsafe-eval'; img-src ‘self' data:;` 
 
Die **default-src** -Direktive dient zum Ändern von [-src-Direktiven](https://developer.mozilla.org/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) , ohne jede Direktive explizit aufzulisten. Beispielsweise ist im folgenden Beispiel die Richtlinie 1 mit der Richtlinie 2 identisch.  

Richtlinie 1 
```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src 'self'" 
```
 
Richtlinie 2
```PowerShell 
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "script-src ‘self'; img-src ‘self'; font-src 'self';  
frame-src 'self'; manifest-src 'self'; media-src 'self';" 
```

Wenn eine-Direktive explizit aufgelistet ist, überschreibt der angegebene Wert den für Default-src angegebenen Wert. Im folgenden Beispiel nimmt img-src den Wert "*" (damit Bilder aus beliebigen Ursprungs geladen werden können), während andere-src-Direktiven den Wert als "Self" (auf denselben Ursprung wie die Webseite einschränken) übernehmen.  

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "Content-Security-Policy" -SetHeaderValue "default-src ‘self'; img-src *" 
```
Die folgenden Quellen können für die Default-src-Richtlinie definiert werden:
 
- "Self" – Dies bedeutet, dass der Ursprung des Inhalts auf den Ursprung der Webseite beschränkt wird. 
- "unsicher-Inline" – die Angabe dieses in der Richtlinie ermöglicht die Verwendung von Inline-JavaScript und CSS. 
- "unsicher-eval" – die Angabe dieses in der Richtlinie ermöglicht die Verwendung von Text-zu-JavaScript-Mechanismen wie eval. 
- "None" – durch Angabe dieser Einschränkung wird der Inhalt von einem beliebigen Ursprung zum Laden eingeschränkt. 
- Daten: durch das Angeben von Daten: URIs können Inhalts Ersteller kleine Dateien Inline in Dokumente einbetten. Die Verwendung ist nicht empfehlenswert.  
 
>[!NOTE]
>AD FS verwendet JavaScript im Authentifizierungsprozess und aktiviert daher JavaScript durch das Einschließen von "unsichere Inline" und "unsichere-eval"-Quellen in die Standard Richtlinie.  

### <a name="custom-headers"></a>Benutzerdefinierte Header 
Zusätzlich zu den oben aufgeführten Sicherheits Antwort Headern (hsts, CSP, x-Frame-Options, x-XSS-Protection und cors) bietet AD FS 2019 die Möglichkeit, neue Header festzulegen.  
 
Beispiel: So legen Sie einen neuen Header "tesderader" mit dem Wert "testhadervalue" fest 

```PowerShell
Set-AdfsResponseHeaders -SetHeaderName "TestHeader" -SetHeaderValue "TestHeaderValue" 
 ```

Nachdem die neue Kopfzeile festgelegt wurde, wird Sie in der AD FS-Antwort (unten nach dem folgenden Code Ausschnitt) gesendet.  
 
![Fiddler](media/customize-http-security-headers-ad-fs/header2.png)

## <a name="web-browser-compatibility"></a>Webbrowser Kompatibilität
Verwenden Sie die folgende Tabelle und die Links, um zu bestimmen, welche Webbrowser mit den einzelnen Sicherheits Antwort Headern kompatibel sind.

|HTTP-Sicherheits Antwortheader|Browserkompatibilität|
|-----|-----|
|HTTP Strict-Transport-Security (hsts)|[Hsts-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/Headers/Strict-Transport-Security#Browser_compatibility)|
|X-Frame-Optionen|[X-Frame-Options-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility)| 
|X-XSS-Schutz|[Browserkompatibilität mit X-XSS-Protection](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-XSS-Protection#Browser_compatibility)| 
|Ressourcenfreigabe zwischen verschiedenen Ursprüngen (CORS)|[Cors-Browserkompatibilität](https://developer.mozilla.org/docs/Web/HTTP/CORS#Browser_compatibility) 
|Inhalts Sicherheitsrichtlinie (CSP)|[Kompatibilität des CSP-Browsers](https://developer.mozilla.org/docs/Web/HTTP/CSP#Browser_compatibility) 

## <a name="next"></a>Weiter

- [Verwenden AD FS Hilfe Handbücher zur Problembehandlung](https://aka.ms/adfshelp/troubleshooting )
- [Behandeln von AD FS-Problemen](../../ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
