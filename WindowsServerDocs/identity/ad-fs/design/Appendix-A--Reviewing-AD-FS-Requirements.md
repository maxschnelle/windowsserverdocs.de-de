---
ms.assetid: 39ecc468-77c5-4938-827e-48ce498a25ad
title: "Anhang A – Überprüfen der AD FS-Anforderungen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d5cfb5de77843eebfc152b9c79ac55bab1fa7727
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-a-reviewing-ad-fs-requirements"></a>AnhangA: Überprüfen der AD FS-Anforderungen

>Gilt für: Windows Server 2012

Damit die organisationspartner in Ihrer Active Directory-Verbunddienste (AD FS)-Bereitstellung erfolgreich zusammenarbeiten können, müssen Sie zunächst sicherstellen, dass Ihre unternehmensnetzwerkinfrastruktur für die Unterstützung von AD FS-Anforderungen für Konten, namensauflösung und Zertifikate konfiguriert ist. AD FS hat die folgenden Arten von Anforderungen:  
  
> [!TIP]  
> Finden Sie weitere AD FS-Ressourcenlinks auf die [AD FS-Inhalte](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) Seite auf der Microsoft TechNet-Wiki. Diese Seite wird von Mitgliedern der AD FS-Community verwaltet und regelmäßig vom der AD FS-Produktteam überprüft.  
  
## <a name="hardware-requirements"></a>Hardwareanforderungen  
Die folgenden Mindest- und empfohlenen hardwareanforderungen gelten für den Verbundserver und Verbundserverproxy-Computer.  
  
|Die Hardware|Mindestanforderung|Empfehlung|  
|------------------------|-----------------------|---------------------------|  
|CPU-Geschwindigkeit|Single-Core, 1 Gigahertz (GHz)|Quad-Core, 2 GHz|  
|RAM|1 GB|4GB|  
|Speicherplatz|50 MB|100 MB|  
  
## <a name="software-requirements"></a>Anforderungen der Clientsoftware  
AD FS verwendet Serverfunktionen, die in das Betriebssystem Windows Server® 2012 integriert ist.  
  
> [!NOTE]  
> Die Verbunddienst- und Verbunddienstproxy-Rollendienste können nicht auf demselben Computer ausgeführt werden.  
  
## <a name="certificate-requirements"></a>Zertifikatanforderungen  
Zertifikate spielen äußerst wichtige Rolle beim Sichern der Kommunikation zwischen Verbundservern, Verbundserverproxys, Ansprüche unterstützenden Anwendungen und Webclients. Die Anforderungen für Zertifikate hängt davon ab, ob Sie einen Verbundserver oder Verbundserverproxy-Computer, einrichten, wie in diesem Abschnitt beschrieben.  
  
### <a name="federation-server-certificates"></a>Verbundserverzertifikate  
Verbundserver sind die Zertifikate in der folgenden Tabelle erforderlich.  
  
