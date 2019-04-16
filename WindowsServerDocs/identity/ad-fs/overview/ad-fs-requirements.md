---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: AD FS 2016-Anforderungen
description: "Anforderungen für die Installation von Active Directory Federation Services."
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81b51c751d5f54436b14450ef21bf49feb864290
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen

>Gilt für: Windows Server 2016

Im folgenden sind die Anforderungen für die Bereitstellung von AD FS:  
  
-   [Zertifikatanforderungen](ad-fs-requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](ad-fs-requirements.md#BKMK_2)  
  
-   [Proxy-Anforderungen](ad-fs-requirements.md#BKMK_3)  
  
-   [AD DS-Anforderungen](ad-fs-requirements.md#BKMK_4)  
  
-   [Anforderungen an die Datenbank](ad-fs-requirements.md#BKMK_5)  
  
-   [Anforderungen an Webbrowser](ad-fs-requirements.md#BKMK_6)  

-   [Netzwerkanforderungen](ad-fs-requirements.md#BKMK_7)  
  
-   [Erforderliche Berechtigungen](ad-fs-requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>Zertifikatanforderungen  
  
### <a name="ssl-certificates"></a>SSL-Zertifikate

Jeder AD FS und Web Application Proxy-Server hat Service HTTPS-Anforderungen an den Verbunddienst ein SSL-Zertifikat.  The Web Application Proxy können zusätzliche SSL-Zertifikate für Serviceanfragen mit veröffentlichten Anwendungen verfügen.

**Empfehlung:** dasselbe SSL-Zertifikat für alle AD FS-Verbundserver und Web Application-Proxys verwenden. 

**Anforderungen:**

SSL-Zertifikate auf Verbundservern müssen die folgenden Anforderungen erfüllen.
- Zertifikat ist öffentlich vertrauenswürdigen (für den Praxiseinsatz)
- Zertifikat enthält den Wert Server Authentifizierung erweiterten Schlüsselverwendung (EKU)
- Zertifikat enthält den Namen des Verbunddiensts, z.B. "fs.contoso.com" im Betreff oder (Subject Alternative Name, SAN)
- Für die benutzerzertifikatauthentifizierung Port 443 enthält Zertifikat "Certauth. \ < Federation Service Tokentypen >", z.B. "certauth.fs.contoso.com" im SAN
- Für die Geräteregistrierung oder für moderne-Authentifizierung auf lokalen Ressourcen vor Windows10-Clients verwenden muss die SAN "Enterpriseregistration. \ < Upn Suffix\ >" für jede Benutzerprinzipalnamen-Suffix verwendet in Ihrer Organisation enthalten.

SSL-Zertifikate auf den Web Application Proxy müssen die folgenden Anforderungen erfüllen.
- Wenn der Proxy, um verwendet wird müssen AD FS-Proxy-Anfragen, die integrierte Windows-Authentifizierung, die Proxy-SSL-Zertifikat verwenden identisch sein (mit dem gleichen Schlüssel) das SSL-Zertifikat Föderation
- Wenn die AD FS-Eigenschaft, die "ExtendedProtectionTokenCheck" ist (die Standardeinstellung in AD FS) aktiviert ist, muss die Proxy-SSL-Zertifikat identisch sein (verwenden Sie den gleichen Schlüssel) das SSL-Zertifikat Föderation
- Andernfalls sind die Anforderungen für die Proxy-SSL-Zertifikat identisch mit denen für das SSL-Zertifikat Föderation

### <a name="service-communication-certificate"></a>Dienstkommunikationszertifikat
Dieses Zertifikat ist nicht erforderlich, für die meisten AD FS-Szenarien, einschließlich der Azure AD und Office365. Standardmäßig konfiguriert AD FS das SSL-Zertifikat nach der Erstkonfiguration als das dienstkommunikationszertifikat bereitgestellt.

**Empfehlung:**
- Verwenden Sie das gleiche Zertifikat wie für SSL.  

### <a name="token-signing-certificate"></a>Token Signing Certificate
Dieses Zertifikat ist verwendeten Anmeldung ausgestellte Token für vertrauende Seiten, sodass Anwendungen der vertrauenden Seite das Zertifikat erkennen müssen und der zugehörige Schlüssel als bekannte und vertrauenswürdige. Wenn das Token signierenden Zertifikat ändert, z.B. wenn es abgelaufen ist und Sie ein neues Zertifikat konfigurieren, müssen alle vertrauende Seiten aktualisiert werden.

**Empfehlung:** verwenden Sie die AD FS-standardmäßig, intern generierte, selbstsignierte Tokensignaturzertifikat Zertifikate.  

**Anforderungen:**
- Wenn Ihre Organisation erforderlich ist, dass Zertifikate von Unternehmens-PKI zum Signieren von Token verwendet werden, dies kann mit dem SigningCertificateThumbprint-Parameter des Cmdlets Install-AdfsFarm.
- Standardmäßig intern generierte Zertifikate verwenden oder extern registrierte Zertifikate, wenn das Tokensignaturzertifikat geändert werden, wird müssen sicherstellen, dass alle vertrauende Seiten mit den neuen Informationen aktualisiert wurden.  Andernfalls tritt ein Anmeldungen alle vertrauenden Seiten, die nicht aktualisiert.

### <a name="token-encryptingdecrypting-certificate"></a>Token Ver- und Entschlüsselung Zertifikat
Dieses Zertifikat wird von Anspruchsanbietern verwendet, die Token ausgestellt für AD FS zu verschlüsseln.

**Empfehlung:** verwenden Sie die AD FS-standardmäßig, intern generierte, selbstsignierte Zertifikate entschlüsseln Token.  

**Anforderungen:**
- Wenn Ihre Organisation erforderlich ist, dass Zertifikate von Unternehmens-PKI zum Signieren von Token verwendet werden, dies kann mit dem DecryptingCertificateThumbprint-Parameter des Cmdlets Install-AdfsFarm.
- Standardmäßig intern generierte Zertifikate verwenden oder extern registrierte Zertifikate, wenn das Token entschlüsseln Zertifikats geändert werden, wird müssen sicherstellen, dass alle Anspruchsanbietern mit den neuen Informationen aktualisiert wurden.  Andernfalls tritt ein Anmeldungen verwenden alle Ansprüche Anbieter nicht aktualisiert.
  
> [!CAUTION]  
> Zertifikate, die zum Signieren von Token\ und Token\-Decrypting\/Verschlüsseln von verwendet werden, sind entscheidend für die Stabilität des Verbunddiensts. Kunden, die ihre eigenen Zertifikate Token\-Signierung und Token\-Decrypting\/Verschlüsselung verwalten sollten sicherstellen, dass diese Zertifikate gesichert werden und unabhängig während einer Wiederherstellungsereignis stehen.  

### <a name="user-certificates"></a>Benutzerzertifikate
- Wenn Sie X509 verwenden, für die benutzerzertifikatauthentifizierung mit AD FS, Zertifikate für alle Benutzer mit einer Stammzertifizierungsstelle verkettet muss, die vom AD FS und Web Application Proxy Server als vertrauenswürdig eingestuft wird.

## <a name="BKMK_2"></a>Hardwareanforderungen  
AD FS und Web Application Proxy Hardwareanforderungen (physisch oder virtuell) sind auf CPU, abgegrenzter, damit Sie die Größe der Farm für die Verarbeitung von Kapazität sollten.  
- Verwenden der [AD FS 2016 Capacity Planning Kalkulationstabelle](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx) die Anzahl der AD FS und Web Application Proxy Server festlegen müssen.

Die Arbeitsspeicher- und Anforderungen für AD FS relativ statisch sind, finden Sie in der folgenden Tabelle:


|**Die Hardware**|**Mindestanforderung**|**Empfehlung**|
|----- | ----- |-----|
|RAM|2GB|4GB |
|Speicherplatz|32GB|100GB |

**SQL Server-Hardwareanforderungen**

Wenn Sie SQL Server für Ihre AD FS-Konfigurationsdatenbank verwenden, die Größe der SQL Server gemäß der grundlegendsten SQL Server-Empfehlungen.  Die Größe der AD FS-Datenbank ist sehr klein und AD FS installieren eine erhebliche Arbeitslast nicht auf die Datenbankinstanz.  AD FS vorhanden ist, jedoch Verbinden mit der Datenbank mehrere Male bei einer Authentifizierung, daher sollte die Netzwerkschnittstelle stabile sein.  SQL Azure wird für die AD FS-Konfigurationsdatenbank leider nicht unterstützt.
  
## <a name="BKMK_3"></a>Proxy-Anforderungen  
  
-   Für den Extranetzugriff, müssen Sie die Webanwendungsproxy-Rollendienst bereitstellen \ - Teil der Remotezugriffs-Serverrolle. 

-   Drittanbieter-Proxys müssen unterstützen die [MS-ADFSPIP Protokoll](https://msdn.microsoft.com/en-us/library/dn392811.aspx) als AD FS-Proxy unterstützt werden müssen.  Eine Liste der 3rd Party Anbietern finden Sie unter der [häufig gestellte Fragen zu](AD-FS-FAQ.md#what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip).

-   AD FS 2016 sind Web Application Proxy Server unter Windows Server2016 erforderlich.  Downlevel Proxy kann für ein Verhalten 2016 Farmebene mit AD FS 2016-Farm konfiguriert werden.
  
-   Verbundserver und den Webanwendungsproxy-Rollendienst können auf demselben Computer installiert werden.  
  
## <a name="BKMK_4"></a>AD DS-Anforderungen  
**Anforderungen an den Domänencontroller**  
  
- AD FS ist Domänencontroller unter Windows Server 2008 oder höher erforderlich.

- Mindestens Windows Server2016-Domänencontroller ist für Microsoft Passport for Work erforderlich.
  
> [!NOTE]  
> Unterstützung für Umgebungen mit Windows Server2003-Domänencontroller wurde beendet. Besuchen Sie [auf dieser Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) zusätzliche Informationen auf der Microsoft Support Lifecycle.  
  
**Domänenanforderungen Functional\-Ebene**  
  
 - Alle Domänen mit Benutzerkonten und der Domäne an, die die AD FS-Server hinzugefügt werden, müssen auf die Domänenfunktionsebene von Windows Server2003 oder höher ausgeführt werden.  
  
 - Ein Windows Server2008-Domänenfunktionsebene ist oder höher für die Authentifizierung per Clientzertifikat erforderlich, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
**Schema-Anforderungen**  
  
-   Neue Installationen von AD FS 2016 erfordern das Jahr 2016 Active Directory-Schema (Mindestversion 85).

-   Auslösen der AD FS-Farm Verhalten Ebene (FBL) auf die Ebene 2016 muss das Jahr 2016 Active Directory-Schema (Mindestversion 85).  

  
**Dienstkontenanforderungen**  
  
-   Alle standardmäßigen Domänenkonto als Dienstkonto für AD FS dienen. Gruppe von verwalteten Dienstkonten werden ebenfalls unterstützt. Die Berechtigungen zur Laufzeit werden beim Konfigurieren von AD FS automatisch hinzugefügt.

-   Gruppe verwalteter Dienstkonten ist mindestens ein Domänencontroller unter Windows Server 2012 oder höher erforderlich.  Das GMSA muss unter die standardmäßige live "CN = verwaltete Dienstkonten-Container.  

-   Kerberos-Authentifizierung, den Dienstprinzipalnamen '`HOST/<adfs\_service\_name>`"muss auf dem AD FS-Dienstkonto registriert werden. Standardmäßig wird das Konfigurieren von AD FS beim Erstellen einer neuen AD FS-Farm.  Wenn dies fehlschlägt, z.B. bei einem Konflikt oder nicht über ausreichende Berechtigungen, wird eine Warnung angezeigt, und sollten Sie es manuell hinzufügen.  
   
**Domänenanforderungen**  
  
-   Alle AD FS-Server muss zu einer AD DS-Domäne angehören.  
  
-   Alle AD FS-Server in einer Farm müssen in der gleichen Domäne bereitgestellt werden.  
   
**Anforderungen des Multi-Gesamtstruktur**  
  
-   Jede Domäne oder Gesamtstruktur, die Benutzer authentifiziert sich gegenüber des AD FS-Diensts enthält, muss die Domäne, die die AD FS-Server angehören, vertrauen.  

-   Die Gesamtstruktur, der die AD FS-Dienstkonto Mitglied ist, muss alle Benutzer Anmeldung Gesamtstrukturen vertrauen. 
  
-   Der AD FS-Dienstkonto benötigen Berechtigungen zum Lesen von Benutzerattributen in jeder Domäne, die Benutzer authentifiziert sich gegenüber des AD FS-Diensts enthält.  
  
## <a name="BKMK_5"></a>Anforderungen an die Datenbank  
Dieser Abschnittbeschreibt die Anforderungen und Einschränkungen für AD FS-Farmen, die bzw. die Windows Internal Database (WID) oder SQL Server als Datenbank zu verwenden:  
  
**INTERNE WINDOWS-DATENBANK**  
  
-   Das Artefakt Auflösung Profil des SAML 2.0 wird in einer WID-Farm nicht unterstützt.    

-   Erkennung von tokenwiederholungen ist eine Windows-datenbankfarm unterstützt. (Diese Funktion wird nur nur in Szenarien, in dem AD FS als Verbundserverproxy Anbieter fungiert und Speicherressourcen Sicherheitstoken von externen Anspruchsanbietern, verwendet.)  
  
Die folgende Tabelle enthält eine Übersicht darüber, wie viele AD FS-Server sind in einer WID-Vs eine SQL Server-Farm unterstützt.    
  
  
|| 1 – 100 Vertrauensstellungen der vertrauenden Seite (RP) Vertrauensstellungen in AD FS konfiguriert | Mehr als 100 RP Vertrauensstellungen konfiguriert  |
| --- |--- | --- |
|1-30 AD FS-Server|Interne Windows-Datenbank unterstützt|Nicht unterstützt, mit WID - SQL Server erforderlich |
|Mehr als 30 AD FS-Server|Nicht unterstützt, mit WID - SQL Server erforderlich|Nicht unterstützt, mit WID - SQL Server erforderlich  
  
**SqlServer**  
  
- Für AD FS unter Windows Server2016 werden SQL Server2008 und höhere Versionen unterstützt.

- SAML-Artefaktauflösung und Erkennung von tokenwiederholungen werden in einer SQL Server-Farm unterstützt.  
  
## <a name="BKMK_6"></a>Anforderungen an Webbrowser  
Wenn AD FS-Authentifizierung über einen Browser oder ein Webbrowser-Steuerelement ausgeführt wird, muss Ihren Browser die folgenden Anforderungen erfüllen:  
  
-   JavaScript muss aktiviert sein  
  
-   Für einmaliges Anmelden muss der Clientbrowser konfiguriert werden Cookies zulassen  
  
-   Server Name Indication \(SNI\) muss unterstützt werden  
  
-   Für die Benutzer-Zertifikat und Gerät Zertifikatauthentifizierung muss der Browser SSL-Zertifikat Clientauthentifizierung unterstützt.  

-   Für eine nahtlose Anmeldung mithilfe der integrierten Windows-Authentifizierung muss der verbunddienstnamen (z.B. https:\/\/fs.contoso.com) in der Zone für lokales Intranet oder vertrauenswürdige Sites konfiguriert werden.
## <a name="BKMK_7"></a>Netzwerkanforderungen  
 
**Firewallanforderungen**  
  
Firewall zwischen dem Web Application Proxy und die Verbundserverfarm und die Firewall zwischen den Clients und dem Web Application Proxy müssen TCP-Port 443 aktiviert haben eingehende.  
  
Darüber hinaus, wenn Clientbenutzer Authentifizierung Zertifikat \ (ClientTLS-Authentifizierung mithilfe von X509 Benutzer Certificates\) ist erforderlich, und der Endpunkt Certauth auf Port 443 ist nicht aktiviert, AD FS 2016 erfordert, dass TCP-Port 49443 aktiviert werden in der Firewall zwischen den Clients und dem Web Application Proxy eingehende. Dies ist nicht in der Firewall zwischen the Web Application Proxy und die Verbundserverproxy-Server\ erforderlich). 

Weitere Informationen zur Hybrid-Port Anforderungen finden Sie unter [Hybrid-Identität Ports und Protokolle](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports). 

Weitere Informationen finden Sie unter [bewährte Methoden zum Schützen von Active Directory-Verbunddienste](..\deployment\Best-Practices-Securing-AD-FS.md)
  
**DNS-Anforderungen**  
  
-   Für den Intranetzugriff müssen alle Clients, die Zugriff auf AD FS-Dienst in der internen Unternehmensnetzwerk \(intranet\) der AD FS-Dienstname Lastenausgleich für die AD FS-Server oder AD FS-Server auflösen können.  
  
-   Für Extranet-Zugriff muss alle Clients, die Zugriff auf AD FS-Dienst von außerhalb der Unternehmensnetzwerk \(Extranet\/Internet\) der AD FS-Dienst Lastenausgleich für die Web Application Proxy Server oder das Web Application Proxy Server auflösen kann.  
  
-   Jede Web Application Proxy Server in der DMZ muss AD FS-Dienst dem Lastenausgleichsmodul für die AD FS-Server oder AD FS-Server auflösen kann. Dies kann mit einem anderen DNS-Server im DMZ-Netzwerk oder mithilfe der Hostdatei lokaler Server-Auflösung ändern erreicht werden.  
  
-   Für die integrierte Windows-Authentifizierung müssen Sie einen DNS A-Eintrag \(not CNAME\) für den verbunddienstnamen verwenden.  

-   Für die benutzerzertifikatauthentifizierung Port 443 muss "Certauth. \ < Federation Service Tokentypen >" in DNS zum Auflösen in den Verbundserver oder Web Application Proxy konfiguriert werden.

-   Für die Geräteregistrierung oder für moderne-Authentifizierung auf lokalen Ressourcen vor Windows10-Clients verwenden muss "Enterpriseregistration. \ < Upn Suffix\ >", für die einzelnen Benutzerprinzipalnamen-Suffix in Ihrer Organisation an den Verbundserver oder eine webanwendungsproxy beheben konfiguriert werden.

**Load Balancer Anforderungen**
- Der Lastenausgleich muss nicht beendet werden SSL. AD FS unterstützt mehrere Anwendungsfälle mit zertifikatbasierter Authentifizierung die umgebrochen werden, wenn Sie SSL zu beenden. Beenden SSL am Lastenausgleichsmodul wird für alle Anwendungsfall nicht unterstützt. 
- Es wird empfohlen, einen Lastenausgleich zu verwenden, der SNI unterstützt. In den Ereignisdaten werden nicht, verwenden die 0.0.0.0 fallback-Bindung auf AD FS/Web Application Proxy Server sollte eine Problemumgehung bereitstellen.
- Es wird empfohlen, mit der HTTP (nicht HTTPS) Integrität Prüfpunkt Endpunkte Load Balancer integritätsprüfungen Datenverkehr ausgeführt werden. Dadurch werden alle Probleme im Zusammenhang mit SNI vermieden. Die Antwort auf diese Endpunkte Test ist ein HTTP-200 OK und lokal mit keine Abhängigkeit vom Back-End-Dienste bereitgestellt wird. Der HTTP-Test kann über HTTP mit dem Pfad '/ Adfs/Test' zugegriffen werden
    - http://&lt;Web Application Proxy-Namen&gt;/Adfs/Test
    - http://&lt;AD FS-Servername&gt;/Adfs/Test
    - http://&lt;Web Application Proxy-IP-Adresse&gt;/Adfs/Test
    - http://&lt;ADFS-IP-Adresse&gt;/Adfs/Test
- Es wird nicht empfohlen, DNS verwenden Roundrobin als Methode für den Lastenausgleich. Bei dieser Art von Lastenausgleich bietet keine automatisierte Möglichkeit zum Entfernen eines Knotens aus dem Integritäts-Prüfpunkte mit Lastenausgleich. 
- Es wird nicht empfohlen, IP-basierten Sitzung Affinität oder Kurznotiz Sitzungen Authentifizierungsdatenverkehr an AD FS innerhalb der Lastenausgleich zu verwenden. Dies kann eine Überladung bestimmter Knoten führen, wenn Legacy-Authentifizierungsprotokoll für E-Mail-Clients mit Office365 E-Mail-Dienste (Exchange Online) herstellen. 

## <a name="BKMK_13"></a>Erforderliche Berechtigungen  
Der Administrator, der die Installation und die Erstkonfiguration von AD FS durchführt, muss lokale Administratorberechtigungen auf dem AD FS-Server verfügen.  Wenn der lokale Administrator nicht über Berechtigungen zum Erstellen von Objekten in Active Directory verfügt, müssen sie ein Domänenadministrator haben die erforderlichen Active Directory-Objekte erstellen und konfigurieren Sie die AD FS-Farm unter Verwendung des Parameters AdminConfiguration.  
  
  

