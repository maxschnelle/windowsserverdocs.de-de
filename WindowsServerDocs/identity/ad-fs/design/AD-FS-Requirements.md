---
ms.assetid: 8ce6e7c4-cf8e-4b55-980c-048fea28d50f
title: Verbundserverfarm mit SQL Server
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1310792158995608e8f477b6df9d6cf7c0284571
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822251"
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen

>Gilt für: Windows Server 2012 R2

Im folgenden finden die verschiedenen Anforderungen, denen Sie beim Bereitstellen von AD FS entsprechen soll:  
  
-   [Zertifikatanforderungen](AD-FS-Requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](AD-FS-Requirements.md#BKMK_2)  
  
-   [Softwareanforderungen](AD-FS-Requirements.md#BKMK_3)  
  
-   [AD DS-Anforderungen](AD-FS-Requirements.md#BKMK_4)  
  
-   [Anforderungen an die Datenbank](AD-FS-Requirements.md#BKMK_5)  
  
-   [Browseranforderungen](AD-FS-Requirements.md#BKMK_6)  
  
-   [Extranet-Anforderungen](AD-FS-Requirements.md#BKMK_extranet)  
  
-   [Netzwerkanforderungen](AD-FS-Requirements.md#BKMK_7)  
  
-   [Anforderungen an den Attributspeicher](AD-FS-Requirements.md#BKMK_8)  
  
-   [Anwendungsanforderungen](AD-FS-Requirements.md#BKMK_9)  
  
-   [Anforderungen für die Authentifizierung](AD-FS-Requirements.md#BKMK_10)  
  
-   [Workplace Join-Anforderungen](AD-FS-Requirements.md#BKMK_11)  
  
-   [Verschlüsselungsanforderungen](AD-FS-Requirements.md#BKMK_12)  
  
-   [Erforderliche Berechtigungen](AD-FS-Requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>Zertifikatanforderungen  
Zertifikate spielen die wichtigste Rolle beim Sichern der Kommunikation zwischen Federation Server, Webanwendungsproxys, Ansprüche\-unterstützenden Anwendungen und Webclients. Die Anforderungen für Zertifikate sind abhängig, ob Sie einen Verbundserver oder eine Proxy-Computer einrichten, wie in diesem Abschnitt beschrieben.  
  
**Verbundserverzertifikate**  
  
|||  
|-|-|  
|**Zertifikattyp**|**Anforderungen, Support und wichtige Informationen**|  
|**Secure Sockets Layer \(SSL\) Zertifikat:** Dies ist ein standardmäßiges SSL-Zertifikat, das zum Sichern der Kommunikation zwischen Verbundservern und Clients verwendet wird.|: Dieses Zertifikat muss eine öffentlich vertrauenswürdige\* X509 v3-Zertifikat.<br />– Alle Clients, die den Zugriff auf alle AD FS-Endpunkt müssen diesem Zertifikat vertrauen. Es wird dringend empfohlen, zum Verwenden von Zertifikaten, die von einer öffentlichen ausgegeben werden \(dritte\-Partei\) Zertifizierungsstelle \(Zertifizierungsstelle\). Sie können ein selbstsigniertes\-signierten SSL-Zertifikat erfolgreich Verbundserver in einer testumgebung auszuführen. Für eine produktionsumgebung empfehlen wir jedoch, dass Sie das Zertifikat von einer öffentlichen Zertifizierungsstelle beziehen.<br />-Unterstützt alle Schlüsselgrößen, die von Windows Server 2012 R2 für SSL-Zertifikate unterstützt werden.<br />– Keine Zertifikate unterstützt, die CNG-Schlüsseln zu verwenden ist.<br />– Wenn Sie zusammen mit der Arbeitsbereichverknüpfung verwendet\/Device Registration Service, in der alternativen Antragstellernamen des SSL-Zertifikats für AD FS-Diensts darf der Wert Enterpriseregistration, der den Benutzerprinzipalnamen folgt\(UPN\) Suffix Ihrer Organisation, z. B. enterpriseregistration.contoso.com.<br />-Platzhalterzertifikate werden unterstützt. Wenn Sie AD FS-Farm erstellen, werden Sie aufgefordert, den Dienstnamen für den AD FS-Dienst bereitstellen \(z. B. **"ADFS.contoso.com"**.<br />– Es wird dringend empfohlen, dasselbe SSL-Zertifikat für die Web Application Proxy zu verwenden. Dies ist jedoch **erforderlichen** identisch sein, bei der Unterstützung der integrierten Windows-Authentifizierung-Endpunkte über den Webanwendungsproxy und bei der Authentifizierung für erweiterten Schutz aktiviert ist \(Standardeinstellung\).<br />-Der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede Instanz von AD FS darzustellen, die Sie bereitstellen. Aus diesem Grund sollten Sie in Betracht ziehen einen Antragstellernamen auf einer neuen Zertifizierungsstelle\-ausgestellte Zertifikate, die am besten den Namen Ihrer Firma oder Organisation gegenüber Partnern darstellt.<br />    Die Identität des Zertifikats muss dem Namen des Verbunddiensts übereinstimmen \(z. B. "FS.contoso.com"\). Die Identität ist entweder eine Erweiterung alternativen Antragstellernamens des Typs "DnsName", oder wenn keine Subject alternative Namenseinträge vorhanden sind, wird der Name des Antragstellers als ein allgemeiner Name angegeben. Mehrfach Subject alternative Name können im Zertifikat vorhanden sein, bereitgestellte einen dieser Namen des Verbunddiensts übereinstimmt.<br />-   **Wichtig:** es wird dringend empfohlen, um dasselbe SSL-Zertifikat für alle Knoten der AD FS-Farm sowie alle Webanwendung Proxys in der AD FS-Farm zu verwenden.|  
|**Dienstkommunikationszertifikat:** Mit diesem Zertifikat wird die WCF-Nachrichtensicherheit für das Sichern der Kommunikation zwischen Verbundservern aktiviert.|– In der Standardeinstellung wird das SSL-Zertifikat als dienstkommunikationszertifikat verwendet.  Sie haben jedoch auch die Möglichkeit, ein anderes Zertifikat als das Dienstzertifikat für die Kommunikation zu konfigurieren.<br />-   **Wichtig:** bei Verwendung der SSL-Zertifikat als das dienstkommunikationszertifikat, wenn das SSL-Zertifikat abläuft, stellen Sie sicher, um das erneuerte SSL-Zertifikat als des Dienstzertifikats für die Kommunikation zu konfigurieren. Dies geschieht nicht automatisch.<br />: Dieses Zertifikat muss von Clients von AD FS vertrauenswürdig sein, die WCF-Nachrichtensicherheit verwenden.<br />– Es wird empfohlen, dass Sie ein Serverauthentifizierungszertifikat verwenden, die von einer öffentlichen ausgegeben wird \(dritte\-Partei\) Zertifizierungsstelle \(Zertifizierungsstelle\).<br />-Das dienstkommunikationszertifikat darf nicht über ein Zertifikat sein, die CNG-Schlüssel verwendet.<br />: Dieses Zertifikat kann mithilfe der AD FS-Verwaltungskonsole verwaltet werden.|  
|**Token\-Signaturzertifikat:** Dies ist ein Standard-X509-Zertifikat, das für die sichere Signierung aller Token verwendet wird, die der Verbungsserver ausstellt.|-AD FS erstellt standardmäßig ein selbstsigniertes\-selbstsignierten Zertifikats mit 2048-Bit-Schlüsseln.<br />-Zertifizierungsstelle ausgestellten Zertifikate werden ebenfalls unterstützt und kann geändert werden, mithilfe der AD FS-Verwaltungs-Snap\-in<br />-Zertifizierungsstelle ausgestellte Zertifikate muss erfolgt über ein CSP-Kryptografieanbieter & gespeichert werden.<br />-Das Tokensignaturzertifikat darf nicht über ein Zertifikat sein, die CNG-Schlüssel verwendet.<br />-AD FS erfordert keine externe Registrierung von Zertifikaten für die Tokensignatur.<br />    AD FS automatisch erneuert diese Self-Service\-Zertifikate signiert, bevor sie ablaufen, konfigurieren zunächst die neuen Zertifikate als sekundären Zertifikate für Partner, die sie nutzen können dann zum primären Replikat in einem Prozess kippen automatische aufgerufen zertifikatrollover. Es wird empfohlen, dass Sie die Standardeinstellung, die automatisch generierte Zertifikate für die Tokensignatur verwenden.<br />    Wenn Ihre Organisation Richtlinien, die verschiedene Zertifikate verfügt konfiguriert werden, für die Tokensignatur erfordern, können Sie die Zertifikate angeben, bei der Installation mithilfe von Powershell \(verwenden Sie den Parameter – SigningCertificateThumbprint der Installation \-AdfsFarm Cmdlet\).  Nach der Installation können Sie anzeigen und Verwalten von token mit dem AD FS-Verwaltungskonsole oder der Powershell-Cmdlets Set-Signaturzertifikate\-AdfsCertificate "und" Get\-AdfsCertificate.<br />    Wenn extern Registrierung von Zertifikaten für die Tokensignatur verwendet werden, führt die AD FS keine automatische Verlängerung von Zertifikaten oder Rollover durch.  Dieser Vorgang muss von einem Administrator ausgeführt werden.<br />    Um zertifikatrollover zuzulassen, wenn ein Zertifikat nahezu abgelaufen ist, kann eine sekundäre Tokensignaturzertifikat im AD FS konfiguriert werden. Standardmäßig werden alle token-Signaturzertifikate in Verbundmetadaten, aber nur das primäre Token veröffentlicht\-Signaturzertifikat zum Signieren von Token tatsächlich von AD FS verwendet wird.|  
|**Token\-Entschlüsselung\/Verschlüsselungszertifikat:** Dies ist ein standard X509 Zertifikat, das zur Entschlüsselung verwendet wird\/aller eingehenden Token zu verschlüsseln. Es wird außerdem in den Verbundmetadaten veröffentlicht.|-AD FS erstellt standardmäßig ein selbstsigniertes\-selbstsignierten Zertifikats mit 2048-Bit-Schlüsseln.<br />-Zertifizierungsstelle ausgestellten Zertifikate werden ebenfalls unterstützt und kann geändert werden, mithilfe der AD FS-Verwaltungs-Snap\-in<br />-Zertifizierungsstelle ausgestellte Zertifikate muss erfolgt über ein CSP-Kryptografieanbieter & gespeichert werden.<br />-Das Token\-Entschlüsselung\/Verschlüsselungszertifikat handelt es sich nicht um ein Zertifikat aus, die CNG-Schlüssel verwendet.<br />-Standardmäßig AD FS generiert und verwendet einen eigenen, intern generierte und Self\-selbstsignierten Zertifikaten für die Entschlüsselung von token.  AD FS erfordert keine externe Registrierung von Zertifikaten für diesen Zweck.<br />    Darüber hinaus AD FS automatisch erneuert diese Self-Service\-Zertifikate signiert, bevor sie ablaufen.<br />    **Es wird empfohlen, dass Sie die Standardwerte des automatisch generierten Zertifikate für die Entschlüsselung von token verwenden.**<br />    Wenn Ihre Organisation Richtlinien, die verschiedene Zertifikate verfügt konfiguriert werden, für die Entschlüsselung von token benötigen, können Sie die Zertifikate angeben, bei der Installation mithilfe von Powershell \(verwenden den – DecryptionCertificateThumbprint-Parameter, der die Installieren Sie\-AdfsFarm Cmdlet\).  Nach der Installation können Sie anzeigen und Verwalten von tokenentschlüsselungszertifikate, die mit dem AD FS-Verwaltungskonsole oder der Powershell-Cmdlets Set\-AdfsCertificate "und" Get\-AdfsCertificate.<br />    **Wenn externe Registrierung von Zertifikaten für die Entschlüsselung von token verwendet werden, führt der AD FS keine automatische Verlängerung von Zertifikaten.  Dieser Vorgang muss von einem Administrator ausgeführt werden**.<br />– Das AD FS-Dienstkonto benötigen Zugriff auf das Token\-Signieren der private Schlüssel des Zertifikats im persönlichen Speicher des lokalen Computers. Dies wird vom Setup übernommen. Sie können auch die AD FS-Verwaltungs-Snap\-um diesen Zugriff sicherzustellen, wenn Sie anschließend das Token ändern\-Signaturzertifikat.|  
  
> [!CAUTION]  
> Zertifikate, die für Token verwendet werden\-signier- und token\-entschlüsseln\/Verschlüsselung sind entscheidend, um die Stabilität des Verbunddiensts. Kunden verwalten ihre eigenen Token\-Signierung & token\-entschlüsseln\/Verschlüsselungszertifikate sorgen dafür, dass diese Zertifikate gesichert werden und sind unabhängig voneinander während eines Ereignisses für die Wiederherstellung verfügbar.  
  
> [!NOTE]  
> In AD FS können Sie den sicheren Hashalgorithmus ändern \(SHA\) Ebene, die verwendet wird, für digitale Signaturen entweder SHA\-1 oder SHA\-256 \(sicherer\). AD FS unterstützt nicht die Verwendung von Zertifikaten mit anderen Hashmethoden als MD5 \(der Standardhashalgorithmus, der verwendet wird, mit dem Befehl Makecert.exe\-Tools "Linie"\). Als bewährte Sicherheitsmethode es wird empfohlen, die Verwendung von SHA\-256 \(der wird standardmäßig festgelegt\) für alle Signaturen. SHA\-1 wird empfohlen, nur in Szenarien, in denen Sie interoperieren müssen mit einem Produkt, das keine Kommunikation über SHA unterstützt\-256, z. B. ein nicht\-Microsoft-Produkt oder eine ältere Versionen von AD FS.  
  
> [!NOTE]  
> Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher auf dem lokalen Computer importiert werden. Sie können Zertifikate importieren, in den persönlichen Speicher mit dem Zertifikate-MMC-Snap\-in.  
  
## <a name="BKMK_2"></a>Hardwareanforderungen  
Die folgenden Mindestanforderungen bzw. empfohlenen hardwareanforderungen gelten für die AD FS-Verbundservern in Windows Server 2012 R2:  
  
||||  
|-|-|-|  
|**Hardwareanforderung**|**Mindestanforderung**|**Empfehlung**|  
|CPU-Geschwindigkeit|1,4-GHz-64\--bit-Prozessor|Quad\-Kern, 2 GHz|  
|RAM|512 MB|4 GB|  
|Speicherplatz|32 GB|100 GB|  
  
## <a name="BKMK_3"></a>Softwareanforderungen  
Die folgenden AD FS-Anforderungen gelten für die Serverfunktionen, die in das Betriebssystem Windows Server® 2012 R2 integriert ist:  
  
-   Für den Extranetzugriff, müssen Sie die Webanwendungsproxy-Rollendienst bereitstellen \- Teil der Windows Server® 2012 R2-RAS-Serverrolle. Frühere Versionen von einem Verbundserverproxy werden mit AD FS unter Windows Server® 2012 R2 nicht unterstützt.  
  
-   Verbundserver und den Webanwendungsproxy-Rollendienst können nicht auf demselben Computer installiert werden.  
  
## <a name="BKMK_4"></a>AD DS-Anforderungen  
**Anforderungen an den Domänencontroller**  
  
DS-Domänencontroller in Domänen für alle Benutzer und die Domäne, die mit der AD FS-Servern verknüpft sind müssen WindowsServer 2008 oder höher ausgeführt werden.  
  
> [!NOTE]  
> Alle Unterstützung für Umgebungen mit Windows Server 2003-Domänencontrollern endet nach dem die erweiterte Unterstützung End Date für Windows Server 2003. Kunden werden dringend empfohlen, die Domänencontroller so bald wie möglich zu aktualisieren. Besuchen Sie [auf dieser Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) Weitere Informationen zur Microsoft Support Lifecycle. Für Probleme, die ermittelt werden, die für Windows Server 2003 Domain Controller-Umgebungen, Fixes nur für Sicherheitsprobleme ausgegeben werden, und wenn eine Lösung vor Ablauf der erweiterte Support für Windows Server 2003 ausgelöst werden kann.  
  
**Domänenfunktionsebene\-Anforderungen**  
  
Alle Domänen-Benutzerkonten und die Domäne, die mit der AD FS-Servern verknüpft sind, müssen auf die Domänenfunktionsebene von Windows Server 2003 oder höher ausgeführt werden.  
  
Die meisten AD FS-Features erfordern keine AD DS funktionale\-Ebene Änderungen erfolgreich betrieben werden kann. Allerdings ist die Windows Server 2008-Domänenfunktionsebene oder höher erforderlich, damit die Clientzertifikatauthentifizierung erfolgreich betrieben werden kann, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
**Schemaanforderungen**  
  
-   AD FS erfordert keine Änderungen am Datenbankschema oder funktionale\-Ebene Modifikationen an AD DS.  
  
-   Um Workplace Join-Funktionen verwenden, muss das Schema der Gesamtstruktur, der mit AD FS-Server verbunden sind, zu Windows Server 2012 R2 festgelegt werden.  
  
**Anforderungen an das Dienstkonto**  
  
-   Alle standard-Service-Konto kann als Dienstkonto für AD FS verwendet werden. Verwaltete gruppendienstkonten werden ebenfalls unterstützt. Dies erfordert, dass mindestens ein Domänencontroller \(es wird empfohlen, dass Sie zwei oder mehr bereitstellen\) , WindowsServer 2012 oder höher ausgeführt wird.  
  
-   Für Kerberos-Authentifizierung zwischen Domänen-Funktion\-eingebundenen Clients und AD FS, die "HOST\/< AD FS\_Service\_Name >' muss als einen SPN für das Dienstkonto registriert werden. Standardmäßig werden AD FS dies konfigurieren, wenn eine neue AD FS-Farm zu erstellen, wenn sie über ausreichende Berechtigungen zum Ausführen dieses Vorgangs verfügt.  
  
-   Das AD FS-Dienstkonto muss in jeder Benutzerdomäne vertrauenswürdig sein, das enthält, Benutzer zu authentifizieren, um AD FS-Diensts.  
  
**Domänenanforderungen**  
  
-   Alle AD FS-Server müssen zu einer AD DS-Domäne eingebunden sein.  
  
-   Alle AD FS-Server innerhalb einer Farm müssen in einer einzelnen Domäne bereitgestellt werden.  
  
-   Die Domäne, der die AD FS-Server angehören muss jede Domäne des Benutzerkontos vertrauen, die Benutzer, die Authentifizierung bei AD FS-Diensts enthält.  
  
**Anforderungen für mehrere Gesamtstrukturen**  
  
-   Jede Domäne des Benutzerkontos oder der Gesamtstruktur, die Benutzer, die Authentifizierung bei AD FS-Diensts enthält, muss die Domäne, der die AD FS-Server angehören vertrauen.  
  
-   Das AD FS-Dienstkonto muss in jeder Benutzerdomäne vertrauenswürdig sein, das enthält, Benutzer zu authentifizieren, um AD FS-Diensts.  
  
## <a name="BKMK_5"></a>Anforderungen an die Datenbank  
Im folgenden sind die Anforderungen und Einschränkungen basierend auf den Konfigurationsspeicher:  
  
**WID**  
  
-   Eine WID-Farm hat ein Limit von 30 Verbundserver aus, wenn Sie bis zu 100 Vertrauensstellungen der vertrauenden Seite Partei haben.  
  
-   Artefakt Auflösung-Profil in SAML 2.0 wird in der Konfigurationsdatenbank WID nicht unterstützt.  Token-Replay-Erkennung wird in der Konfigurationsdatenbank WID nicht unterstützt. Diese Funktion wird nur dann nur in Szenarien verwendet, in dem AD FS fungiert als verbundanbieter ist, und Nutzen von Sicherheitstoken von externen Anspruchsanbietern.  
  
-   Bereitstellen von AD FS-Server in unterschiedlichen Rechenzentren für ein Failover oder geografischen Lastenausgleich wird unterstützt, solange die Anzahl der Server nicht 30 nicht überschreiten.  
  
Die folgende Tabelle enthält eine Zusammenfassung für die Verwendung einer Windows-datenbankfarm.  Verwenden Sie sie an, um Ihre Implementierung planen.  
  
||||  
|-|-|-|  
||1 \- 100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen|  
|1 \- 30 AD FS-Knoten|WID unterstützt|Nicht unterstützt, mit WID \- SQL erforderlich|  
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \- SQL erforderlich|Nicht unterstützt, mit WID \- SQL erforderlich|  
  
**SQL Server**  
  
Für AD FS unter Windows Server 2012 R2 können Sie SQLServer 2008 und höher verwenden.  
  
## <a name="BKMK_6"></a>Browseranforderungen  
Wenn AD FS-Authentifizierung über einen Browser bzw. ein Webbrowser-Steuerelement ausgeführt wird, muss Ihr Browser die folgenden Anforderungen erfüllt werden:  
  
-   JavaScript muss aktiviert sein  
  
-   Cookies müssen aktiviert sein  
  
-   Server Name Indication \(SNI\) unterstützt werden müssen  
  
-   Für die Authentifizierung mit Zertifikat & ät Benutzerzertifikat \(Workplace Join Funktionalität\), muss die Browserunterstützung SSL-Clientzertifikatauthentifizierung  
  
Mehrere Schlüssel Browser und Plattformen unterzogen Validierung für das Rendering und Funktionen, die die Details unten aufgeführt sind. Browser und Geräte, die in dieser Tabelle nicht abgedeckt werden weiterhin unterstützt, wenn sie die oben aufgeführten Anforderungen erfüllen:  
  
|||  
|-|-|  
|**Browser**|**Plattformen**|  
|IE 10.0|Windows 7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2|  
|IE 11.0|Windows7, Windows 8.1, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2|  
|Windows Web Authentication Broker|Windows 8.1|  
|Firefox \[v21\]|Windows 7, Windows 8.1|  
|Safari \[v7\]|iOS 6, Mac OS\-X 10.7|  
|Chrome \[v27\]|Windows 7, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, Mac OS\-X 10.7|  
  
> [!IMPORTANT]  
> Bekanntes Problem \- Firefox: Workplace Join-Funktionen, die das Gerät mithilfe eines Zertifikats für Gerät identifiziert, funktioniert nicht auf Windows-Plattformen. Firefox unterstützt derzeit keine SSL-Zertifikat Clientauthentifizierung mithilfe von Zertifikaten, die in den Zertifikatspeicher des Benutzers auf Windows-Clients bereitgestellt.  
  
**Cookies**  
  
AD FS erstellt die Sitzung\-basiert und beständige Cookies, die auf Clientcomputern anmelden bereitstellen gespeichert werden müssen\-Anmeldung\-, einmaliges Anmelden\-auf \(SSO\), und andere Funktionen. Daher muss der Clientbrowser so konfiguriert sein, dass Cookies akzeptiert werden. Cookies, die für die Authentifizierung verwendet werden, sind immer Secure Hypertext Transfer Protocol \(HTTPS\) Sitzungscookies, die für den Ursprungsserver geschrieben werden. Wenn die Konfiguration des Clientbrowsers diese Cookies nicht zulässt, kann AD FS nicht ordnungsgemäß funktionieren. Beständige Cookies werden verwendet, um die Benutzerauswahl des Anspruchsanbieters beizubehalten. Sie können diese deaktivieren, indem Sie über eine Konfigurationseinstellung in der Konfigurationsdatei für die AD FS-Anmeldeseite\-in Seiten. Unterstützung für TLS\/SSL ist aus Sicherheitsgründen erforderlich.  
  
## <a name="BKMK_extranet"></a>Extranet-Anforderungen  
Um extranet-Zugriff auf den AD FS-Dienst bereitzustellen, müssen Sie die Webanwendungsproxy-Rollendienst der Rolle des extranet zugängliche, Proxys authentifizierungsanforderungen auf sichere Weise mit dem AD FS-Dienst bereitstellen. Dadurch wird die Isolation von den AD FS-Dienst-Endpunkten sowie die Isolation von allen Sicherheitsschlüsseln \(wie z. B. Tokensignaturzertifikate\) von Anforderungen, die aus dem Internet stammen. Darüber hinaus erfordern Features wie z. B. vorläufig Extranetsperre Konto die Verwendung des Webanwendungsproxys. Weitere Informationen zum Webanwendungsproxy finden Sie unter [Web Application Proxy](https://technet.microsoft.com/library/dn584107.aspx).  
  
Wenn Sie eine dritte verwenden möchten\-Proxy für den Extranetzugriff, diesem dritten Partei\-Partei Proxy muss das Protokoll in definierten unterstützen [http:\/\/download.microsoft.com\/herunterladen\/9\/5\/E\/95EF66AF\-9026\-4BB0\-A41D\-A4F81802D92C\/% 5bMS\-ADFSPIP%5d.pdf](https://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-ADFSPIP%5d.pdf).  
  
## <a name="BKMK_7"></a>Netzwerkanforderungen  
Konfigurieren entsprechend der folgenden Netzwerkdienste ist wichtig, für eine erfolgreiche Bereitstellung von AD FS in Ihrer Organisation:  
  
**Konfigurieren von Unternehmens-Firewall**  
  
Sowohl die Firewall zwischen Webanwendungsproxy und der Verbundserverfarm und der Firewall zwischen den Clients und des Webanwendungsproxys müssen TCP-Port 443 aktiviert eingehende.  
  
Darüber hinaus, wenn der Clientbenutzer-Zertifikatauthentifizierung \(ClientTLS-Authentifizierung mit X509 Benutzerzertifikate\) ist erforderlich, die AD FS unter Windows Server 2012 R2 erfordert, dass TCP-Port 49443 eingehende der Firewall zwischen den Clients und des Webanwendungsproxys. Dies ist nicht erforderlich, in der Firewall zwischen dem Webanwendungsproxy und den Verbundservern\).  
  
**Konfigurieren von DNS**  
  
-   Für den Intranetzugriff, alle Clients, die Zugriff auf AD FS-Dienst im internen Unternehmensnetzwerk \(Intranet\) muss in der Lage, den AD FS-Dienstnamen aufzulösen \(durch das SSL-Zertifikat bereitgestellte Name\) mit dem Laden Lastenausgleich für die AD FS-Server oder dem AD FS-Server.  
  
-   Für den Extranetzugriff, alle Clients, die Zugriff auf AD FS-Diensts über außerhalb des Unternehmensnetzwerks \(extranet\/Internet\) muss in der Lage, den AD FS-Dienstnamen aufzulösen \(durch das SSL-ZertifikatangegebeneName\) für den Load Balancer für die Webanwendungsproxy-Server oder den Webanwendungsproxy-Server.  
  
-   Für den Extranetzugriff ordnungsgemäß funktioniert, jedem Webanwendungsproxy-Server in der DMZ muss in der Lage, AD FS-Dienstnamen aufzulösen \(durch das SSL-Zertifikat bereitgestellte Name\) für den Load Balancer für die AD FS-Server oder dem AD FS-Server. Dies kann erreicht werden, verwenden einen alternativen DNS-Server in der DMZ-Netzwerk oder lokalen Server auflösen, die mithilfe von "HOSTS"-Datei ändern.  
  
-   Für die integrierte Windows-Authentifizierung arbeiten innerhalb des Netzwerks und außerhalb des Netzwerks für eine Teilmenge der Endpunkte, die über die Web Application Proxy verfügbar gemacht werden, müssen Sie einen A-Eintrag verwenden \(nicht CNAME\) um auf den Lastenausgleich zu verweisen.  
  
Informationen zum Konfigurieren von Unternehmens-DNS für den Verbunddienst und Device Registration Service, finden Sie unter [Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS](https://technet.microsoft.com/library/dn486786.aspx).  
  
Informationen zum Konfigurieren von Unternehmens-DNS für Web Application-Proxys finden Sie im Abschnitt "Konfigurieren von DNS" in [Schritt 1: Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383644.aspx).  
  
Informationen zum Konfigurieren einer Cluster-IP-Adresse oder FQDN mit NLB-cluster finden Sie unter Angeben der Clusterparameter am [http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=75282](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
## <a name="BKMK_8"></a>Anforderungen an den Attributspeicher  
AD FS erfordert mindestens ein Attributspeicher für das Authentifizieren von Benutzern und Extrahieren von Sicherheitsansprüchen für diese Benutzer verwendet werden soll. Eine Liste von AD FS unterstützten finden Sie unter [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
> [!NOTE]  
> AD FS erstellt standardmäßig automatisch einen Attributspeicher "Active Directory" auf. Hängen Sie, dass Anforderungen an den Attributspeicher gibt an, ob Ihre Organisation als Kontopartner fungiert \(die Verbundbenutzer hostet\) oder der Ressourcenpartnerorganisation \(die verbundanwendung hostet\).  
  
**LDAP-Attributspeicher**  
  
Beim Arbeiten mit anderen Lightweight Directory Access Protocol \(LDAP\)\-basierten attributspeichern, Sie müssen mit einem LDAP-Server, die integrierte Windows-Authentifizierung unterstützt verbinden. Die LDAP-Verbindungszeichenfolge muss außerdem im Format einer LDAP-URL geschrieben sein, wie in RFC 2255 beschrieben.  
  
Es ist auch erforderlich, dass das Dienstkonto für AD FS-Diensts zum Abrufen von Benutzerinformationen in die LDAP-Attributspeicher ist.  
  
**SQL Server-Attributspeichern**  
  
Für AD FS in Windows Server 2012 R2 erfolgreich betrieben werden kann müssen auf Computern, die den SQL Server-Attributspeicher hosten entweder Microsoft SQLServer 2008 oder höher ausgeführt werden. Beim Arbeiten mit SQL\-basierten attributspeichern, außerdem müssen Sie konfigurieren eine Verbindungszeichenfolge.  
  
**Benutzerdefinierte Attributspeicher**  
  
Sie können benutzerdefinierte Attributspeicher entwickeln, um erweiterte Szenarien zu aktivieren.  
  
-   Die in AD FS integrierte Richtiliniensprache kann auf benutzerdefinierte Attributspeicher verweisen, sodass jedes der folgenden Szenarien verbessert werden kann:  
  
    -   Erstellen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Ergänzen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Autorisieren eines Benutzers zum Abrufen eines Token  
  
    -   Autorisieren eines Diensts zum Abrufen eines Token zum Verhalten eines Benutzers  
  
    -   Ausgeben zusätzliche Daten in die vertrauende Seite von AD FS ausgestellten Sicherheitstoken.  
  
-   Alle benutzerdefinierten Attributspeicher müssen auf .NET 4.0 oder höher erstellt werden.  
  
Wenn Sie mit einem benutzerdefinierten Attributspeicher arbeiten, Sie auch möglicherweise eine Verbindungszeichenfolge konfigurieren. In diesem Fall können Sie einen benutzerdefinierten Code Ihrer Wahl eingeben, die eine Verbindung mit Ihrem benutzerdefinierten Attributspeicher ermöglicht. Die Verbindungszeichenfolge in diesem Fall ist ein Satz von Namen\/Wert-Paare, die interpretiert werden, wie vom Entwickler des benutzerdefinierten Attributspeichers implementiert. Weitere Informationen zum Entwickeln und Verwenden von benutzerdefinierten attributspeichern finden Sie unter [Store-Übersicht über Attribute](https://go.microsoft.com/fwlink/?LinkId=190782).  
  
## <a name="BKMK_9"></a>Anwendungsanforderungen  
AD FS unterstützt Ansprüche\-Anwendungen unterstützen, die die folgenden Protokolle verwenden:  
  
-   WS\-Verbund  
  
-   WS\-vertrauen  
  
-   SAML 2.0-Protokolls, die mithilfe von IDPLite, SPLite & eGov1.5 Profilen.  
  
-   OAuth 2.0 Authorization Grant-Profil  
  
AD FS unterstützt auch Authentifizierung und Autorisierung für alle nicht\-Ansprüche\-Anwendungen unterstützen, die von der Web Application Proxy unterstützt werden.  
  
## <a name="BKMK_10"></a>Anforderungen für die Authentifizierung  
**AD DS-Authentifizierung \(primäre Authentifizierung\)**  
  
Für den Intranetzugriff werden die folgenden Mechanismen zur Standardauthentifizierung für AD DS unterstützt:  
  
-   Integrierte Windows-Authentifizierung mithilfe des Negotiate für Kerberos und NTLM  
  
-   Die Formularauthentifizierung mit Benutzernamen\/Kennwörter  
  
-   Zertifikatauthentifizierung mithilfe von Zertifikaten, die Benutzerkonten in AD DS zugeordnet  
  
Für den Extranetzugriff werden die folgenden Authentifizierungsmechanismen unterstützt:  
  
-   Die Formularauthentifizierung mit Benutzernamen\/Kennwörter  
  
-   Zertifikatbasierte Authentifizierung mit Zertifikaten, die Benutzerkonten in AD DS zugeordnet sind  
  
-   Integrierte Windows-Authentifizierung mithilfe des Negotiate \(nur NTLM\) WS\-Trust-Endpunkte, die integrierte Windows-Authentifizierung zu akzeptieren.  
  
Für die Zertifikatauthentifizierung:  
  
-   Erstreckt sich auf Smartcards, die Pin geschützt werden können.  
  
-   Die grafische Benutzeroberfläche für den Benutzer zur Eingabe der Pin nicht von AD FS bereitgestellt wird und ist erforderlich, um das Betriebssystem des Clients gehören, die angezeigt wird, wenn die TLS-Client verwenden.  
  
-   Der Reader und einen Kryptografiedienstanbieter \(CSP\) für die Smartcard, die auf dem Computer arbeiten muss, wo sich der Browser befindet.  
  
-   Das Smartcardzertifikat muss an einen vertrauenswürdigen Stamm auf dem AD FS-Server und Webanwendungs-Proxyservern verkettet, um.  
  
-   Das Zertifikat muss dem Benutzerkonto in AD DS mit einer der folgenden Methoden zugeordnet sein:  
  
    -   Der Antragstellername des Zertifikats entspricht dem definierten LDAP-Namen eines Benutzerkontos in AD DS.  
  
    -   Die Zertifikat Betreff Erweiterung alternatnamen verfügt über den Benutzerprinzipalnamen \(UPN\) eines Benutzerkontos in AD DS.  
  
Verwenden für die nahtlose integrierte Windows-Authentifizierung Kerberos im Intranet,  
  
-   Es ist erforderlich, damit der Dienstname als Teil der vertrauenswürdigen Websites oder lokale Intranetsites.  
  
-   Außerdem wird der HOST\/< AD FS\_Service\_Name > SPN muss festgelegt werden, für das Dienstkonto, auf denen AD FS-Farm ausgeführt.  
  
**Mit mehreren\-zweistufige Authentifizierung**  
  
AD FS unterstützt zusätzlichen Authentifizierung \(neben der primären Authentifizierung von AD DS unterstützt\) mithilfe eines Anbietermodells durch Anbieter\/Kunden können ihre eigenen mit mehreren erstellen\-Factor Authentication-Adapter ein Administrator kann registrieren und während der Anmeldung verwenden.  
  
Alle MFA-Adapter muss auf .NET 4.5 erstellt werden.  
  
Weitere Informationen zu MFA, finden Sie unter [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).  
  
**Geräteauthentifizierung**  
  
AD FS unterstützt Geräteauthentifizierung mit Zertifikaten, die während der Vorgang von einem Endbenutzer Workplace verknüpfen ihr Gerät beim Device Registration Service bereitgestellt.  
  
## <a name="BKMK_11"></a>Workplace Join-Anforderungen  
Endbenutzer können arbeitsplatzbeitritt ihre Geräte für eine Organisation mithilfe von AD FS. Dies wird durch den Geräteregistrierungsdienst in AD FS unterstützt. Daher erhalten Endbenutzer den zusätzlichen Vorteil von SSO für die Anwendungen, die von AD FS unterstützt. Darüber hinaus können Administratoren durch Einschränken des Zugriffs auf Anwendungen, die nur für Geräte, die für die Organisation Arbeitsplatz wurden Risiko verwalten. Im folgenden finden Sie die folgenden Anforderungen für dieses Szenario zu ermöglichen.  
  
-   AD FS unterstützt eine arbeitsbereichverknüpfung für Windows 8.1 und iOS 5\+ Geräte  
  
-   Um Workplace Join-Funktionen verwenden, muss das Schema der Gesamtstruktur, der mit AD FS-Server verbunden sind, Windows Server 2012 R2 sein.  
  
-   Der alternative Antragstellername des SSL-Zertifikats für AD FS-Dienst muss dem Wert Enterpriseregistration, der den Benutzerprinzipalnamen folgt enthalten \(UPN\) Suffix Ihrer Organisation, z. B. enterpriseregistration.corp.contoso.com.  
  
## <a name="BKMK_12"></a>Verschlüsselungsanforderungen  
Die folgende Tabelle enthält zusätzliche Kryptografie Supportinformationen auf dem AD FS-Token "Signierung", "tokenverschlüsselung\/Entschlüsselung Funktionen:  
  
||||  
|-|-|-|  
|**Algorithmus**|**Schlüssellängen**|**Protokolle\/Anwendungen\/Kommentare**|  
|TripleDES – Standard, 192 \(unterstützt 192 bis 256\) \- [http:\/\/www.w3.org\/2001\/04\/Xmlenc\# TripleDES\-cbc](http://www.w3.org/2001/04/xmlenc)|>\= 192|Unterstützter Algorithmus für das Sicherheitstoken entschlüsseln. Verschlüsseln das Sicherheitstoken, mit dem dieser Algorithmus wird nicht unterstützt.|  
|AES128 \- http:\/\/www.w3.org\/2001\/04\/xmlenc\#aes128\-cbc|128|Unterstützter Algorithmus für das Sicherheitstoken entschlüsseln. Verschlüsseln das Sicherheitstoken, mit dem dieser Algorithmus wird nicht unterstützt.|  
|AES192 \- http:\/\/www.w3.org\/2001\/04\/xmlenc\#aes192\-cbc|192|Unterstützter Algorithmus für das Sicherheitstoken entschlüsseln. Verschlüsseln das Sicherheitstoken, mit dem dieser Algorithmus wird nicht unterstützt.|  
|AES256 \- [http:\/\/www.w3.org\/2001\/04\/xmlenc\#aes256\-cbc](http://www.w3.org/2001/04/xmlenc)|256|**Standard**: Unterstützter Algorithmus für das Sicherheitstoken zu verschlüsseln.|  
|TripleDESKeyWrap \- http:\/\/www.w3.org\/2001\/04\/xmlenc\#kw\-tripledes|Alle Schlüssel-Größen, die von .NET 4.0 unterstützt werden\+|Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der ein Sicherheitstoken verschlüsselt.|  
|AES128KeyWrap \- [http:\/\/www.w3.org\/2001\/04\/xmlenc\#kw\-aes128](http://www.w3.org/2001/04/xmlenc)|128|Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheitstoken verschlüsselt.|  
|AES192KeyWrap \- [http:\/\/www.w3.org\/2001\/04\/xmlenc\#kw\-aes192](http://www.w3.org/2001/04/xmlenc)|192|Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheitstoken verschlüsselt.|  
|AES256KeyWrap \- [http:\/\/www.w3.org\/2001\/04\/xmlenc\#kw\-aes256](http://www.w3.org/2001/04/xmlenc)|256|Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheitstoken verschlüsselt.|  
|RsaV15KeyWrap \- http:\/\/www.w3.org\/2001\/04\/xmlenc\#rsa\-1\_5|1024|Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheitstoken verschlüsselt.|  
|RsaOaepKeyWrap \- [http:\/\/www.w3.org\/2001\/04\/xmlenc\#rsa\-oaep\-mgf1p](http://www.w3.org/2001/04/xmlenc)|1024|Default. Unterstützt Algorithmus zum Verschlüsseln des symmetrischen Schlüssels, der das Sicherheitstoken verschlüsselt.|  
|SHA1\-http:\/\/www.w3.org\/PICS\/DSig\/SHA1\_1\_0.html|N\/A|Von AD FS-Server verwendet in Artefakt SourceId Generation:  In diesem Szenario der STS verwendet SHA1 \(pro die Empfehlung in der SAML 2.0-Standard\) einen kurzen 160-Bit-Wert für die SourceiD Artefakt erstellen.<br /><br />Auch von der AD FS-Web-Agent verwendet \(legacykomponente aus WS2003 Zeitrahmen\) zum Identifizieren von Änderungen in einer "Letzte Aktualisierung"-Wert, damit dieser weiß, wann Informationen aus dem STS zu aktualisieren.|  
|SHA1withRSA\-<br /><br />http:\/\/www.w3.org\/PICS\/DSig\/RSA\-SHA1\_1\_0.html|N\/A|In Fällen verwendet, wenn AD FS-Server die Signatur des SAML-AuthenticationRequest überprüft hat, melden Sie sich die Artefakt-Auflösung-Anforderung oder Antwort, token erstellen\-Signaturzertifikat.<br /><br />In diesen Fällen SHA256 ist die Standardeinstellung und SHA1 wird nur verwendet, wenn der Partner \(vertrauende\) unterstützt keine SHA256 und muss SHA1.|  
  
## <a name="BKMK_13"></a>Erforderliche Berechtigungen  
Der Administrator, der die Installation und die Erstkonfiguration von AD FS durchführt, muss Domänenadministrator-Berechtigungen verfügen, in der lokalen Domäne \(in anderen Worten: die Domäne, zu der der Verbundserver hinzugefügt wird.\)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