|Zertifikattyp|Beschreibung|Was Sie vor der Bereitstellung wissen müssen|  
|--------------------|---------------|------------------------------------------|  
|Secure Sockets Layer (SSL)-Zertifikat|Hierbei handelt es sich um ein standardmäßiges Secure Sockets Layer (SSL)-Zertifikat, das zum Sichern der Kommunikation zwischen Verbundservern und Clients verwendet wird.|Dieses Zertifikat muss auf der Standardwebsite in IIS (Internetinformationsdienste) für einen Verbundserver oder a Federation Server Proxy gebunden werden.  Vor der Federation Server Proxy-Assistent erfolgreich ausgeführt wurde, muss für einen Verbundserverproxy die Bindung in IIS konfiguriert werden.<br /><br />**Empfehlung:** da dieses Zertifikat von Clients von AD FS vertrauenswürdig sein muss, verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen (Drittanbieter) Zertifizierungsstelle (CA), z. B. VeriSign ausgestellt wurde. **Tipp:** der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede Instanz von AD FS darzustellen, die Sie bereitstellen. Aus diesem Grund sollten Sie einen Antragstellernamen auf alle neuen Zertifizierungsstelle ausgestellten Zertifikate, die den Namen Ihres Unternehmens oder Ihrer Organisation gegenüber Partnern am besten widerspiegelt.|  
|Dienstkommunikationszertifikat|Mit diesem Zertifikat können WCF-nachrichtensicherheit für das Sichern der Kommunikation zwischen Verbundservern.|Standardmäßig wird das SSL-Zertifikat als dienstkommunikationszertifikat verwendet.  Dies kann mithilfe der AD FS-Verwaltungskonsole geändert werden.|  
|Tokensignaturzertifikat|Hierbei handelt es sich um einen standardmäßigen X509 Zertifikat, das verwendet wird, für die sichere Signierung aller Token, die vom Verbundserver ausgestellt.|Das Tokensignaturzertifikat muss einen privaten Schlüssel enthalten, und es sollte an einen vertrauenswürdigen Stamm im Verbunddienst verketten. Standardmäßig erstellt AD FS ein selbstsigniertes Zertifikat. Allerdings können Sie dies später zu einer Zertifizierungsstelle ausgestelltes Zertifikat ändern, indem mit AD FS-Verwaltungs-Snap-in je nach den Anforderungen Ihrer Organisation.|  
|Tokenentschlüsselungszertifikats|Dies ist ein standardmäßiges SSL-Zertifikat, mit der Entschlüsselung aller eingehenden Token, die von einem Partnerverbundserver verschlüsselt werden. Es wird auch in den Verbundmetadaten veröffentlicht.|Standardmäßig erstellt AD FS ein selbstsigniertes Zertifikat. Allerdings können Sie dies später zu einer Zertifizierungsstelle ausgestelltes Zertifikat ändern, indem mit AD FS-Verwaltungs-Snap-in je nach den Anforderungen Ihrer Organisation.|  
  
> [!CAUTION]  
> Zertifikate, die für die Tokensignatur und Entschlüsselung von Token verwendet werden, sind entscheidend für die Stabilität des Verbunddiensts. Da der Verlust oder die ungeplante Entfernung von Zertifikaten, die für diesen Zweck konfiguriert sind Dienst unterbrechen kann, sollten Sie alle Zertifikate sichern, die für diesen Zweck konfiguriert sind.  
  
Weitere Informationen zu den von Verbundservern verwendeten Zertifikaten finden Sie unter [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md).  
  
### <a name="federation-server-proxy-certificates"></a>Verbundserverproxy-Zertifikate  
Verbundserverproxys erfordern die Zertifikate in der folgenden Tabelle.  
  
|Zertifikattyp|Beschreibung|Was Sie vor der Bereitstellung wissen müssen|  
|--------------------|---------------|------------------------------------------|  
|Serverauthentifizierungszertifikat|Dies ist ein standardmäßiges Secure Sockets Layer (SSL)-Zertifikat, das zum Sichern der Kommunikation zwischen einem Verbundserverproxy und Internet-Client Computern verwendet wird.|Dieses Zertifikat muss die auf der Standardwebsite in IIS (Internetinformationsdienste) gebunden werden, bevor Sie die AD FS-Konfigurationsassistenten für den Verbundserverproxy erfolgreich ausführen können.<br /><br />**Empfehlung:** da dieses Zertifikat von Clients von AD FS vertrauenswürdig sein muss, verwenden Sie ein Serverauthentifizierungszertifikat, das von einer öffentlichen (Drittanbieter) Zertifizierungsstelle (CA), z. B. VeriSign ausgestellt wurde.<br /><br />**Tipp:** der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede Instanz von AD FS darzustellen, die Sie bereitstellen. Aus diesem Grund sollten Sie einen Betreff Namen, die den Namen Ihres Unternehmens oder Ihrer Organisation gegenüber Partnern am besten widerspiegelt.|  
  
