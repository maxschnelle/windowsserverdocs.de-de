---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: Anforderungen für AD FS 2016
description: Die softwareanforderungen zum Installieren von Active Directory Federation Services.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e72556f9a630e188b59722e09650f9e48fb6852
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280469"
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen



Es folgen die Anforderungen für die Bereitstellung von AD FS:  
  
-   [Zertifikatanforderungen](ad-fs-requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](ad-fs-requirements.md#BKMK_2)  
  
-   [Proxyanforderungen](ad-fs-requirements.md#BKMK_3)  
  
-   [AD DS-Anforderungen](ad-fs-requirements.md#BKMK_4)  
  
-   [Anforderungen an die Datenbank](ad-fs-requirements.md#BKMK_5)  
  
-   [Browseranforderungen](ad-fs-requirements.md#BKMK_6)  

-   [Netzwerkanforderungen](ad-fs-requirements.md#BKMK_7)  
  
-   [Erforderliche Berechtigungen](ad-fs-requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>Zertifikatanforderungen  
  
### <a name="ssl-certificates"></a>SSL-Zertifikate

Jedem AD FS- und Webanwendungsproxy-Server hat ein SSL-Zertifikat für HTTPS-dienstanforderungen für den Verbunddienst an.  Die Web Application Proxy haben zusätzliche SSL-Zertifikate, Anforderungen an die veröffentlichte Anwendungen.

**Empfehlung:** Verwenden Sie dasselbe SSL-Zertifikat für alle AD FS-Verbundserver und Webanwendung Proxys ein. 

**Anforderungen:**

SSL-Zertifikate auf Verbundservern müssen die folgenden Anforderungen erfüllen.
- Das Zertifikat ist öffentlich vertrauenswürdig (für Bereitstellungen in der Produktion)
- Zertifikat enthält den Wert Server Authentication erweiterten Schlüsselverwendung (EKU)
- Zertifikat enthält den Namen des Verbunddiensts, z. B. "fs.contoso.com" im Betreff oder alternativen Antragstellernamen (SAN)
- Für die Authentifizierung mit Benutzerzertifikat an Port 443 ist "Certauth das Zertifikat enthält. \<verbunddienstname\>", wie z. B."certauth.fs.contoso.com"im SAN
- Für die geräteregistrierung oder für die moderne Authentifizierung auf lokale Ressourcen Prä-Windows 10-Clients verwenden darf die SAN "Enterpriseregistration. \<Upn-Suffix\>"für jede UPN-Suffix in Ihrer Organisation verwendet werden soll.

SSL-Zertifikate auf den Webanwendungsproxy müssen die folgenden Anforderungen erfüllen.
- Wenn der Proxy, um verwendet wird müssen AD FS-Proxy für Anforderungen, die integrierte Windows-Authentifizierung, die SSL-Zertifikat verwenden identisch sein (verwenden Sie den gleichen Schlüssel) als Verbund-Server SSL-Zertifikat
- Wenn die AD FS-Eigenschaft, die "ExtendedProtectionTokenCheck" ist (die Standardeinstellung bei AD FS) aktiviert, muss die SSL-Zertifikat identisch sein (verwenden Sie den gleichen Schlüssel) als Verbund-Server SSL-Zertifikat
- Andernfalls sind die Anforderungen für die SSL-Zertifikat identisch mit denen für den Verbund SSL-Zertifikat

### <a name="service-communication-certificate"></a>Dienstkommunikationszertifikat
Dieses Zertifikat ist nicht erforderlich, für die meisten AD FS-Szenarien einschließlich der Azure AD und Office 365. Standardmäßig konfiguriert AD FS das SSL-Zertifikat, das nach der Erstkonfiguration als das dienstkommunikationszertifikat bereitgestellt.

**Empfehlung:**
- Verwenden Sie das gleiche Zertifikat, wie Sie für SSL verwenden.  

### <a name="token-signing-certificate"></a>Tokensignaturzertifikat
Dieses Zertifikat wird zum Signieren von ausgestellter Tokens für vertrauende Seiten, damit Anwendungen der vertrauenden Seite, dass das Zertifikat erkennen müssen und die dazugehörigen Schlüssel als bekannten und vertrauenswürdigen verwendet. Wenn das token Signieren Zertifikats ändert sich, wie z. B. wenn er abläuft, und Sie ein neues Zertifikat konfigurieren, müssen alle vertrauende Seiten aktualisiert werden.

**Empfehlung:** Verwenden Sie die AD FS-Standard, der intern generierte, selbstsignierte Token-Signaturzertifikate.  

**Anforderungen:**
- Wenn Ihre Organisation erfordert, dass die Zertifikate aus dem Unternehmens-PKI für die Tokensignatur verwendet werden, dies ist möglich mit dem Cmdlet Install-AdfsFarm SigningCertificateThumbprint-Parameter.
- Ob Sie standardmäßig intern generierte Zertifikate verwenden oder extern registrierte Zertifikate, wenn Sie das Tokensignaturzertifikat geändert wird müssen Sie sicherstellen, dass alle vertrauende Seiten mit den neuen Zertifikatsinformationen aktualisiert werden.  Andernfalls schlägt fehl Anmeldungen für alle vertrauenden Seiten, die nicht aktualisiert.

### <a name="token-encryptingdecrypting-certificate"></a>Verschlüsseln/Tokenentschlüsselungszertifikat
Dieses Zertifikat wird von Anspruchsanbietern verwendet, die mit AD FS ausgestellte Token zu verschlüsseln.

**Empfehlung:** Verwenden Sie die AD FS-Standard, der intern generierte, selbstsignierte tokenentschlüsselungszertifikaten.  

**Anforderungen:**
- Wenn Ihre Organisation erfordert, dass die Zertifikate aus dem Unternehmens-PKI für die Tokensignatur verwendet werden, dies ist möglich mit dem Cmdlet Install-AdfsFarm DecryptingCertificateThumbprint-Parameter.
- Ob Sie standardmäßig intern generierte Zertifikate verwenden oder extern registrierte Zertifikate, wenn das Token, das Zertifikat zu entschlüsseln, die Sie geändert wird müssen Sie sicherstellen, dass alle Anspruchsanbietern mit den neuen Zertifikatsinformationen aktualisiert werden.  Andernfalls schlägt fehl Anmeldungen mithilfe einer Anspruchsanbieter-Anbieter, die nicht aktualisiert.
  
> [!CAUTION]  
> Zertifikate, die für Token verwendet werden\-signier- und token\-entschlüsseln\/Verschlüsselung sind entscheidend, um die Stabilität des Verbunddiensts. Kunden verwalten ihre eigenen Token\-Signierung & token\-entschlüsseln\/Verschlüsselungszertifikate sorgen dafür, dass diese Zertifikate gesichert werden und sind unabhängig voneinander während eines Ereignisses für die Wiederherstellung verfügbar.  

### <a name="user-certificates"></a>Benutzerzertifikate
- Wenn Sie X509 verwenden, die Authentifizierung mit Benutzerzertifikat mit AD FS, Zertifikate für alle Benutzer mit einer Stammzertifizierungsstelle verkettet muss, die durch die AD FS- und Webanwendungsproxy-Server als vertrauenswürdig eingestuft wird.

## <a name="BKMK_2"></a>Hardwareanforderungen  
AD FS und Webanwendungsproxy hardwareanforderungen (physisch oder virtuell) sind auf CPU, gated-damit Sie die Größe der Farm für die Verarbeitung von Kapazität sollte.  
- Verwenden der [AD FS 2016 Kapazitätsplanung Arbeitsblatt](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx) um zu bestimmen, die Anzahl der AD FS- und Webanwendungsproxy-Server Sie benötigen.

Die Anforderungen für Arbeitsspeicher- und speicherplatzanforderungen für AD FS relativ statisch sind, finden Sie in der folgenden Tabelle:


|**Hardwareanforderung**|**Mindestanforderung**|**Empfehlung**|
|----- | ----- |-----|
|RAM|2 GB|4 GB |
|Speicherplatz|32 GB|100 GB |

**SQL Server-Hardware-Anforderungen**

Wenn Sie SQL Server für die AD FS-Konfigurationsdatenbank verwenden, die Größe der SQL Server entsprechend den Empfehlungen für die meisten grundlegenden SQL Server.  Die Größe der AD FS-Datenbank ist sehr klein wird, und AD FS keine erhebliche Verarbeitungslast auf die Datenbank-Instanz.  AD FS der Fall ist, jedoch Herstellen einer Verbindung mit der Datenbank mehrere Male während der Authentifizierung, die Netzwerkverbindung stabil sein sollte.  Leider ist SQL Azure, für die AD FS-Konfigurationsdatenbank nicht unterstützt.
  
## <a name="BKMK_3"></a>Proxyanforderungen  
  
-   Für den Extranetzugriff, müssen Sie die Webanwendungsproxy-Rollendienst bereitstellen \- Teil der Serverrolle "Remotezugriff". 

-   Unterstützung von Drittanbieter-Proxys müssen die [MS-ADFSPIP Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) als AD FS-Proxy unterstützt werden müssen.  Eine Liste der 3rd Party Anbietern finden Sie unter den [– häufig gestellte Fragen](AD-FS-FAQ.md#what-third-party-proxies-are-available-for-ad-fs-that-support-ms-adfspip).

-   AD FS 2016 ist die Webanwendungsproxy-Server unter Windows Server 2016 erforderlich.  Ein Downlevel-Proxy kann nicht für eine der verhaltensebene 2016-Farm mit AD FS 2016-Farm konfiguriert werden.
  
-   Verbundserver und den Webanwendungsproxy-Rollendienst können nicht auf demselben Computer installiert werden.  
  
## <a name="BKMK_4"></a>AD DS-Anforderungen  
**Anforderungen an den Domänencontroller**  
  
- AD FS erfordert Domänencontroller mit WindowsServer 2008 oder höher.

- Mindestens ein Windows Server 2016-Domänencontroller ist erforderlich, damit Microsoft Passport for Work.
  
> [!NOTE]  
> Alle Unterstützung für Umgebungen mit Windows Server 2003-Domänencontrollern wurde beendet. Besuchen Sie [auf dieser Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) für Weitere Informationen zu den Microsoft Support-Lebenszyklus.  
  
**Domänenfunktionsebene\-Anforderungen**  
  
 - Alle Domänen-Benutzerkonten und die Domäne, die mit der AD FS-Servern verknüpft sind, müssen auf die Domänenfunktionsebene von Windows Server 2003 oder höher ausgeführt werden.  
  
 - Ein Windows Server 2008-Domänenfunktionsebene ist oder höher für die Authentifizierung per Clientzertifikat erforderlich, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
**Schemaanforderungen**  
  
-   Neue Installationen von AD FS 2016 müssen das Active Directory-2016-Schema (Mindestversion 85).

-   Auslösen von AD FS-Farm Verhalten-Ebene (FBL) auf 2016 ist erforderlich, das Active Directory-2016-Schema (Mindestversion 85).  

  
**Anforderungen an das Dienstkonto**  
  
-   Alle standard-Domänenkonto als Dienstkonto für AD FS dienen. Verwaltete gruppendienstkonten werden ebenfalls unterstützt. Die Berechtigungen, die zur Laufzeit erforderlich werden automatisch hinzugefügt werden, wenn Sie AD FS konfigurieren.

-   Das Zuweisen von Benutzerrechten für das AD-Dienstkonto erforderlich sind, wird "Anmelden als Dienst"

-   Das Zuweisen von Benutzerrechten für die 'NT Service\adfssrv' und "NT Service\drs" erforderlich sind, "Sicherheitsüberprüfung generieren" und "Anmelden als Dienst".

-   Gruppe verwaltete Dienstkonten müssen mindestens einen Domänencontroller unter WindowsServer 2012 oder höher.  Das gruppenverwaltete Dienstkonto muss sind, unter der Standardwert "CN = Managed Service Accounts-Container.  

-   Für die Kerberos-Authentifizierung, Service principal Name "`HOST/<adfs\_service\_name>`" muss auf dem AD FS-Dienstkonto registriert werden. Standardmäßig werden AD FS dies konfigurieren, wenn eine neue AD FS-Farm erstellen.  Wenn dies fehlschlägt, wie z. B. bei einem Konflikt oder keine ausreichenden Berechtigungen, sehen Sie eine Warnung, und sollten Sie sie manuell hinzufügen.  
   
**Domänenanforderungen**  
  
-   Alle AD FS-Server müssen zu einer AD DS-Domäne eingebunden sein.  
  
-   Alle AD FS-Server innerhalb einer Farm müssen in der gleichen Domäne bereitgestellt werden.  
   
**Anforderungen für mehrere Gesamtstrukturen**  
  
-   Jede Domäne oder Gesamtstruktur, die Benutzer, die Authentifizierung bei AD FS-Diensts enthält, muss die Domäne, die mit der AD FS-Servern verknüpft sind vertrauen.  

-   Die Gesamtstruktur, der die AD FS-Dienstkonto Mitglied ist, muss alle Gesamtstrukturen für die Anmeldung von Benutzer vertrauen. 
  
-   Das AD FS-Dienstkonto benötigen Berechtigungen zum Lesen von Benutzerattributen in jeder Domäne, die enthält, Benutzer zu authentifizieren, um AD FS-Diensts.  
  
## <a name="BKMK_5"></a>Anforderungen an die Datenbank  
Dieser Abschnitt beschreibt die Anforderungen und Einschränkungen für AD FS-Farmen, die die Windows Internal Database (WID) oder SQL Server wie die Datenbank verwenden:  
  
**WID**  
  
-   Das Artefakt Auflösung-Profil des SAML 2.0 wird in einer WID-Farm nicht unterstützt.    

-   Erkennung von tokenwiederholungen ist eine WID-Farm unterstützt. (Diese Funktion wird nur nur in Szenarien, in dem AD FS fungiert als verbundanbieter ist, und Nutzen von Sicherheitstoken von externen Anspruchsanbietern, verwendet.)  
  
Die folgende Tabelle enthält einen Überblick darüber, wie viele AD FS-Server unterstützt in einer WID-Visual Studio eine SQL Server-Farm.    
  
  
|| 1 - 100, die vertrauenden Seite (Relying Party, RP) Vertrauensstellungen in AD FS konfiguriert | Mehr als 100 RP-Vertrauensstellungen konfiguriert  |
| --- |--- | --- |
|1-30 AD FS-Server|WID unterstützt|Nicht unterstützt, mit WID - SQL-Server, die erforderlich sind |
|Mehr als 30 AD FS-Server|Nicht unterstützt, mit WID - SQL-Server, die erforderlich sind|Nicht unterstützt, mit WID - SQL-Server, die erforderlich sind  
  
**SQL Server**  
  
- Für AD FS unter Windows Server 2016 werden SQL Server 2008 und höheren Versionen unterstützt.

- Sowohl die SAML-artefaktauflösung als auch die Erkennung einer tokenmehrfachverwendung werden in einer SQL Server-Farm unterstützt.  
  
## <a name="BKMK_6"></a>Browseranforderungen  
Wenn AD FS-Authentifizierung über einen Browser bzw. ein Webbrowser-Steuerelement ausgeführt wird, muss Ihr Browser die folgenden Anforderungen erfüllt werden:  
  
- JavaScript muss aktiviert sein  
  
- Für einmaliges Anmelden muss der Clientbrowser konfiguriert werden Cookies zulassen  
  
- Server Name Indication \(SNI\) unterstützt werden müssen  
  
- Für die Benutzer-Zertifikat & ät Zertifikatauthentifizierung muss der Browser unterstützt SSL-Clientzertifikatauthentifizierung  

- Für die nahtlose Anmeldung mithilfe der integrierten Windows-Authentifizierung, dem Namen des Verbunddiensts (z. B. Https:\/\/"FS.contoso.com") muss in der lokalen Intranetzone oder der Zone vertrauenswürdiger Sites konfiguriert sein.
  ## <a name="BKMK_7"></a>Netzwerkanforderungen  
 
**Firewallanforderungen**  
  
Sowohl die Firewall zwischen Webanwendungsproxy und der Verbundserverfarm und der Firewall zwischen den Clients und des Webanwendungsproxys müssen TCP-Port 443 aktiviert eingehende.  
  
Darüber hinaus, wenn der Clientbenutzer-Zertifikatauthentifizierung \(ClientTLS-Authentifizierung mit X509 Benutzerzertifikate\) ist erforderlich, und die Certauth-Endpunkt an Port 443 ist nicht aktiviert, AD FS 2016 erfordert, dass TCP-Port 49443 verwendet eingehende Daten Sie in der Firewall zwischen den Clients und des Webanwendungsproxys. Dies ist nicht erforderlich, in der Firewall zwischen dem Webanwendungsproxy und den Verbundservern\). 

Weitere Informationen zur Hybrid-Ports finden Sie unter [Hybrid Identity Ports und Protokolle](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports). 

Weitere Informationen finden Sie [bewährte Methoden zum Schützen von Active Directory Federation Services](../deployment/Best-Practices-Securing-AD-FS.md)
  
**DNS-Anforderungen**  
  
-   Für den Intranetzugriff, alle Clients, die Zugriff auf AD FS-Dienst im internen Unternehmensnetzwerk \(Intranet\) muss in der Lage, den AD FS-Dienstnamen für den Load Balancer für die AD FS-Server oder dem AD FS-Server aufzulösen.  
  
-   Für den Extranetzugriff, alle Clients, die Zugriff auf AD FS-Diensts über außerhalb des Unternehmensnetzwerks \(extranet\/Internet\) muss der AD FS-Dienstname in der Load Balancer für den Webanwendungsproxy-Servern aufgelöst werden oder der Webanwendungsproxy-Server.  
  
-   Jedem Webanwendungsproxy-Server in der DMZ muss AD FS-Dienstnamen in der Load Balancer für den AD FS-Servern oder AD FS-Servers auflösen können. Dies kann erreicht werden, verwenden einen alternativen DNS-Server in der DMZ-Netzwerk oder lokalen Server Auflösung mithilfe der HOSTS-Datei ändern.  
  
-   Für integrierte Windows-Authentifizierung, müssen Sie einen DNS-A-Eintrag verwenden \(nicht CNAME\) für den Namen des Verbunddiensts.  

-   Für die Authentifizierung mit Benutzerzertifikat an Port 443 "Certauth. \<verbunddienstname\>"muss im DNS zum Auflösen in den Verbund-Server oder Web-Anwendungsproxy konfiguriert werden.

-   Für die geräteregistrierung oder für die moderne Authentifizierung zu lokalen Ressourcen mithilfe der Prä-Windows 10-Clients "Enterpriseregistration. \<Upn-Suffix\>", für jede UPN-Suffix verwendet, die in Ihrer Organisation muss konfiguriert werden, um in den Verbund-Server oder Web-Anwendungsproxy aufzulösen.

**Lastenausgleichsmodule**
- Der Load Balancer darf nicht SSL zu beenden. AD FS unterstützt mehrere Anwendungsfälle mit zertifikatbasierter Authentifizierung die unterbricht, wenn SSL zu beenden. Beenden von SSL auf dem Load Balancer wird für jeden Anwendungsfall nicht unterstützt. 
- Es wird empfohlen, einen Load Balancer zu verwenden, der unterstützt SNI. Im Ereignis nicht, verwenden das fallback-Bindung für AD FS "0.0.0.0" / Web Application Proxy-Server sollte dieses Problem zu umgehen bereitstellen.
- Es wird empfohlen, mit der Integritätstest-Endpunkte HTTP (nicht HTTPS) Load Balancer-integritätsprüfungen für die Weiterleitung des Datenverkehrs durchführen. Dies vermeidet Probleme im Zusammenhang mit SNI. Die Antwort, die diesen Endpunkten Test ist eine HTTP 200 OK und lokal mit keine Abhängigkeit mehr von Back-End-Diensten bereitgestellt wird. Der HTTP-Test kann über HTTP mit dem Pfad "/ Adfs/Probe" zugegriffen werden
    - http://&lt;Namen für Webanwendungsproxy &gt; /Adfs/Probe
    - http://&lt;AD FS-Servername &gt; /Adfs/Probe
    - http://&lt;Web Application Proxy-IP-Adresse &gt; /Adfs/Probe
    - http://&lt;ADFS IP-Adresse &gt; /Adfs/Probe
- Es wird nicht empfohlen, DNS zu verwenden Roundrobin als Methode für den Lastenausgleich. Verwenden diese Art von Lastenausgleich bietet keine automatisierte Möglichkeit zum Entfernen eines Knotens aus dem Load Balancer mit Integritätstests. 
- Es wird nicht empfohlen, IP-basierten sitzungsaffinität oder persistente Sitzungen für den Authentifizierungsdatenverkehr mit AD FS innerhalb der Load Balancer verwenden. Dies kann eine Überladung von bestimmten Knoten führen, bei der älteren Authentifizierungsprotokoll für die e-Mail-Clients mit Office 365 (Exchange Online)-e-Mail-Diensten herstellen. 

## <a name="BKMK_13"></a>Erforderliche Berechtigungen  
Der Administrator, der die Installation und die Erstkonfiguration von AD FS durchführt, muss lokale Administratorberechtigungen auf dem AD FS-Server verfügen.  Wenn der lokale Administrator keine Berechtigungen zum Erstellen von Objekten in Active Directory, müssen sie ein Domänenadministrator haben die erforderlichen Active Directory-Objekte erstellen, und konfigurieren Sie AD FS-Farm mit dem AdminConfiguration-Parameter.  
  
  

