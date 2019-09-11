---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: Anforderungen für AD FS 2016
description: Anforderungen für die Installation von Active Directory-Verbunddienste (AD FS).
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b93848a47eca952ebbeeec2a55c3e6f9b60dbfb8
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865481"
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen



Nachfolgend sind die Anforderungen für die Bereitstellung von AD FS aufgeführt:  
  
-   [Zertifikatanforderungen](ad-fs-requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](ad-fs-requirements.md#BKMK_2)  
  
-   [Proxy Anforderungen](ad-fs-requirements.md#BKMK_3)  
  
-   [AD DS Anforderungen](ad-fs-requirements.md#BKMK_4)  
  
-   [Anforderungen an die Konfigurations Datenbank](ad-fs-requirements.md#BKMK_5)  
  
-   [Browser Anforderungen](ad-fs-requirements.md#BKMK_6)  

-   [Netzwerk Anforderungen](ad-fs-requirements.md#BKMK_7)  
  
-   [Berechtigungsanforderungen](ad-fs-requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>Zertifikat Anforderungen  
  
### <a name="ssl-certificates"></a>SSL-Zertifikate

Jeder AD FS und webanwendungsproxy-Server verfügt über ein SSL-Zertifikat für die HTTPS-Anforderungen an den Verbund Dienst.  Der webanwendungsproxy kann über zusätzliche SSL-Zertifikate verfügen, um Anforderungen an veröffentlichte Anwendungen zu bedienen.

**Sonder** Verwenden Sie das gleiche SSL-Zertifikat für alle AD FS Verbund Server und webanwendungsproxys. 

**Bedingungen**

SSL-Zertifikate auf Verbund Servern müssen die folgenden Anforderungen erfüllen:
- Zertifikat ist öffentlich vertrauenswürdig (für Produktions Bereitstellungen)
- Das Zertifikat enthält den EKU-Wert (Enhanced Key Usage) für die Server Authentifizierung.
- Das Zertifikat enthält den Verbund Dienstnamen, z. b. "FS.contoso.com" im Betreff oder alternativen Antragsteller Namen (San).
- Für die Benutzerzertifikat Authentifizierung auf Port 443 enthält das Zertifikat "certauth. Verbund Dienst Name\>", z. b." certauth.fs.contoso.com "im San \<
- Für die Geräteregistrierung oder die moderne Authentifizierung bei lokalen Ressourcen mithilfe von Clients vor Windows 10 muss das San "enterpriseregistration" enthalten. UPN-\>Suffix "für jedes UPN-Suffix, das in Ihrer Organisation verwendet wird. \<

SSL-Zertifikate auf dem webanwendungsproxy müssen die folgenden Anforderungen erfüllen:
- Wenn der Proxy für die Proxy AD FS Anforderungen verwendet wird, die die integrierte Windows-Authentifizierung verwenden, muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbund Servers identisch sein (verwenden Sie denselben Schlüssel).
- Wenn die AD FS-Eigenschaft "extendedschutztokencheck" aktiviert ist (die Standardeinstellung in AD FS), muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbund Servers identisch sein (verwenden Sie denselben Schlüssel).
- Andernfalls sind die Anforderungen für das Proxy-SSL-Zertifikat identisch mit denen für das SSL-Zertifikat des Verbund Servers.

### <a name="service-communication-certificate"></a>Dienst Kommunikations Zertifikat
Dieses Zertifikat ist für die meisten AD FS Szenarien, einschließlich Azure AD und Office 365, nicht erforderlich. Standardmäßig konfiguriert AD FS das bei der Erstkonfiguration bereitgestellte SSL-Zertifikat als Dienst Kommunikations Zertifikat.

**Sonder**
- Verwenden Sie das Zertifikat, das Sie für SSL verwenden.  

### <a name="token-signing-certificate"></a>Tokensignaturzertifikat
Dieses Zertifikat wird zum Signieren von ausgestellten Token an vertrauende Seiten verwendet, damit Anwendungen der vertrauenden Seite das Zertifikat erkennen und den Schlüssel wie bekannt und vertrauenswürdig erhalten. Wenn sich das Tokensignaturzertifikat ändert (z. b. wenn es abläuft und Sie ein neues Zertifikat konfigurieren), müssen alle vertrauenden Seiten aktualisiert werden.

**Sonder** Verwenden Sie die AD FS standardmäßig generierten, selbst signierten Tokensignaturzertifikate.  

**Bedingungen**
- Wenn Ihre Organisation erfordert, dass Zertifikate aus der Unternehmens-PKI für die Tokensignierung verwendet werden, kann dies mit dem Parameter signingcertifikatethumbprint des Cmdlets install-adfsfarm erfolgen.
- Unabhängig davon, ob Sie die standardmäßigen intern generierten Zertifikate oder extern registrierte Zertifikate verwenden, müssen Sie beim Ändern des Tokensignaturzertifikats sicherstellen, dass alle vertrauenden Seiten mit den neuen Zertifikat Informationen aktualisiert werden.  Andernfalls können Anmeldungen bei nicht aktualisierten vertrauenden Seiten fehlschlagen.

### <a name="token-encryptingdecrypting-certificate"></a>Zertifikatverschlüsselungs-/Entschlüsselungszertifikat
Dieses Zertifikat wird von Anspruchs Anbietern verwendet, die Token verschlüsseln, die für AD FS ausgestellt wurden.

**Sonder** Verwenden Sie die AD FS standardmäßig generierten, selbst signierten tokenentschlüsselungszertifikate.  

**Bedingungen**
- Wenn Ihre Organisation erfordert, dass Zertifikate aus der Unternehmens-PKI für die Tokensignierung verwendet werden, können Sie dies mithilfe des Parameters decryptingcertifigatethumbprint des Cmdlets install-adfsfarm durcharbeiten.
- Unabhängig davon, ob Sie die standardmäßig generierten Zertifikate oder extern registrierten Zertifikate verwenden, müssen Sie, wenn das tokenentschlüsselungszertifikat geändert wird, sicherstellen, dass alle Anspruchs Anbieter mit den neuen Zertifikat Informationen aktualisiert werden.  Andernfalls tritt bei Anmeldungen, die keine aktualisierten Anspruchs Anbieter verwenden, ein Fehler auf.
  
> [!CAUTION]  
> Zertifikate, die für die Tokensignatur\-und die\/tokenentschlüsselungsverschlüsselung\-verwendet werden, sind wichtig für die Stabilität der Verbunddienst. Kunden, die ihre eigene\-Tokensignatur\-& Token zum\/Entschlüsseln verschlüsselter Zertifikate verwalten, sollten sicherstellen, dass diese Zertifikate gesichert werden und während eines Wiederherstellungs Ereignisses unabhängig verfügbar sind.  

### <a name="user-certificates"></a>Benutzerzertifikate
- Bei Verwendung der x. 509-Benutzerzertifikat Authentifizierung mit AD FS müssen alle Benutzerzertifikate an eine Stamm Zertifizierungsstelle verkettet sein, die von den AD FS und webanwendungsproxy-Servern als vertrauenswürdig eingestuft wird

## <a name="BKMK_2"></a>Hardware Anforderungen  
AD FS-und webanwendungsproxy-Hardwareanforderungen (physisch oder virtuell) werden auf der CPU-Größe abgegrenzt, sodass Sie die Größe Ihrer Farm für die Verarbeitungskapazität  
- Verwenden Sie das Arbeitsblatt " [Kapazitätsplanung für AD FS 2016](http://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx) ", um die Anzahl der benötigten AD FS und webanwendungsproxy-Server zu ermitteln

Die Arbeitsspeicher-und Datenträger Anforderungen für AD FS sind recht statisch. Weitere Informationen finden Sie in der folgenden Tabelle:


|**Hardware Anforderung**|**Mindestanforderung**|**Empfohlene Anforderung**|
|----- | ----- |-----|
|RAM|2 GB|4 GB |
|Speicherplatz|32 GB|100 GB |

**SQL Server Hardware Anforderungen**

Wenn Sie SQL Server für die AD FS Konfigurations Datenbank verwenden, können Sie die SQL Server entsprechend den grundlegendsten SQL Server Empfehlungen anpassen.  Die AD FS-Datenbankgröße ist sehr klein, und AD FS führt nicht zu einer erheblichen Verarbeitungs Last für die Daten Bank Instanz.  AD FS stellt jedoch während einer Authentifizierung mehrmals eine Verbindung mit der Datenbank her, sodass die Netzwerkverbindung robust sein sollte.  Leider wird SQL Azure für die AD FS Konfigurations Datenbank nicht unterstützt.
  
## <a name="BKMK_3"></a>Proxy Anforderungen  
  
-   Für den Extranetzugriff müssen Sie den webanwendungsproxy-Rollen Dienst \- Teil der Remote Zugriffs-Server Rolle bereitstellen. 

-   Proxys von Drittanbietern müssen das [MS-adfspip-Protokoll](https://msdn.microsoft.com/library/dn392811.aspx) unterstützen, um als AD FS Proxy unterstützt zu werden.  Eine Liste von Drittanbietern finden Sie [in den häufig](AD-FS-FAQ.md)gestellten Fragen.

-   AD FS 2016 erfordert webanwendungsproxy-Server unter Windows Server 2016.  Ein downlevelproxy kann nicht für eine AD FS 2016-Farm konfiguriert werden, die auf der 2016-Farm Verhaltensebene ausgeführt wird.
  
-   Ein Verbund Server und der webanwendungsproxy-Rollen Dienst können nicht auf demselben Computer installiert werden.  
  
## <a name="BKMK_4"></a>AD DS Anforderungen  
**Domänen Controller Anforderungen**  
  
- AD FS erfordert Domänen Controller, auf denen Windows Server 2008 oder höher ausgeführt wird.

- Mindestens ein Windows Server 2016-Domänen Controller ist für Microsoft Passport for Work erforderlich.
  
> [!NOTE]  
> Die Unterstützung für Umgebungen mit Windows Server 2003-Domänen Controllern wurde beendet. Besuchen Sie [Diese Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) , um weitere Informationen zum Microsoft-Support Lebenszyklus zu erhalten.  
  
**Anforderungen an\-die Domänen Funktionsebene**  
  
 - Alle Benutzerkonto Domänen und die Domäne, der die AD FS Server beitreten, müssen auf der Domänen Funktionsebene von Windows Server 2003 oder höher ausgeführt werden.  
  
 - Eine Windows Server 2008-Domänen Funktionsebene oder höher ist für die Client Zertifikat Authentifizierung erforderlich, wenn das Zertifikat in AD DS explizit einem Benutzerkonto zugeordnet ist.  
  
**Schema Anforderungen**  
  
-   Neue Installationen von AD FS 2016 erfordern das Active Directory 2016-Schema (mindestens Version 85).

-   Für das Erhöhen des AD FS-Farm Verhaltens Level (FBL) auf die 2016-Ebene ist das Active Directory 2016-Schema erforderlich (mindestens Version 85).  

  
**Dienst Kontoanforderungen**  
  
-   Jedes Standard Domänen Konto kann als Dienst Konto für AD FS verwendet werden. Gruppen verwaltete Dienst Konten werden ebenfalls unterstützt. Die zur Laufzeit erforderlichen Berechtigungen werden automatisch hinzugefügt, wenn Sie AD FS konfigurieren.

-   Die für das AD-Dienst Konto erforderliche Zuweisung von Benutzerrechten ist "Anmelden als Dienst".

-   Die für "NT service\adf" und "NT service\drs" erforderlichen Benutzerrechte Zuweisungen sind "Generieren von Sicherheits Überwachungen" und "Anmelden als Dienst".

-   Gruppen verwaltete Dienst Konten erfordern mindestens einen Domänen Controller, auf dem Windows Server 2012 oder höher ausgeführt wird.  Das GMSA muss sich im Standardcontainer "CN = Managed Service Accounts" befinden.  

-   Bei der Kerberos-Authentifizierung muss der Dienst Prinzipal Name "`HOST/<adfs\_service\_name>`" für das AD FS Dienst Konto registriert sein. Standardmäßig konfiguriert AD FS dies, wenn eine neue AD FS Farm erstellt wird.  Wenn dies nicht möglich ist (z. b. bei einem Konflikt oder bei unzureichenden Berechtigungen), wird eine Warnung angezeigt, und Sie sollten Sie manuell hinzufügen.  
   
**Domänen Anforderungen**  
  
-   Alle AD FS Server müssen einer AD DS Domäne beitreten.  
  
-   Alle AD FS Server innerhalb einer Farm müssen in derselben Domäne bereitgestellt werden.  
   
**Anforderungen für mehrere Gesamtstrukturen**  
  
-   Die Domäne, der die AD FS Server beitreten, muss jede Domäne oder Gesamtstruktur vertrauen, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  

-   Die Gesamtstruktur, in der das AD FS-Dienst Konto Mitglied ist, muss allen Benutzer Anmelde-Gesamtstrukturen vertrauen. 
  
-   Das AD FS-Dienst Konto muss über Berechtigungen zum Lesen von Benutzer Attributen in jeder Domäne verfügen, die Benutzer enthält, die sich für den AD FS-Dienst authentifizieren.  
  
## <a name="BKMK_5"></a>Anforderungen an die Konfigurations Datenbank  
In diesem Abschnitt werden die Anforderungen und Einschränkungen für AD FS Farmen beschrieben, die die interne Windows-Datenbank (WID) oder SQL Server als Datenbank verwenden:  
  
**WID**  
  
-   Das artefaktauflösungs Profil von SAML 2,0 wird in einer wid-Farm nicht unterstützt.    

-   Die Erkennung von tokenwiedergabe wird in einer wid-Farm nicht unterstützt (Diese Funktion wird nur in Szenarien verwendet, in denen AD FS als Verbund Anbieter fungiert und Sicherheits Token von externen Anspruchs Anbietern beansprucht.)  
  
Die folgende Tabelle enthält eine Zusammenfassung der Anzahl von AD FS Servern, die in einer wid-oder einer SQL Server Farm unterstützt werden.    
  
  
|| 1-100 in AD FS konfigurierte Vertrauens Stellungen der vertrauenden Seite (RP) | Mehr als 100 RP-Vertrauens Stellungen konfiguriert  |
| --- |--- | --- |
|1-30 AD FS Server|Unterstützt wid|Nicht unterstützt mit wid-SQL Server erforderlich |
|Mehr als 30 AD FS Server|Nicht unterstützt mit wid-SQL Server erforderlich|Nicht unterstützt mit wid-SQL Server erforderlich  
  
**SQL Server**  
  
- Für AD FS in Windows Server 2016 werden SQL Server 2008 und höhere Versionen unterstützt.

- Die SAML-artefaktauflösung und die Erkennung von tokenwiedergabe werden in einer SQL Server-Farm unterstützt.  
  
## <a name="BKMK_6"></a>Browser Anforderungen  
Wenn AD FS Authentifizierung über ein Browser-oder Browser-Steuerelement ausgeführt wird, muss der Browser die folgenden Anforderungen erfüllen:  
  
- JavaScript muss aktiviert sein  
  
- Für einmaliges Anmelden muss der Client Browser so konfiguriert sein, dass Cookies zulässig sind.  
  
- Servernamensanzeige \(SNI\) muss unterstützt werden.  
  
- Bei der Authentifizierung von Benutzer Zertifikaten & Geräte Zertifikaten muss der Browser SSL-Client Zertifikat Authentifizierung unterstützen.  

- Für eine nahtlose Anmeldung mithilfe der integrierten Windows-Authentifizierung muss der Verbund Dienst Name (z.\/b. https:\/FS.contoso.com) in der Zone "Lokales Intranet" oder "Vertrauenswürdige Sites" konfiguriert werden.
  ## <a name="BKMK_7"></a>Netzwerk Anforderungen  
 
**Firewallanforderungen**  
  
Sowohl für die Firewall zwischen dem webanwendungsproxy als auch der Verbund Serverfarm und der Firewall zwischen den Clients und dem webanwendungsproxy muss der TCP-Port 443 in eingehender Richtung aktiviert sein.  
  
Wenn außerdem die \(clienttls-Authentifizierung des Client Benutzer Zertifikats mit X509-Benutzer\) Zertifikaten erforderlich ist und der certauth-Endpunkt an Port 443 nicht aktiviert ist, erfordert AD FS 2016, dass TCP-Port 49443 aktiviert ist. eingehende Daten in der Firewall zwischen den Clients und dem webanwendungsproxy. Dies ist für die Firewall zwischen dem webanwendungsproxy und den Verbund\)Servern nicht erforderlich. 

Weitere Informationen zu den Anforderungen an Hybrid Anschlüsse finden Sie unter [hybride identitätsports und-Protokolle](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports). 

Weitere Informationen finden Sie unter [bewährte Methoden für das Sichern Active Directory-Verbunddienste (AD FS)](../deployment/Best-Practices-Securing-AD-FS.md)
  
**DNS-Anforderungen**  
  
-   Für den Intranetzugriff\) müssen alle Clients, die auf AD FS Dienst \(innerhalb des internen Unternehmensnetzwerks zugreifen, in der Lage sein, den AD FS Dienstnamen in den Load Balancer für die AD FS Server oder den AD FS Server aufzulösen.  
  
-   Für den Extranetzugriff müssen alle Clients, die von außerhalb des Unternehmens \(Netzwerks extranetinternet\/\) auf AD FS-Dienst zugreifen, den AD FS Dienstnamen in den Load Balancer für die webanwendungsproxy-Server auflösen können. der webanwendungsproxy-Server.  
  
-   Jeder webanwendungsproxy-Server in der DMZ muss in der Lage sein, AD FS Dienstnamen in den Load Balancer für die AD FS-Server oder den AD FS-Server aufzulösen. Dies kann mithilfe eines alternativen DNS-Servers im DMZ-Netzwerk oder durch Ändern der Auflösung des lokalen Servers mithilfe der Hosts-Datei erreicht werden.  
  
-   Bei der integrierten Windows-Authentifizierung müssen Sie einen DNS a- \(Datensatz für den\) Verbund Dienstnamen verwenden, der nicht CNAME ist.  

-   Für die Benutzerzertifikat Authentifizierung an Port 443, "certauth. der Verbund Dienst\>Name muss in DNS für die Auflösung auf den Verbund Server oder webanwendungsproxy konfiguriert werden. \<

-   Zur Geräteregistrierung oder zur modernen Authentifizierung bei lokalen Ressourcen mithilfe von Windows 10-Clients vor Windows 10, "enterpriseregistration". UPN-\>Suffix: muss für jedes UPN-Suffix, das in Ihrer Organisation verwendet wird, so konfiguriert werden, dass es auf den Verbund Server oder webanwendungsproxy aufgelöst wird. \<

**Load Balancer Anforderungen**
- Der Load Balancer darf SSL nicht beenden. AD FS unterstützt mehrere Anwendungsfälle mit Zertifikat Authentifizierung, die beim Beenden von SSL abgebrochen werden. Das Beenden von SSL auf dem Load Balancer wird für keinen Anwendungsfall unterstützt. 
- Es wird empfohlen, einen Load Balancer zu verwenden, der SNI unterstützt. Wenn dies nicht der Fall ist, sollte die Verwendung der 0.0.0.0-Fall Back-Bindung auf Ihrem AD FS/webanwendungsproxy-Server eine Problem Umgehung bereitstellen.
- Es wird empfohlen, die Integritätstest-Endpunkte von http (nicht HTTPS) zum Ausführen von Load Balancer-Integritätsprüfungen für den Routing Datenverkehr zu verwenden. Dadurch werden alle Probleme im Zusammenhang mit SNI vermieden. Die Antwort auf diese Test Endpunkte ist ein HTTP 200 OK und wird lokal ohne Abhängigkeit von Back-End-Diensten bereitgestellt. Auf den HTTP-Test kann über HTTP mit dem Pfad "/ADFS/Probe" zugegriffen werden.
    - http://&lt;webanwendungsproxy-Name&gt;/ADFS/Probe
    - http://&lt;ADFS-Server&gt;Name/ADFS/Probe
    - http://&lt;webanwendungsproxy-IP-Adresse&gt;/ADFS/Probe
    - http://&lt;ADFS-IP&gt;-Adresse/ADFS/Probe
- Es wird nicht empfohlen, DNS-Roundrobin als Methode für den Lastenausgleich zu verwenden. Die Verwendung dieser Art von Lastenausgleich bietet keine automatisierte Möglichkeit zum Entfernen eines Knotens aus dem Load Balancer mithilfe von Integritätstests. 
- Es wird nicht empfohlen, IP-basierte Sitzungs Affinität oder persistente Sitzungen zu verwenden, damit der Authentifizierungs Datenverkehr innerhalb des Load Balancers AD FS wird. Dies kann eine Überladung bestimmter Knoten verursachen, wenn das Legacy Authentifizierungsprotokoll verwendet wird, damit e-Mail-Clients eine Verbindung mit Office 365 Mail Services (Exchange Online) herstellen können. 

## <a name="BKMK_13"></a>Berechtigungsanforderungen  
Der Administrator, der die Installation und Erstkonfiguration von AD FS durchführt, muss über lokale Administrator Berechtigungen für den AD FS Server verfügen.  Wenn der lokale Administrator nicht über Berechtigungen zum Erstellen von Objekten in Active Directory verfügt, muss der Domänen Administrator zuerst die erforderlichen AD-Objekte erstellen und dann die AD FS Farm mithilfe des Parameters "AdminConfiguration" konfigurieren.  
  
  