Weitere Informationen zu den von Verbundserverproxys verwendeten Zertifikaten finden Sie unter [Certificate Requirements for Federation Server Proxies](Certificate-Requirements-for-Federation-Server-Proxies.md).  
  
## <a name="browser-requirements"></a>Anforderungen an Webbrowser  
Auch wenn jeder aktuelle Webbrowser mit JavaScript-Funktion kann als AD FS-Client funktionieren, haben, die standardmäßig bereitgestellten Webseiten nur Internet Explorer 7.0, 8.0 und 9.0 sowie Mozilla Firefox 3.0 und Safari 3.1 unter Windows getestet. JavaScript muss aktiviert sein, und Cookies müssen für die browserbasierte an- und Abmeldung aktiviert sein ordnungsgemäß funktioniert.  
  
Der AD FS-Produktteam bei Microsoft getestet erfolgreich den Browser und Betriebssystemkonfigurationen in der folgenden Tabelle.  
  
|Browser|Windows 7|Windowsvista|  
|-----------|-------------|-----------------|  
|InternetExplorer 7.0|X|X|  
|InternetExplorer 8.0|X|X|  
|InternetExplorer 9.0|X|Nicht getestet|  
|FireFox 3.0|X|X|  
|Safari 3.1|X|X|  
  
> [!NOTE]  
> AD FS unterstützt sowohl die 32-Bit und 64-Bit-Versionen von allen Browsern, die in der obigen Tabelle angezeigt.  
  
### <a name="cookies"></a>Cookies  
AD FS erstellt sitzungsbasierte und beständige Cookies, die auf Clientcomputern, Anmeldung, Abmeldung, einmaliges Anmelden (SSO) und andere Funktionen bereitzustellen gespeichert werden müssen. Daher muss der Clientbrowser konfiguriert werden, um Cookies zu akzeptieren. Cookies, die für die Authentifizierung verwendet werden, sind immer Secure Hypertext Transfer Protocol (HTTPS)-Sitzungscookies, die für den Ursprungsserver geschrieben werden. Wenn der Clientbrowser nicht konfiguriert ist, um diese Cookies zulassen, können nicht AD FS ordnungsgemäß ausgeführt. Beständige Cookies werden verwendet, um die Benutzerauswahl des Anspruchsanbieters beizubehalten. Sie können sie mithilfe einer Einstellung in der Konfigurationsdatei für die AD FS-Anmeldeseiten deaktivieren.  
  
Unterstützung für TLS/SSL ist aus Gründen der Sicherheit erforderlich.  
  
## <a name="network-requirements"></a>Netzwerkanforderungen  
Konfigurieren entsprechend der folgenden Netzwerkdienste ist wichtig für die erfolgreiche Bereitstellung von AD FS in Ihrer Organisation.  
  
### <a name="tcpip-network-connectivity"></a>TCP/IP-Netzwerkkonnektivität  
Für AD FS ordnungsgemäß funktioniert muss die TCP/IP-Netzwerkkonnektivität zwischen dem Client vorhanden sein. ein Domänencontroller; und die Computer, auf denen der Verbunddienst, den Verbunddienstproxy (Wenn dieser verwendet wird) und die AD FS-Web-Agent gehostet.  
  
### <a name="dns"></a>DNS  
Der primäre Netzwerkdienst, die wichtig für den Betrieb von AD FS, als Active Directory-Domänendienste (AD DS), ist Domain Name System (DNS). Wenn DNS bereitgestellt wird, können Benutzer computeranzeigenamen verwenden, die leicht zu merken, die Verbindung mit Computern und anderen Ressourcen in IP-Netzwerken sind.  
  
 Windows Server 2008 verwendet DNS für die namensauflösung anstellt der Windows Internet Name Service (WINS)-NetBIOS-namensauflösung, die in Windows NT 4.0-basieren Netzwerken verwendet wurde. Es ist immer noch möglich, WINS für Anwendungen, die dies erfordern. Allerdings werden für AD DS und AD FS DNS-namensauflösung erforderlich.  
  
