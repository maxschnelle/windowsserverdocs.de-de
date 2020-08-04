---
ms.assetid: 28f4a518-1341-4a10-8a4e-5f84625b314b
title: Anforderungen für AD FS 2016
description: Anforderungen für die Installation der Active Directory-Verbunddienste (AD FS).
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/06/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d44213c8ea477cee7400eb24f9e855d7ad0c2971
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519699"
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen

Im Folgenden sind die Anforderungen für die Bereitstellung von AD FS aufgeführt:

-   [Zertifikatanforderungen](ad-fs-requirements.md#BKMK_1)

-   [Hardwareanforderungen](ad-fs-requirements.md#BKMK_2)

-   [Proxyanforderungen](ad-fs-requirements.md#BKMK_3)

-   [AD DS-Anforderungen](ad-fs-requirements.md#BKMK_4)

-   [Anforderungen an die Konfigurationsdatenbank](ad-fs-requirements.md#BKMK_5)

-   [Browseranforderungen](ad-fs-requirements.md#BKMK_6)

-   [Netzwerkanforderungen](ad-fs-requirements.md#BKMK_7)

-   [Berechtigungsanforderungen](ad-fs-requirements.md#BKMK_13)

## <a name="certificate-requirements"></a><a name="BKMK_1"></a>Zertifikatanforderungen

### <a name="ssl-certificates"></a>SSL-Zertifikate

Jeder AD FS- und Webanwendungsproxy-Server verfügt über ein SSL-Zertifikat, um HTTPS-Anforderungen an den Verbunddienst zu bedienen.  Der Webanwendungsproxy kann über zusätzliche SSL-Zertifikate für Dienstanforderungen an veröffentlichte Anwendungen verfügen.

**Empfehlung:** Verwende dasselbe SSL-Zertifikat für alle AD FS-Verbundserver und Webanwendungsproxys.

**Anforderungen:**

SSL-Zertifikate auf Verbundservern müssen die folgenden Anforderungen erfüllen
- Zertifikat ist öffentlich vertrauenswürdig (für Bereitstellungen in der Produktionsumgebung)
- Das Zertifikat enthält den EKU-Wert (Enhanced Key Usage) für die Serverauthentifizierung
- Das Zertifikat enthält den Namen des Verbunddiensts, z. B. „fs.contoso.com“ im Betreff oder im alternativen Antragstellername (SAN)
- Für die Benutzerzertifikatauthentifizierung an Port 443 enthält das Zertifikat „certauth.\<federation service name\>“, z. B. „certauth.fs.contoso.com“, im SAN
- Für die Geräteregistrierung oder für die moderne Authentifizierung an lokalen Ressourcen unter Verwendung von Vor-Windows 10-Clients muss das SAN „enterpriseregistration.\<upn suffix\>“ für jedes in Ihrer Organisation verwendete UPN-Suffix enthalten.

SSL-Zertifikate auf dem Webanwendungsproxy müssen die folgenden Anforderungen erfüllen
- Wenn der Proxy für AD FS-Anforderungen eingesetzt wird, die die integrierte Windows-Authentifizierung verwenden, muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbundservers identisch sein (verwende denselben Schlüssel).
- Wenn die AD FS-Eigenschaft „ExtendedProtectionTokenCheck“ aktiviert ist (die Standardeinstellung in AD FS), muss das Proxy-SSL-Zertifikat mit dem SSL-Zertifikat des Verbundservers identisch sein (verwende denselben Schlüssel).
- Andernfalls sind die Anforderungen für das Proxy-SSL-Zertifikat dieselben wie die für das SSL-Zertifikat des Verbundservers.

### <a name="service-communication-certificate"></a>Dienstkommunikationszertifikat
Dieses Zertifikat ist für die meisten AD FS-Szenarien, einschließlich Azure AD und Office 365, nicht erforderlich.
Standardmäßig konfiguriert AD FS das bei der Erstkonfiguration bereitgestellte SSL-Zertifikat als Dienstkommunikationszertifikat.

**Empfehlung:**
- Verwende dasselbe Zertifikat, das du für SSL verwendest.

### <a name="token-signing-certificate"></a>Tokensignaturzertifikat
Dieses Zertifikat wird verwendet, um ausgegebene Token an vertrauende Seiten zu signieren, sodass Anwendungen von vertrauenden Seiten das Zertifikat und den zugehörigen Schlüssel als bekannt und vertrauenswürdig erkennen müssen. Wenn sich das Tokensignaturzertifikat ändert (wenn es z. B. abläuft und du ein neues Zertifikat konfigurierst), müssen alle beteiligten Seiten aktualisiert werden.

**Empfehlung:** Verwende die standardmäßigen, intern generierten, selbstsignierten AD FS-Tokensignaturzertifikate.

**Anforderungen:**
- Wenn die Organisation die Verwendung von Zertifikaten aus der Unternehmens-PKI für die Tokensignatur erfordert, kann dies mit dem SigningCertificateThumbprint-Parameter des Cmdlets „Install-AdfsFarm“ erfolgen.
- Unabhängig davon, ob du die intern generierten Standardzertifikate oder extern registrierte Zertifikate verwendest, musst du bei einer Änderung des Tokensignaturzertifikats sicherstellen, dass alle Seiten, die sich auf das Zertifikat verlassen, mit den neuen Zertifikatsinformationen aktualisiert werden.  Andernfalls treten bei der Anmeldung aller abhängigen Seiten, die nicht aktualisiert wurden, Fehler auf.

### <a name="token-encryptingdecrypting-certificate"></a>Zertifikat zur Verschlüsselung/Entschlüsselung von Token
Dieses Zertifikat wird von Anspruchsanbietern verwendet, die an AD FS ausgegebene Token verschlüsseln.

**Empfehlung:** Verwende die standardmäßigen, intern generierten, selbstsignierten AD FS-Tokenentschlüsselungszertifikate.

**Anforderungen:**
- Wenn die Organisation die Verwendung von Zertifikaten aus der Unternehmens-PKI für die Tokensignatur erfordert, kann dies mit dem DecryptingCertificateThumbprint-Parameter des Cmdlets „Install-AdfsFarm“ erfolgen.
- Unabhängig davon, ob du die intern generierten Standardzertifikate oder extern registrierte Zertifikate verwendest, musst du bei einer Änderung des Tokenentschlüsselungszertifikats sicherstellen, dass alle Anspruchanbieter mit den neuen Zertifikatsinformationen aktualisiert werden.  Andernfalls treten bei Anmeldungen, die beliebige nicht aktualisierte Anspruchsanbieter verwenden, entsprechende Fehler auf.

> [!CAUTION]
> Zertifikate, die für die Tokensignatur und die Tokenentschlüsselung bzw. -verschlüsselung verwendet werden, sind wichtig für die Stabilität des Verbunddiensts. Kunden, die ihre eigenen Zertifikate für Tokensignatur und Tokenentschlüsselung bzw. -verschlüsselung verwalten, sollten sicherstellen, dass diese Zertifikate gesichert werden und während eines Wiederherstellungsereignisses unabhängig voneinander verfügbar sind.

### <a name="user-certificates"></a>Benutzerzertifikate
- Bei Verwendung der x509-Benutzerzertifikatauthentifizierung mit AD FS müssen alle Benutzerzertifikate zu einer Stammzertifizierungsstelle führen, der die Active Directory-Verbunddienste (AD FS) und Webanwendungsproxy-Server vertrauen.

## <a name="hardware-requirements"></a><a name="BKMK_2"></a>Hardwareanforderungen
Die Hardwareanforderungen für AD FS und den Webanwendungsproxy (physisch oder virtuell) werden auf die CPU abgegrenzt, daher solltest du die Größe deiner Farm auf die Verarbeitungskapazität ausrichten.
- Verwende das Tabellenblatt [Kapazitätsplanung für AD FS 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx), um die Anzahl der benötigten AD FS- und Webanwendungsproxy-Server zu bestimmen.

Die Anforderungen an Arbeitsspeicher und Datenträger für AD FS sind relativ statisch. Weitere Informationen sind in der nachfolgenden Tabelle enthalten:


|**Hardwareanforderung**|**Mindestanforderung**|**Empfohlene Anforderung**|
|----- | ----- |-----|
|RAM|2 GB|4 GB |
|Speicherplatz|32 GB|100 GB |

**Hardwareanforderungen von SQL Server**

Wenn du SQL Server für die AD FS-Konfigurationsdatenbank verwendest, dimensioniere den SQL Server entsprechend den grundlegendsten SQL Server-Empfehlungen.  Die AD FS-Datenbank ist sehr klein, und AD FS belastet die Datenbankinstanz nicht wesentlich bei der Verarbeitung.  AD FS verbindet sich jedoch während einer Authentifizierung mehrfach mit der Datenbank, sodass die Netzwerkverbindung zuverlässig sein sollte.  Leider wird SQL Azure für die AD FS-Konfigurationsdatenbank nicht unterstützt.

## <a name="proxy-requirements"></a><a name="BKMK_3"></a>Proxyanforderungen

-   Für den Extranetzugriff muss der Webanwendungsproxy-Rollendienst \- als Teil der Remotezugriffs-Serverrolle bereitgestellt werden.

-   Proxys von Drittanbietern müssen das [MS-ADFSPIP-Protokoll](/openspecs/windows_protocols/ms-adfspip/76deccb1-1429-4c80-8349-d38e61da5cbb) unterstützen, um als AD FS-Proxy unterstützt zu werden.  Eine Liste von Drittanbietern findest du unter [Häufig gestellte Fragen (FAQ)](AD-FS-FAQ.md).

-   AD FS 2016 erfordert Webanwendungsproxy-Server unter Windows Server 2016.  Ein Proxy der Vorgängerversion kann nicht für eine AD FS 2016-Farm konfiguriert werden, die auf der Farmverhaltensebene 2016 ausgeführt wird.

-   Ein Verbundserver und der Webanwendungsproxy-Rollendienst können nicht auf demselben Computer installiert werden.

## <a name="ad-ds-requirements"></a><a name="BKMK_4"></a>AD DS-Anforderungen
**Anforderungen an den Domänencontroller**

- AD FS erfordert Domänencontroller mit Windows Server 2008 oder höher.

- Für Microsoft Passport for Work ist mindestens ein Windows Server 2016-Domänencontroller erforderlich.

> [!NOTE]
> Sämtliche Unterstützung für Umgebungen mit Windows Server 2003-Domänencontrollern wurde eingestellt. Besuche [diese Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO), um weitere Informationen über den Microsoft Support Lifecycle zu erhalten.

**Anforderungen auf Domänenfunktionsebene**

 - Alle Benutzerkontodomänen und die Domäne, mit der die AD FS-Server verbunden sind, müssen auf der Domänenfunktionsebene von Windows Server 2003 oder höher betrieben werden.

 - Die Windows Server 2008-Domänenfunktionsebene oder höher ist für die Clientzertifikatauthentifizierung erforderlich, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.

**Schemaanforderungen**

-   Neue Installationen von AD FS 2016 erfordern das Active Directory 2016-Schema (mindestens Version 85).

-   Das Heraufsetzen der AD FS-Farmverhaltensebene auf die Ebene von 2016 erfordert das Active Directory 2016-Schema (mindestens Version 85).


**Dienstkontenanforderungen**

-   Jedes Standarddomänenkonto kann als Dienstkonto für AD FS verwendet werden. Über Gruppen verwaltete Dienstkonten werden ebenfalls unterstützt. Die zur Laufzeit erforderlichen Berechtigungen werden automatisch hinzugefügt, wenn du AD FS konfigurierst.

-   Die für das AD-Dienstkonto erforderliche Zuweisung von Benutzerrechten lautet „Anmelden als Dienst“.

-   Die für „NT Service\adfssrv“ und „NT Service\drs“ erforderliche Zuweisung von Benutzerrechten lautet „Generieren von Sicherheitsüberwachungen“ und „Anmelden als Dienst“.

-   Für über Gruppen verwaltete Dienstkonten ist mindestens ein Domänencontroller mit Windows Server 2012 oder höher erforderlich.  Die GMSA muss sich unter dem Standardcontainer „CN=Managed Service Accounts“ befinden.

-   Für die Kerberos-Authentifizierung muss der Dienstprinzipalname „`HOST/<adfs\_service\_name>`“ für das AD FS-Dienstkonto registriert werden. Standardmäßig wird dies von AD FS beim Erstellen einer neuen AD FS-Farm konfiguriert.  Wenn dies fehlschlägt, z. B. bei Konflikten oder unzureichenden Berechtigungen, wird eine Warnung angezeigt und du solltest sie dann manuell hinzufügen.

**Domänenanforderungen**

-   Alle AD FS-Server müssen einer AD DS-Domäne beigetreten sein.

-   Alle AD FS-Server innerhalb einer Farm müssen in derselben Domäne bereitgestellt werden.

**Anforderungen für mehrere Gesamtstrukturen**

-   Die Domäne, der die AD FS-Server beigetreten sind, muss jeder Domäne oder Gesamtstruktur vertrauen, die Benutzer enthält, die sich gegenüber dem AD FS-Dienst authentifizieren.

-   Die Gesamtstruktur, bei der das AD FS-Dienstkonto ein Mitglied ist, muss allen Gesamtstrukturen für die Benutzeranmeldung vertrauen.

-   Das AD FS-Dienstkonto muss über Berechtigungen zum Lesen von Benutzerattributen in jeder Domäne verfügen, die Benutzer enthält, die sich gegenüber dem AD FS-Dienst authentifizieren.

## <a name="configuration-database-requirements"></a><a name="BKMK_5"></a>Anforderungen an die Konfigurationsdatenbank
In diesem Abschnitt werden die Anforderungen und Einschränkungen für AD FS-Farmen beschrieben, die als Datenbank die interne Windows-Datenbank (WID) oder SQL Server verwenden:

**WID**

-   Das Artefaktauflösungsprofil von SAML 2.0 wird in einer WID-Farm nicht unterstützt.

-   Die Tokenwiederholungserkennung wird in einer WID-Farm nicht unterstützt. (Diese Funktionalität wird nur in Szenarien verwendet, in denen AD FS als Verbundanbieter fungiert und Sicherheitstoken von externen Anspruchsanbietern verbraucht).

Die folgende Tabelle bietet eine Übersicht, wie viele AD FS-Server in einer WID-Farm im Vergleich zu einer SQL Server-Farm unterstützt werden.

| 1–100 Vertrauensstellungen der vertrauenden Seite (RP) | Mehr als 100 Vertrauensstellungen der vertrauenden Seite (RP) |
|--|--|
| **1–30 AD FS-Knoten:** Von WID unterstützt | **1–30 AD FS-Knoten:** Bei Verwendung von WID nicht unterstützt – SQL erforderlich |
| **Mehr als 30 AD FS-Knoten:** Bei Verwendung von WID nicht unterstützt – SQL erforderlich | **Mehr als 30 AD FS-Knoten:** Bei Verwendung von WID nicht unterstützt – SQL erforderlich |

**SQL Server**

- Für AD FS in Windows Server 2016 werden SQL Server 2008 und höhere Versionen unterstützt.

- In einer SQL Server-Farm werden sowohl die SAML-Artefaktauflösung als auch die Tokenwiederholungserkennung unterstützt.

## <a name="browser-requirements"></a><a name="BKMK_6"></a>Browseranforderungen
Wenn die AD FS-Authentifizierung über einen Browser oder ein Browsersteuerelement durchgeführt wird, muss der Browser die folgenden Anforderungen erfüllen:

- JavaScript muss aktiviert sein

- Für die einmalige Anmeldung muss der Clientbrowser so konfiguriert werden, dass er Cookies zulässt

- Die Servernamensanzeige \(Server Name Indicator, SNI\) muss unterstützt werden

- Für die Benutzerzertifikat- und Gerätezertifikatauthentifizierung muss der Browser die SSL-Clientzertifikatauthentifizierung unterstützen.

- Für eine problemlose Anmeldung unter Verwendung der integrierten Windows-Authentifizierung muss der Name des Verbunddiensts (z. B. https:\/\/fs.contoso.com) in der lokalen Intranetzone oder der Zone der vertrauenswürdigen Sites konfiguriert werden.
  ## <a name="network-requirements"></a><a name="BKMK_7"></a>Netzwerkanforderungen

**Firewallanforderungen**

Sowohl die Firewall zwischen dem Webanwendungsproxy und der Verbundserverfarm als auch die Firewall zwischen den Clients und dem Webanwendungsproxy müssen den TCP-Port 443 für eingehende Daten aktiviert haben.

Wenn die Clientbenutzerzertifikat-Authentifizierung \(clientTLS-Authentifizierung mit X509-Benutzerzertifikaten\) erforderlich ist und der certauth-Endpunkt an Port 443 nicht aktiviert ist, erfordert AD FS 2016 außerdem, dass der TCP-Port 49443 der Firewall zwischen den Clients und dem Webanwendungsproxy für eingehende Daten aktiviert ist. Dies ist bei der Firewall zwischen dem Webanwendungsproxy und den Verbundservern nicht erforderlich.

Weitere Informationen zu den Anforderungen an Hybridports findest du unter [Ports und Protokolle für Hybrididentität](/azure/active-directory/connect/active-directory-aadconnect-ports).

Weitere Informationen findest du unter [Bewährte Methoden für die Sicherung von Active Directory-Verbunddiensten](../deployment/Best-Practices-Securing-AD-FS.md).

**DNS-Anforderungen**

-   Für den Intranetzugriff müssen alle Clients, die auf den AD FS-Dienst innerhalb des internen Unternehmensnetzwerks \(Intranet\) zugreifen, in der Lage sein, den Namen des AD FS-Diensts in den Lastenausgleich für die AD FS-Server oder den AD FS-Server aufzulösen.

-   Für den Extranetzugriff müssen alle Clients, die von außerhalb des Unternehmensnetzwerks \(Extranet\/Internet\) auf den AD FS-Dienst zugreifen, in der Lage sein, den Namen des AD FS-Diensts für den Lastenausgleich für die oder den Webanwendungsproxy-Server aufzulösen.

-   Jeder Webanwendungsproxy-Server in der DMZ muss in der Lage sein, den AD FS-Dienstnamen für den Lastenausgleich für die oder den AD FS-Server aufzulösen. Dies kann über einen alternativen DNS-Server im DMZ-Netzwerk oder durch Änderung der lokalen Serverauflösung mithilfe der HOSTS-Datei erreicht werden.

-   Für die integrierte Windows-Authentifizierung musst du einen DNS-A-Eintrag \(nicht CNAME\) für den Verbunddienstnamen verwenden.

-   Für die Benutzerzertifikatauthentifizierung an Port 443 muss „certauth.\<federation service name\>“ im DNS konfiguriert werden, um in den Verbundserver oder Webanwendungsproxy aufzulösen.

-   Für die Geräteregistrierung oder für die moderne Authentifizierung an lokalen Ressourcen unter Verwendung von Vor-Windows 10-Clients muss „enterpriseregistration.\<upn suffix\>“ für jedes in der Organisation verwendete UPN-Suffix so konfiguriert werden, dass es in den Verbundserver oder Webanwendungsproxy aufgelöst wird.

**Anforderungen an den Lastenausgleich**
- Der Lastenausgleich darf SSL NICHT beenden. AD FS unterstützt mehrere Anwendungsfälle mit Zertifikatsauthentifizierung, die beim Beenden von SSL zu Fehlern führt. Die Beendigung von SSL beim Lastenausgleich wird für keinen Anwendungsfall unterstützt.
- Es wird empfohlen, einen Lastenausgleich zu verwenden, der SNI unterstützt. Falls dies nicht der Fall ist, sollte die Verwendung der Fallbackbindung 0.0.0.0.0 auf deinem AD FS-/Webanwendungsproxy-Server eine Problemumgehung bereitstellen.
- Es wird empfohlen, die HTTP-Integritätstestendpunkte (nicht HTTPS) zu verwenden, um Lastenausgleichs-Integritätsprüfungen für das Routing des Datenverkehrs durchzuführen. Auf diese Weise werden alle Probleme im Zusammenhang mit SNI vermieden. Die Antwort auf diese Testendpunkte ist ein „HTTP 200 OK“ und sie wird lokal ohne Abhängigkeit von Back-End-Diensten bedient. Auf den HTTP-Test kann über HTTP unter dem Pfad „/adfs/probe“ zugegriffen werden.
    - http://&lt;Webanwendungsproxy-Name&gt;/adfs/probe
    - http://&lt;ADFS-Servername&gt;/adfs/probe
    - http://&lt;Webanwendungsproxy-IP-Adresse&gt;/adfs/probe
    - http://&lt;ADFS-IP-Adresse&gt;/adfs/probe
- Es wird NICHT empfohlen, DNS-Roundrobin als eine Möglichkeit zum Lastenausgleich zu verwenden. Die Verwendung dieser Art des Lastenausgleichs bietet keine automatische Möglichkeit, einen Knoten mithilfe von Integritätstests aus dem Lastenausgleich zu entfernen.
- Es wird NICHT empfohlen, die IP-basierte Sitzungsaffinität oder „persistente Sitzungen“ für den Authentifizierungsdatenverkehr zu AD FS innerhalb des Lastenausgleichs zu verwenden. Dies kann zu einer Überlastung bestimmter Knoten führen, wenn das Legacyauthentifizierungsprotokoll für E-Mail-Clients verwendet wird, um eine Verbindung mit den E-Mail-Diensten von Office 365 (Exchange Online) herzustellen.

## <a name="permissions-requirements"></a><a name="BKMK_13"></a>Berechtigungsanforderungen
Der Administrator, der die Installation und die Erstkonfiguration von AD FS durchführt, muss über lokale Administratorrechte auf dem AD FS-Server verfügen.  Wenn der lokale Administrator nicht über die Berechtigung zum Erstellen von Objekten in Active Directory verfügt, muss er zunächst von einem Domänenadministrator die erforderlichen AD-Objekte erstellen lassen und dann die AD FS-Farm mit dem Parameter „AdminConfiguration“ konfigurieren.