Die Verfahren zum Konfigurieren von DNS zur Unterstützung von AD FS unterschiedlich, je nachdem, ob:  
  
-   Ihre Organisation verfügt bereits über eine vorhandene DNS-Infrastruktur. In den meisten Szenarien ist DNS bereits im gesamten Netzwerk so konfiguriert, dass Browserclients in Ihrem Unternehmensnetzwerk Zugriff auf das Internet haben. Da Internet und die namensauflösung Voraussetzungen von AD FS, wird angenommen, dass diese Infrastruktur für die AD FS-Bereitstellung vorhanden sein.  
  
-   Sie beabsichtigen, Ihrem Unternehmensnetzwerk einen Verbundserver hinzu. Zum Authentifizieren von Benutzern im Unternehmensnetzwerk, müssen interne DNS-Server in der unternehmensnetzwerkgesamtstruktur konfiguriert werden, dass den CNAME des internen Servers zurückgegeben, auf denen der Verbunddienst ausgeführt wird. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   Sie beabsichtigen, Ihrem Unternehmensnetzwerk einen Verbundserverproxy hinzuzufügen. Wenn Sie Benutzerkonten authentifizieren, die sich im Unternehmensnetzwerk Ihrer identitätspartnerorganisation befinden möchten, müssen der interne DNS-Server in der unternehmensnetzwerkgesamtstruktur zurückgeben den CNAME des internen Verbundserverproxys konfiguriert werden. Informationen zur Vorgehensweise beim Konfigurieren von DNS zum Hinzufügen von Verbundserverproxys finden Sie unter [Name Resolution Requirements for Federation Server Proxies](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
-   Sie sind DNS für eine testumgebung einrichten. Wenn Sie AD FS in einer testumgebung, in denen ist kein einzelner Stamm-DNS-Server autoritativ verwenden möchten, ist es wahrscheinlich, dass Sie DNS-Weiterleitungen einrichten, damit Namensabfragen zwischen zwei oder mehr Gesamtstrukturen ordnungsgemäß weitergeleitet werden müssen. Allgemeine Informationen zum Einrichten einer testumgebung für AD FS finden Sie unter [AD FS schrittweise und wie auf Handbüchern](https://go.microsoft.com/fwlink/?LinkId=180357).  
  
## <a name="attribute-store-requirements"></a>Anforderungen an den Attributspeicher  
AD FS muss mindestens ein Attributspeicher für die Authentifizierung von Benutzern und das Extrahieren von Sicherheitsansprüchen für diese Benutzer verwendet werden. Eine Liste der Attribute gespeichert werden, dass AD FS unterstützt, finden Sie unter [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md) in AD FS-Entwurfshandbuch.  
  
> [!NOTE]  
> AD FS erstellt standardmäßig automatisch einen Active Directory-Attributspeicher.  
  
Anforderungen an den Attributspeicher hängen davon ab, ob Ihre Organisation als Kontopartner (die Verbundbenutzer hostet) oder der Ressourcenpartner (die verbundanwendung hostet) verwendet wird.  
  
### <a name="ad-ds"></a>AD DS  
Für AD FS ordnungsgemäß funktioniert müssen auf den Domänencontrollern in der Kontopartnerorganisation oder der Ressourcenpartnerorganisation Windows Server 2003 SP1, Windows Server 2003 R2, Windows Server 2008 oder Windows Server 2012 ausgeführt werden.  
  
Wenn AD FS installiert ist und auf einem Computer einer Domäne konfiguriert wird, ist der Active Directory-benutzerkontenspeicher für diese Domäne als auswählbarer Attributspeicher zur Verfügung gestellt.  
  
> [!IMPORTANT]  
> Da AD FS die Installation von Internet Information Services (IIS) erforderlich ist, empfehlen wir, dass Sie die AD FS-Software auf einem Domänencontroller in einer produktionsumgebung aus Sicherheitsgründen nicht installiert. Diese Konfiguration wird jedoch von Microsoft-Kundensupport-Dienst unterstützt.  
  
#### <a name="schema-requirements"></a>Schema-Anforderungen  
AD FS erfordert keine Änderungen oder Modifikationen, die auf Funktionsebene in AD DS.  
  
#### <a name="functional-level-requirements"></a>Anforderungen an die funktionale Ebene  
Die meisten AD FS-Funktionen erfordern keine AD DS-Funktionsebene Änderungen erfolgreich betrieben werden kann. Ist jedoch Windows Server 2008-Domänenfunktionsebene oder höher erforderlich, damit die Clientzertifikatauthentifizierung erfolgreich betrieben werden kann, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
#### <a name="service-account-requirements"></a>Dienstkontenanforderungen  
Wenn Sie eine Verbundserverfarm erstellen, müssen Sie zunächst ein dediziertes Dienstkonto mit einem domänenbasierten in AD DS erstellen, die den Verbunddienst verwenden können. Später, konfigurieren Sie jeden Verbundserver in der Farm für dieses Konto verwenden. Weitere Informationen hierzu finden Sie unter [manuell konfigurieren eines Dienstkontos für eine Verbundserverfarm](../../ad-fs/deployment/Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) in AD FS-Bereitstellungshandbuch.  
  
### <a name="ldap"></a>LDAP  
Wenn Sie mit anderen Lightweight Directory Access Protocol LDAP-basierten attributspeichern arbeiten, müssen Sie mit einem LDAP-Server verbinden, die die integrierte Windows-Authentifizierung unterstützt. Die LDAP-Verbindungszeichenfolge muss außerdem im Format einer LDAP-URL geschrieben werden, wie in RFC 2255 beschrieben.  
  
### <a name="sql-server"></a>SqlServer  
Für AD FS ordnungsgemäß funktioniert müssen auf Computern, die den Attributspeicher Structured Query Language (SQL) hosten Microsoft SQL Server 2005 oder SQL Server 2008 ausgeführt werden. Wenn Sie mit SQL-basierten attributspeichern arbeiten, müssen Sie außerdem eine Verbindungszeichenfolge konfigurieren.  
  
### <a name="custom-attribute-stores"></a>Benutzerdefinierte Attributspeicher  
Entwickeln Sie benutzerdefinierte Attributspeicher, um erweiterte Szenarien zu ermöglichen. Die für richtliniensprache, die in AD FS integriert ist, kann benutzerdefinierte Attributspeicher verweisen, so, dass eines der folgenden Szenarien verbessert werden kann:  
  
-   Erstellen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
-   Ergänzen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
-   Autorisieren eines Benutzers zum Abrufen eines token  
  
-   Autorisieren eines Diensts zum Abrufen eines Token zum Verhalten eines Benutzers  
  
Wenn Sie mit einem benutzerdefinierten Attributspeicher arbeiten, müssen Sie auch eine Verbindungszeichenfolge konfigurieren. In diesem Fall können Sie alle benutzerdefinierten Code aus, den Sie eingeben, die eine Verbindung mit Ihrem benutzerdefinierten Attributspeicher ermöglicht. Die Verbindungszeichenfolge in dieser Situation ist ein Satz von Name-Wert-Paaren, die vom Entwickler des benutzerdefinierten Attributspeichers Implementierung interpretiert werden.  
  
Weitere Informationen zum Entwickeln und Verwenden von benutzerdefinierten attributspeichern finden Sie unter [Übersicht über Attributspeicher](https://go.microsoft.com/fwlink/?LinkId=190782).  
  
## <a name="application-requirements"></a>Anwendungsanforderungen  
Verbundserver können mit kommunizieren und verbundanwendungen wie Ansprüche unterstützenden Anwendungen zu schützen.  
  
## <a name="authentication-requirements"></a>Authentifizierungsanforderungen  
AD FS integriert natürliche Weise in die vorhandene Windows-Authentifizierung, z. B. Kerberos-Authentifizierung, NTLM, Smartcards und clientseitige x. 509 v3-Zertifikate. Verbundserver verwenden die standard-Kerberos-Authentifizierung zum Authentifizieren von Benutzern gegenüber einer Domäne. Mithilfe der formularbasierte Authentifizierung, Smartcard-Authentifizierung und die integrierte Windows-Authentifizierung, je nachdem, wie Sie die Authentifizierung konfigurieren, können Clients authentifizieren.  
  
Der AD FS Verbundserverproxy-Rolle ermöglicht ein Szenario, in der der Benutzer extern über SSL-Clientauthentifizierung authentifiziert. Sie können auch konfigurieren, die Verbundserver-Rolle zum Erzwingen von SSL-Clientauthentifizierung, obwohl in der Regel die nahtloseste benutzererfahrung erfolgt durch die Konfiguration des kontoverbundservers für die integrierte Windows-Authentifizierung. In dieser Situation hat AD FS keine Kontrolle darüber, welche Anmeldeinformationen der Benutzer für die Windows-desktop-Anmeldung verwendet.  
  
### <a name="smart-card-logon"></a>Smartcard-Anmeldung  
Obwohl AD FS den Typ der Anmeldeinformationen, die für die Authentifizierung (Kennwörter, SSL-Clientauthentifizierung oder integrierte Windows-Authentifizierung) verwendet erzwingen können, wird es Authentifizierung mit Smartcards nicht direkt erzwungen. Aus diesem Grund bietet AD FS eine clientseitige Benutzeroberfläche (UI) keine Smartcard-Anmeldeinformationen (Number, PIN) erhalten. Dies ist, da Windows-basierte Clients absichtlich keine Anmeldeinformationen Benutzerdetails Verbundserver oder Webserver bereitstellen.  
  
### <a name="smart-card-authentication"></a>Smartcard-Authentifizierung  
Smartcard-Authentifizierung verwendet das Kerberos-Protokoll, um die Authentifizierung bei einem Kontoverbundserver. AD FS kann nicht erweitert werden, um neue Authentifizierungsmethoden hinzuzufügen. Das Zertifikat auf der Smartcard ist nicht erforderlich, an einen vertrauenswürdigen Stamm auf dem Clientcomputer gebunden. Smart Card-basierte Zertifikate mit AD FS ist Folgendes erforderlich:  
  
-   Der Leser und der Kryptografiedienstanbieter (CSP) für die Smartcard müssen auf dem Computer arbeiten, wo sich der Browser befindet.  
  
-   Das Smartcardzertifikat muss an einen vertrauenswürdigen Stamm auf dem Kontoverbundserver und die Konto-Verbundserverproxy verkettet.  
  
-   Das Zertifikat muss dem Benutzerkonto in AD DS mit einer der folgenden Methoden zugeordnet:  
  
    -   Der Antragstellername des Zertifikats entspricht dem definierten LDAP-Namen eines Benutzerkontos in AD DS.  
  
    -   Das zertifikaterweiterung für den Zertifikatantragsteller-alternatnamen verfügt hat der Benutzerprinzipalname (UPN) eines Benutzerkontos in AD DS.  
  
Um bestimmte Verschlüsselungsstärke authentifizierungsanforderungen in einigen Szenarien zu unterstützen, ist es auch möglich, konfigurieren AD FS für die Erstellung eines Anspruchs, das angibt, wie der Benutzer authentifiziert wurde. Eine vertrauende Seite kann diesen Anspruch dann verwenden, um eine autorisierungsentscheidung zu treffen.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
