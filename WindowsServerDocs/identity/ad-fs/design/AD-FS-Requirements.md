---
ms.assetid: 8ce6e7c4-cf8e-4b55-980c-048fea28d50f
title: Verbundserverfarm mit SQLServer
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e23154b20dfcd642178a5ac0de17f1b6a490f91f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-requirements"></a>AD FS-Anforderungen

>Gilt für: Windows Server 2012 R2

Im folgenden sind die verschiedenen Anforderungen, denen Sie bei der Bereitstellung von AD FS entsprechen müssen:  
  
-   [Zertifikatanforderungen](AD-FS-Requirements.md#BKMK_1)  
  
-   [Hardwareanforderungen](AD-FS-Requirements.md#BKMK_2)  
  
-   [Anforderungen der Clientsoftware](AD-FS-Requirements.md#BKMK_3)  
  
-   [AD DS-Anforderungen](AD-FS-Requirements.md#BKMK_4)  
  
-   [Anforderungen an die Datenbank](AD-FS-Requirements.md#BKMK_5)  
  
-   [Anforderungen an Webbrowser](AD-FS-Requirements.md#BKMK_6)  
  
-   [Extranet-Anforderungen](AD-FS-Requirements.md#BKMK_extranet)  
  
-   [Netzwerkanforderungen](AD-FS-Requirements.md#BKMK_7)  
  
-   [Anforderungen an den Attributspeicher](AD-FS-Requirements.md#BKMK_8)  
  
-   [Anwendungsanforderungen](AD-FS-Requirements.md#BKMK_9)  
  
-   [Authentifizierungsanforderungen](AD-FS-Requirements.md#BKMK_10)  
  
-   [Arbeitsplatz beitreten Anforderungen](AD-FS-Requirements.md#BKMK_11)  
  
-   [Kryptografie-Anforderungen](AD-FS-Requirements.md#BKMK_12)  
  
-   [Erforderliche Berechtigungen](AD-FS-Requirements.md#BKMK_13)  
  
## <a name="BKMK_1"></a>Zertifikatanforderungen  
Zertifikate spielen äußerst wichtige Rolle beim Sichern der Kommunikation zwischen Verbundservern, Webanwendungsproxys, Claims\ unterstützenden Anwendungen und Webclients. Die Anforderungen für Zertifikate variieren je nach, ob Sie einen Verbundserver oder eine Proxy-Computer einrichten, wie in diesem Abschnitt beschrieben.  
  
**Verbundserverzertifikate**  
  
|||  
|-|-|  
|**Zertifikattyp**|**Anforderungen, Support und wichtige Informationen**|  
|**Secure Sockets Layer \(SSL\) Zertifikat:** Dies ist ein standard-SSL-Zertifikat, das zum Sichern der Kommunikation zwischen Verbundservern und Clients verwendet wird.|– Dieses Zertifikat muss ein öffentlich Trusted\ * X509 v3-Zertifikat.<br />-Alle Clients, die alle AD FS-Endpunkt zugreifen müssen diesem Zertifikat vertrauen. Es wird dringend empfohlen, Zertifikate verwenden, die von einer öffentlichen \(third\-party\) Zertifizierungsstelle ausgestellt werden \(CA\). Sie können eine SSL-Zertifikat mit deren Hilfe signierte erfolgreich auf dem Verbundserver in einer testumgebung verwenden. Für eine produktionsumgebung wird jedoch empfohlen, dass Sie das Zertifikat von einer öffentlichen Zertifizierungsstelle erhalten.<br />– Unterstützt Schlüsselgröße von Windows Server 2012 R2 für SSL-Zertifikate unterstützt.<br />-Wird nicht Support-Zertifikate, die CNG-Schlüssel verwenden.<br />-Wenn zusammen mit dem Arbeitsplatz Join\/Device Registration Service verwendet wird, muss der alternativen Antragstellernamen des SSL-Zertifikats für den AD FS-Dienst die Enterpriseregistration Wert enthalten, die durch das \(UPN\) Benutzerprinzipalnamen-Suffix Ihrer Organisation, z. B.: enterpriseregistration.contoso.com folgt.<br />-Zertifikate Platzhalter werden unterstützt. Wenn Sie Ihre AD FS-Farm erstellen, werden Sie aufgefordert, den Dienstnamen für den AD FS-Dienst bereitzustellen \ (z. B. **adfs.contoso.com**.<br />– Es wird dringend empfohlen, dasselbe SSL-Zertifikat für den Web Application Proxy zu verwenden. Dies ist jedoch **erforderlichen** identisch sein, bei der Unterstützung von integrierten Windows-Authentifizierung Endpunkten über das Web Application Proxy und \(default setting\) Authentifizierung für erweiterten Schutz aktiviert ist.<br />– Der Antragstellername dieses Zertifikats wird verwendet, um den Namen des Verbunddiensts für jede Instanz von AD FS darzustellen, die Sie bereitstellen. Aus diesem Grund sollten Sie einen Antragsstellernamen für alle neuen CA\ ausgestellte Zertifikate, die den Namen Ihres Unternehmens oder Ihrer Organisation gegenüber Partnern am besten widerspiegelt.<br />    Die Identität des Zertifikats muss mit den verbunddienstnamen übereinstimmen \ (z. B. fs.contoso.com\). Die Identität ist entweder einer alternativen Namen Erweiterung für den Zertifikatantragsteller des Typs dNSName oder wenn keine Subject alternative Namenseinträge vorhanden sind, der Name des Antragstellers als einem allgemeinen Namen angegeben. Mehrere Subject alternative Namenseinträge können in das Zertifikat vorhanden sein, sofern eine von ihnen den Namen des Verbunddiensts übereinstimmt.<br />-   **Wichtig:** hat dringend empfohlen, um dasselbe SSL-Zertifikat auf allen Knoten des AD FS-Farm sowie alle Web Application-Proxys in der AD FS-Farm zu verwenden.|  
|**Dienstkommunikationszertifikat:** mit diesem Zertifikat können WCF-nachrichtensicherheit für das Sichern der Kommunikation zwischen Verbundservern.|– In der Standardeinstellung wird das SSL-Zertifikat als dienstkommunikationszertifikat verwendet.  Sie haben jedoch auch die Möglichkeit, ein anderes Zertifikat als das dienstkommunikationszertifikat zu konfigurieren.<br />-   **Wichtig:** bei Verwendung der SSL-Zertifikat als das dienstkommunikationszertifikat, wenn das SSL-Zertifikat abläuft, stellen Sie sicher, das erneuerte SSL-Zertifikat als Ihre dienstkommunikationszertifikat konfigurieren. Dies geschieht nicht automatisch.<br />– Dieses Zertifikat muss von Clients von AD FS vertrauenswürdig sein, die WCF-Nachrichtensicherheit verwenden.<br />– Es wird empfohlen, dass Sie ein Serverauthentifizierungszertifikat verwenden, das von einer öffentlichen \(third\-party\) Zertifizierungsstelle ausgestellt wird \(CA\).<br />-Das dienstkommunikationszertifikat kein Zertifikat, das CNG-Schlüsseln verwendet.<br />– Dieses Zertifikat kann mit der AD FS-Verwaltungskonsole verwaltet werden.|  
|**Token\-Signaturzertifikat:** Hierbei handelt es sich um einen standardmäßigen X509 Zertifikat, das verwendet wird, für die sichere Signierung aller Token, die vom Verbundserver ausgestellt.|-Wird standardmäßig erstellt AD FS eine Zertifikat mit deren Hilfe signiert mit 2048-Bit-Schlüssel.<br />-Zertifizierungsstelle ausgestellten Zertifikate werden ebenfalls unterstützt und können mithilfe von AD FS-Verwaltungs-Snap-Ins geändert werden<br />-Zertifizierungsstelle ausgestellte Zertifikate muss gespeichert und über einen CSP-Kryptografieanbieter zugegriffen werden.<br />-Das Tokensignaturzertifikat kein Zertifikat, das CNG-Schlüsseln verwendet.<br />-AD FS erfordert keine extern Registrierung von Zertifikaten für die Tokensignatur.<br />    AD FS erneuert automatisch diese Hilfe signierte Zertifikate vor dem ablaufen, konfigurieren neue Zertifikate zunächst als sekundären Zertifikate für Partner, die sie nutzen können, und klicken Sie dann kippen zum primären automatische zertifikatrollover mit. Es wird empfohlen, dass Sie standardmäßig automatisch generierte Zertifikate zum Signieren von token verwenden.<br />    Wenn Ihre Organisation Richtlinien, die verschiedene Zertifikaten konfiguriert werden verfügt, für die Tokensignatur erfordern, können Sie die Zertifikate angeben, bei der Installation mithilfe von Powershell \ (verwenden Sie den – SigningCertificateThumbprint-Parameter, der die Install\ AdfsFarm Cmdlet\).  Nach der Installation können Sie anzeigen und Verwalten mithilfe der AD FS-Verwaltungskonsole oder Powershell-Cmdlets Set-AdfsCertificate und Get-AdfsCertificate Tokensignaturzertifikate.<br />    Extern registrierte Zertifikate zum Signieren von token verwendet werden, wird AD FS keine automatische Erneuerung oder Rollover durchgeführt.  Dieser Vorgang muss von einem Administrator ausgeführt werden.<br />    Um zertifikatrollover zuzulassen, wenn ein Zertifikat nahezu abgelaufen ist, kann eine sekundäre Tokensignaturzertifikat in AD FS konfiguriert werden. Standardmäßig werden alle Tokensignaturzertifikate in den Verbundmetadaten veröffentlicht, aber nur das primäre Token\-Signaturzertifikat wird von AD FS für das tatsächliche Signieren von Token verwendet.|  
|**Token\-Decryption\/Verschlüsselungszertifikat:** Dies ist eine standardmäßige X509 Zertifikat, d. h. zum Decrypt\/Verschlüsseln aller eingehenden Token verwendet. Es wird auch in den Verbundmetadaten veröffentlicht.|-Wird standardmäßig erstellt AD FS eine Zertifikat mit deren Hilfe signiert mit 2048-Bit-Schlüssel.<br />-Zertifizierungsstelle ausgestellten Zertifikate werden ebenfalls unterstützt und können mithilfe von AD FS-Verwaltungs-Snap-Ins geändert werden<br />-Zertifizierungsstelle ausgestellte Zertifikate muss gespeichert und über einen CSP-Kryptografieanbieter zugegriffen werden.<br />-Token\-Decryption\/Verschlüsselungszertifikats kein Zertifikat, das CNG-Schlüsseln verwendet.<br />-Standardmäßig AD FS generiert und seine eigenen, intern generiert und deren Hilfe signierte Zertifikate für die Entschlüsselung von token verwendet.  AD FS erfordert keine extern Registrierung von Zertifikaten für diesen Zweck.<br />    Darüber hinaus wird AD FS automatisch diese Hilfe signierte Zertifikate vor dem ablaufen.<br />    **Es wird empfohlen, dass Sie standardmäßig automatisch generierte Zertifikate für die Entschlüsselung von token verwenden.**<br />    Wenn Ihre Organisation Richtlinien, die verschiedene Zertifikaten konfiguriert werden, für die Entschlüsselung von token benötigen verfügt, können Sie die Zertifikate angeben, bei der Installation mithilfe von Powershell \ (verwenden Sie den – DecryptionCertificateThumbprint-Parameter, der die Install\ AdfsFarm Cmdlet\).  Nach der Installation können Sie anzeigen und Verwalten mithilfe der AD FS-Verwaltungskonsole oder Powershell-Cmdlets Set-AdfsCertificate und Get-AdfsCertificate tokenverschlüsselungszertifikate.<br />    **Wenn extern Registrierung von Zertifikaten für die Entschlüsselung von token verwendet werden, wird AD FS keine automatische Erneuerung durchgeführt. Dieser Vorgang muss von einem Administrator ausgeführt werden**.<br />– Das AD FS-Dienstkonto benötigen Zugriff auf das Token\-Signaturzertifikat den privaten Schlüssel im persönlichen Speicher des lokalen Computers. Dies wird von Setup durchgeführt. Sie können auch AD FS-Verwaltungs-Snap-in verwenden, um diesen Zugriff sicherzustellen, dass wenn Sie das Signaturzertifikat Token\ später ändern.|  
  
> [!CAUTION]  
> Zertifikate, die zum Signieren von Token\ und Token\-Decrypting\/Verschlüsseln von verwendet werden, sind entscheidend für die Stabilität des Verbunddiensts. Kunden, die ihre eigenen Zertifikate Token\-Signierung und Token\-Decrypting\/Verschlüsselung verwalten sollten sicherstellen, dass diese Zertifikate gesichert werden und unabhängig während einer Wiederherstellungsereignis stehen.  
  
> [!NOTE]  
> In AD FS können Sie die Secure Hash Algorithm \(SHA\) Ebene ändern, die für digitale Signaturen SHA\-1 oder SHA\-256 \(more secure\) verwendet wird. AD FS unterstützt nicht die Verwendung von Zertifikaten mit anderen Hashmethoden wie MD5 \ (der Standardhashalgorithmus, der mit dem Makecert.exe Befehlszeilenoption Tool\ verwendet wird). Als bewährte Sicherheitsmethode wir empfehlen die Verwendung von SHA\-256 \ (durch Default\ festgelegt) für alle Signaturen. SHA\-1 wird nur in Szenarien empfohlen, in denen Sie mit einem Produkt interoperieren müssen, das keine Kommunikation über SHA\-256 unterstützt, beispielsweise ein-Microsoft-Produkt oder ältere Versionen von AD FS.  
  
> [!NOTE]  
> Nachdem Sie ein Zertifikat von einer Zertifizierungsstelle erhalten haben, stellen Sie sicher, dass alle Zertifikate in den persönlichen Zertifikatspeicher des lokalen Computers importiert werden. Sie können Zertifikate in den persönlichen Speicher mit dem Zertifikate-MMC-Snap-in importieren.  
  
## <a name="BKMK_2"></a>Hardwareanforderungen  
Die folgenden Mindest- und empfohlenen hardwareanforderungen gelten für die AD FS-Verbundservern in Windows Server 2012 R2:  
  
||||  
|-|-|-|  
|**Die Hardware**|**Mindestanforderung**|**Empfehlung**|  
|CPU-Geschwindigkeit|Die 64-Bit-Prozessor 1,4 GHz|Quad\-Core, 2 GHz|  
|RAM|512 MB|4GB|  
|Speicherplatz|32GB|100GB|  
  
## <a name="BKMK_3"></a>Anforderungen der Clientsoftware  
Die folgenden AD FS-Anforderungen sind für die Serverfunktionen, die in das Betriebssystem Windows Server® 2012 R2 integriert ist:  
  
-   Für den Extranetzugriff, müssen Sie die Webanwendungsproxy-Rollendienst bereitstellen \ - Teil der Windows Server® 2012 R2-RAS-Serverrolle. In früheren Versionen von einem Verbundserverproxy werden mit AD FS unter Windows Server® 2012 R2 nicht unterstützt.  
  
-   Verbundserver und den Webanwendungsproxy-Rollendienst können auf demselben Computer installiert werden.  
  
## <a name="BKMK_4"></a>AD DS-Anforderungen  
**Anforderungen an den Domänencontroller**  
  
Domänencontroller in Domänen für alle Benutzer und der Domäne, die die AD FS-Server hinzugefügt werden, müssen WindowsServer 2008 oder höher ausgeführt werden.  
  
> [!NOTE]  
> Unterstützung für Umgebungen mit Windows Server 2003-Domänencontrollern endet nach der erweiterte Support Ende Datum für Windows Server 2003. Kunden werden dringend empfohlen, die Domänencontroller so bald wie möglich zu aktualisieren. Besuchen Sie [auf dieser Seite](https://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows+Server+2003&Filter=FilterNO) Weitere Informationen zur Microsoft Support Lifecycle. Für Probleme aufgetreten sind, die speziell für Windows Server 2003 Domain Controller-Umgebungen, Updates nur für Sicherheitsprobleme ausgegeben werden und ob ein Update vor dem Ablauf des erweiterten Support für Windows Server 2003 ausgestellt werden kann.  
  
**Domänenanforderungen Functional\-Ebene**  
  
Alle Domänen mit Benutzerkonten und der Domäne an, die die AD FS-Server hinzugefügt werden, müssen auf die Domänenfunktionsebene von Windows Server2003 oder höher ausgeführt werden.  
  
Die meisten AD FS-Funktionen erfordern keine AD DS Functional\-Ebene geändert werden, damit Sie erfolgreich ausgeführt werden. Ist jedoch Windows Server 2008-Domänenfunktionsebene oder höher erforderlich, damit die Clientzertifikatauthentifizierung erfolgreich betrieben werden kann, wenn das Zertifikat explizit einem Benutzerkonto in AD DS zugeordnet ist.  
  
**Schema-Anforderungen**  
  
-   AD FS erfordert keine Änderungen oder Modifikationen, die Functional\ Ebene in AD DS.  
  
-   Um Arbeitsplatzbeitritt Funktionen zu verwenden, muss das Schema der Gesamtstruktur, der mit AD FS-Server verbunden sind, Windows Server 2012 R2 festgelegt werden.  
  
**Dienstkontenanforderungen**  
  
-   Standard-Dienstkonto kann als ein Dienstkonto für AD FS verwendet werden. Gruppe von verwalteten Dienstkonten werden ebenfalls unterstützt. Dies erfordert, dass mindestens ein Domänencontroller \ (es wird empfohlen, dass Sie zwei bereitstellen oder More\), die WindowsServer 2012 oder höher ausgeführt wird.  
  
-   Kerberos-Authentifizierung zwischen Domäne\ eingebundenen Clients und AD FS die "HOST\ / < Adfs\_service\_name >' muss als einen SPN für das Dienstkonto registriert werden. Standardmäßig wird das Konfigurieren von AD FS beim Erstellen einer neuen AD FS-Farm, verfügt es über ausreichende Berechtigungen zum Ausführen dieses Vorgangs.  
  
-   Der AD FS-Dienstkonto muss in jeder Domäne vertrauenswürdig sein, das Authentifizieren von Benutzern mit dem AD FS-Dienst enthält.  
  
**Domänenanforderungen**  
  
-   Alle AD FS-Server muss zu einer AD DS-Domäne angehören.  
  
-   Alle AD FS-Server in einer Farm müssen in einer einzelnen Domäne bereitgestellt werden.  
  
-   Die Domäne, der mit der AD FS-Server verbunden sind, muss jede Domäne des Benutzerkontos vertrauen, die Benutzer authentifiziert sich gegenüber des AD FS-Diensts enthält.  
  
**Anforderungen des Multi-Gesamtstruktur**  
  
-   Jede Domäne des Benutzerkontos oder der Gesamtstruktur, die Benutzer authentifiziert sich gegenüber des AD FS-Diensts enthält, muss die Domäne, der die AD FS-Server angehören vertrauen.  
  
-   Der AD FS-Dienstkonto muss in jeder Domäne vertrauenswürdig sein, das Authentifizieren von Benutzern mit dem AD FS-Dienst enthält.  
  
## <a name="BKMK_5"></a>Anforderungen an die Datenbank  
Im folgenden sind die Anforderungen und Einschränkungen basierend auf den Konfigurationsspeicher:  
  
**INTERNE WINDOWS-DATENBANK**  
  
-   Ein Windows-datenbankfarm darf maximal 30 Verbundserver, besitzen Sie bis zu 100 Vertrauensstellungen vertrauenden Seite.  
  
-   Artefakt Auflösung Profil in SAML 2.0 wird in der Konfigurationsdatenbank WID nicht unterstützt.  Erkennung von Tokenwiederholungen Token wird in der Konfigurationsdatenbank WID nicht unterstützt. Diese Funktion wird nur dann nur in Szenarien verwendet, in dem AD FS als Verbundserverproxy Anbieter fungiert und Speicherressourcen Sicherheitstoken von externen Anspruchsanbietern.  
  
-   Bereitstellen von AD FS-Server in unterschiedlichen Daten Kostenstellen für Failover oder geografischen Lastenausgleich wird unterstützt, als die Anzahl der Server nicht mehr als 30 umfasst.  
  
Die folgende Tabelle enthält eine Zusammenfassung für die Verwendung einer Windows-datenbankfarm.  Verwenden Sie, um die Planung der Implementierung.  
  
||||  
|-|-|-|  
||1 \-100 RP-Vertrauensstellungen|Mehr als 100 RP-Vertrauensstellungen|  
|1 \-30-AD FS-Knoten|Interne Windows-Datenbank unterstützt|Nicht unterstützt, mit WID \-SQL erforderlich|  
|Mehr als 30 AD FS-Knoten|Nicht unterstützt, mit WID \-SQL erforderlich|Nicht unterstützt, mit WID \-SQL erforderlich|  
  
**SqlServer**  
  
Für AD FS unter Windows Server 2012 R2 können Sie SQLServer 2008 und höher verwenden.  
  
## <a name="BKMK_6"></a>Anforderungen an Webbrowser  
Wenn AD FS-Authentifizierung über einen Browser oder ein Webbrowser-Steuerelement ausgeführt wird, muss Ihren Browser die folgenden Anforderungen erfüllen:  
  
-   JavaScript muss aktiviert sein  
  
-   Cookies müssen eingeschaltet sein  
  
-   Server Name Indication \(SNI\) muss unterstützt werden  
  
-   Für die Benutzer Zertifikat & Gerät Zertifikatauthentifizierung \ (Arbeitsplatz beitreten Functionality\), muss der Browserunterstützung SSL-Clientzertifikatauthentifizierung  
  
Mehrere Schlüssel Browsern und Plattformen unterzogen Validierung zum Rendern und Funktionen, die Details unten aufgeführt sind. Browser und Geräte, die in dieser Tabelle nicht abgedeckt werden weiterhin unterstützt, wenn sie die oben aufgeführten Anforderungen erfüllen:  
  
|||  
|-|-|  
|**Browser**|**Plattformen**|  
|IE 10.0|Windows 7, Windows 8.1, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2|  
|IE 11.0|Windows7, Windows 8.1, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2|  
|Windows-Webauthentifizierungsbroker|Windows 8.1|  
|Firefox \[v21\]|Windows 7, Windows 8.1|  
|Safari \[v7\]|iOS 6, Mac OS\ X 10.7|  
|Chrome \[v27\]|Windows 7, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, Mac OS\-X 10.7|  
  
> [!IMPORTANT]  
> Bekanntes Problem \-Firefox: Arbeitsplatzbeitritt Funktionen, die das Gerät mit Gerätezertifikat identifiziert funktioniert nicht auf Windows-Plattformen. Firefox unterstützt derzeit nicht funktionierende SSL-Zertifikat Clientauthentifizierung mithilfe von Zertifikaten, die für den Zertifikatspeicher des Benutzers auf Windows-Clients bereitgestellt.  
  
**Cookies**  
  
AD FS erstellt Session\-basierte und beständige Cookies, die auf Clientcomputern Standardparameter in bereitstellen, Standardparameter horizontaler, einzelne Standardparameter auf \(SSO\) und andere Funktionen gespeichert werden müssen. Daher muss der Clientbrowser konfiguriert werden, um Cookies zu akzeptieren. Cookies, die für die Authentifizierung verwendet werden, sind immer Secure Hypertext Transfer Protocol-\(HTTPS\) Sitzungscookies, die für den Ursprungsserver geschrieben werden. Wenn der Clientbrowser nicht konfiguriert ist, um diese Cookies zulassen, können nicht AD FS ordnungsgemäß ausgeführt. Beständige Cookies werden verwendet, um die Benutzerauswahl des Anspruchsanbieters beizubehalten. Sie können sie eine Einstellung in der Konfigurationsdatei für die AD FS Standardparameter in Seiten mit deaktivieren. Unterstützung für TLS\/SSL ist aus Gründen der Sicherheit erforderlich.  
  
## <a name="BKMK_extranet"></a>Extranet-Anforderungen  
Um extranet-Zugriff auf die AD FS-Dienst bieten zu können, müssen Sie die Webanwendungsproxy-Rollendienst der Rolle des extranet sichtbare die Authentifizierungsanfragen Proxys auf sichere Weise mit dem AD FS-Dienst bereitstellen. Dies bietet Isolierung von der AD FS-Endpunkte sowie alle Sicherheitsschlüssel Isolation \ (z. B. token signierenden Certificates\) von Anforderungen, die aus dem Internet stammen. Darüber hinaus wird die Verwendung der the Web Application Proxy von Features wie weichen Extranet Kontosperre erfordern. Weitere Informationen zum Webanwendungsproxy finden Sie unter [Web Application Proxy](https://technet.microsoft.com/library/dn584107.aspx).  
  
Wenn Sie einen Proxy Third\ von Drittanbietern für extranet-Zugriff verwenden möchten, muss dieser Third\ Party-Proxy des Protokolls in definierten unterstützen [http:///\/download.microsoft.com\/download\/9\/5\/E\/95EF66AF\-9026\-4BB0\-A41D\-A4F81802D92C\/%5bMS\-ADFSPIP%5d.pdf](https://download.microsoft.com/download/9/5/E/95EF66AF-9026-4BB0-A41D-A4F81802D92C/%5bMS-ADFSPIP%5d.pdf).  
  
## <a name="BKMK_7"></a>Netzwerkanforderungen  
Konfigurieren entsprechend der folgenden Netzwerkdienste ist wichtig für die erfolgreiche Bereitstellung von AD FS in Ihrer Organisation:  
  
**Konfigurieren von Firewalls des Unternehmens**  
  
Firewall zwischen dem Web Application Proxy und die Verbundserverfarm und die Firewall zwischen den Clients und dem Web Application Proxy müssen TCP-Port 443 aktiviert haben eingehende.  
  
Darüber hinaus, wenn Clientbenutzer Authentifizierung Zertifikat \ (ClientTLS-Authentifizierung mithilfe von X509 Benutzer Certificates\) ist erforderlich, AD FS unter Windows Server 2012 R2 muss TCP-Port 49443 aktiviert werden in der Firewall zwischen den Clients und dem Web Application Proxy eingehende. Dies ist nicht in der Firewall zwischen the Web Application Proxy und die Verbundserverproxy-Server\ erforderlich).  
  
**Konfigurieren von DNS**  
  
-   Für den Intranetzugriff, alle Clients, die Zugriff auf AD FS-Dienst in der internen Unternehmensnetzwerk \(intranet\) müssen aufgelöst werden können der AD FS-Dienstname \ (bereitgestellt durch die SSL-Certificate\-Name) dem Lastenausgleichsmodul für die AD FS-Server oder AD FS-Server.  
  
-   Für den Extranetzugriff, alle Clients, die Zugriff auf AD FS-Dienst von außerhalb der Unternehmensnetzwerk \(extranet\/internet\) müssen aufgelöst werden können der AD FS-Dienstname \ (bereitgestellt durch die SSL-Certificate\-Name) dem Lastenausgleichsmodul für die Web Application Proxy Server oder den Webanwendungsproxy-Server.  
  
-   Für extranet-Zugriff für eine ordnungsgemäße Funktion, jede Web Application Proxy Server in der DMZ muss aufgelöst werden können AD FS-Dienstnamen \ (bereitgestellt durch die SSL-Certificate\-Name) dem Lastenausgleichsmodul für die AD FS-Server oder AD FS-Server. Dies kann mit einem anderen DNS-Server im DMZ-Netzwerk oder mithilfe der Hostdatei lokaler Server-Auflösung ändern erreicht werden.  
  
-   Für die integrierte Windows-Authentifizierung innerhalb des Netzwerks und außerhalb des Netzwerks für einen Teil der Endpunkte, die über das Web Application Proxy verfügbar gemacht werden können müssen Sie einen A-Eintrag \(not CNAME\) verwenden, um auf die Lastenausgleiche zu verweisen.  
  
Informationen zum Konfigurieren von Unternehmens-DNS für den Verbunddienst und Device Registration Service, finden Sie unter [Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS](https://technet.microsoft.com/library/dn486786.aspx).  
  
Informationen zur Konfiguration von Unternehmens-DNS für Web-App-Proxys finden Sie im Abschnitt "Konfigurieren von DNS" in [Schritt 1: Konfigurieren der Infrastruktur für den Webanwendungsproxy](https://technet.microsoft.com/library/dn383644.aspx).  
  
Informationen zur Vorgehensweise beim Konfigurieren einer Cluster-IP-Adresse oder FQDN mit NLB-Clusters finden Sie unter Angeben der Clusterparameter am [http:///\/go.microsoft.com\/fwlink\/? LinkId\ = 75282](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
## <a name="BKMK_8"></a>Anforderungen an den Attributspeicher  
AD FS muss mindestens ein Attributspeicher für die Authentifizierung von Benutzern und das Extrahieren von Sicherheitsansprüchen für diese Benutzer verwendet werden. Eine Liste der Attribute gespeichert werden, dass AD FS unterstützt, finden Sie unter [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
> [!NOTE]  
> AD FS erstellt standardmäßig automatisch einen Attributspeicher "Active Directory". Anforderungen an den Attributspeicher, hängt davon ab, ob Ihre Organisation als Kontopartner fungiert \ (hosting der Verbund Ordner %%amp;quot;Benutzer\) oder den Ressourcenpartner \ (hosting der Verbund Application\).  
  
**LDAP-Attributspeicher**  
  
Bei der Arbeit mit anderen Lightweight Directory Access Protocol \ \-based-Attributspeicher (LDAP\), Sie müssen eine Verbindung herstellen, einen LDAP-Server, die die integrierte Windows-Authentifizierung unterstützt. Die LDAP-Verbindungszeichenfolge muss außerdem im Format einer LDAP-URL geschrieben werden, wie in RFC 2255 beschrieben.  
  
Außerdem ist es erforderlich, dass das Dienstkonto für den AD FS-Dienst über die Berechtigung zum Abrufen der Benutzerinformationen aus dem LDAP-Attributspeicher verfügt.  
  
**SQL Server-Attributspeichern**  
  
Für AD FS unter Windows Server 2012 R2 erfolgreich betrieben werden kann müssen auf Computern, die den SQL Server-Attributspeicher hosten entweder Microsoft SQLServer 2008 oder höher ausgeführt werden. Wenn Sie mit SQL\-basierten attributspeichern arbeiten, müssen Sie außerdem eine Verbindungszeichenfolge konfigurieren.  
  
**Benutzerdefinierte Attributspeicher**  
  
Entwickeln Sie benutzerdefinierte Attributspeicher, um erweiterte Szenarien zu ermöglichen.  
  
-   Die für richtliniensprache, die in AD FS integriert ist, kann benutzerdefinierte Attributspeicher verweisen, so, dass eines der folgenden Szenarien verbessert werden kann:  
  
    -   Erstellen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Ergänzen von Ansprüchen für einen lokal authentifizierten Benutzer  
  
    -   Autorisieren eines Benutzers zum Abrufen eines token  
  
    -   Autorisieren eines Diensts zum Abrufen eines Token zum Verhalten eines Benutzers  
  
    -   Ausstellen von zusätzlichen Daten in Sicherheitstoken, die von AD FS für vertrauende Seiten ausgegeben.  
  
-   Alle benutzerdefinierten Attributspeicher müssen auf .NET 4.0 oder höher erstellt werden.  
  
Wenn Sie mit einem benutzerdefinierten Attributspeicher arbeiten, Sie auch möglicherweise eine Verbindungszeichenfolge konfigurieren. In diesem Fall können Sie einen benutzerdefinierten Code Ihrer Wahl eingeben, die eine Verbindung mit Ihrem benutzerdefinierten Attributspeicher ermöglicht. Die Verbindungszeichenfolge in dieser Situation ist ein Satz von Tokentypen-Wert-Paaren, die vom Entwickler des benutzerdefinierten Attributspeichers Implementierung interpretiert werden. Weitere Informationen zum Entwickeln und Verwenden von benutzerdefinierten attributspeichern finden Sie unter [Übersicht über Attributspeicher](https://go.microsoft.com/fwlink/?LinkId=190782).  
  
## <a name="BKMK_9"></a>Anwendungsanforderungen  
AD FS unterstützt Claims\-fähige Anwendungen, die die folgenden Protokolle verwenden:  
  
-   WS-Federation  
  
-   WS-Trust  
  
-   Mithilfe von Profilen für IDPLite, SPLite und eGov1.5 SAML 2.0-Protokoll.  
  
-   OAuth 2.0 Authorization Grant-Profil  
  
AD FS unterstützt auch Authentifizierung und Autorisierung für-Claims\-fähige Anwendungen, die von the Web Application Proxy unterstützt werden.  
  
## <a name="BKMK_10"></a>Authentifizierungsanforderungen  
**AD DS Authentifizierung \(Primary Authentication\)**  
  
Für den Intranetzugriff werden die folgenden Standardauthentifizierungsmethoden für AD DS unterstützt:  
  
-   Integrierte Windows-Authentifizierung mit Negotiate für Kerberos und NTLM  
  
-   Formularauthentifizierung mit Username\-Kennwörter  
  
-   Zertifikatbasierte Authentifizierung mithilfe von Zertifikaten, die Benutzerkonten in AD DS zugeordnet  
  
Für extranet-Zugriff werden die folgenden Mechanismen unterstützt:  
  
-   Formularauthentifizierung mit Username\-Kennwörter  
  
-   Zertifikatbasierte Authentifizierung mithilfe von Zertifikaten, die Benutzerkonten in AD DS zugeordnet sind  
  
-   Integrierte Windows-Authentifizierung mit Negotiate \(NTLM only\) für WS-Trust-Endpunkte, die integrierte Windows-Authentifizierung zu akzeptieren.  
  
Die zertifikatbasierte Authentifizierung:  
  
-   Erweitert für Smartcards, die Pin geschützt werden können.  
  
-   Die GUI für den Benutzer zur Eingabe ihrer Pin wird nicht von AD FS bereitgestellt und ist erforderlich, um das Clientbetriebssystem gehören, die angezeigt wird, wenn der Client TLS verwenden.  
  
-   Der Leser und der Kryptografiedienstanbieter \(CSP\) für die Smartcard müssen arbeiten, auf dem Computer, auf dem sich der Browser befindet.  
  
-   Das Smartcardzertifikat muss an einen vertrauenswürdigen Stamm auf dem AD FS-Server und Web Application Proxy Server gebunden sein.  
  
-   Das Zertifikat muss dem Benutzerkonto in AD DS mit einer der folgenden Methoden zugeordnet:  
  
    -   Der Antragstellername des Zertifikats entspricht dem definierten LDAP-Namen eines Benutzerkontos in AD DS.  
  
    -   Die Erweiterung des Zertifikats Betreff alternatnamen verfügt über den Benutzerprinzipalnamen eines Benutzerkontos in AD DS \(UPN\) Namen.  
  
Für die nahtlose integrierte Windows-Authentifizierung mithilfe von Kerberos im Intranet,  
  
-   Es ist ein Teil der vertrauenswürdigen Sites oder lokale Intranetsites erforderlich.  
  
-   Darüber hinaus die HOST\ / < Adfs\_service\_name > SPN muss festgelegt werden für das Dienstkonto, das die AD FS-Farm ausgeführt wird, auf.  
  
**Multithread-Faktor-Authentifizierung**  
  
AD FS unterstützt zusätzlichen Authentifizierung \ (neben der primären Authentifizierung von AD DS\ unterstützt) mithilfe eines Anbieters Modell, bei dem Vendors\-Kunden ihre eigenen Multithread-Factor Authentication-Adapter erstellen können, die ein Administrator registrieren und bei der Anmeldung verwenden kann.  
  
Jeder MFA-Adapter muss .NET 4.5 integriert werden.  
  
Weitere Informationen zu MFA, finden Sie unter [Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md).  
  
**Geräteauthentifizierung**  
  
AD FS unterstützt Geräteauthentifizierung mithilfe von Zertifikaten, die von der Device Registration Service bereitgestellt werden, während der Vorgang der einen Endbenutzer Arbeitsplatz beitreten zu ihrem Gerät.  
  
## <a name="BKMK_11"></a>Arbeitsplatz beitreten Anforderungen  
Endbenutzer können arbeitsplatzbeitritt ihre Geräte mit AD FS. Dies wird durch den Geräteregistrierungsdienst in AD FS unterstützt. Daher erhalten Endbenutzer den zusätzlichen Vorteil von SSO für die Anwendungen von AD FS unterstützt werden. Darüber hinaus können Administratoren verwalten von Risiken durch Einschränken des Zugriffs auf Anwendungen nur auf Geräten, die mit dem Arbeitsplatz verbundene für die Organisation wurden. Im folgenden finden Sie die folgenden Anforderungen für dieses Szenario zu ermöglichen.  
  
-   AD FS unterstützt arbeitsplatzbeitritt für Windows 8.1 und iOS-Geräte 5\ +  
  
-   Um Arbeitsplatzbeitritt Funktionen zu verwenden, muss das Schema der Gesamtstruktur, der mit AD FS-Server verbunden sind Windows Server 2012 R2.  
  
-   Der alternative Antragstellername des SSL-Zertifikats für AD FS-Dienst muss der Wert Enterpriseregistration enthalten, der durch das \(UPN\) Benutzerprinzipalnamen-Suffix Ihrer Organisation, z. B. enterpriseregistration.corp.contoso.com folgt.  
  
## <a name="BKMK_12"></a>Kryptografie-Anforderungen  
Die folgende Tabelle enthält zusätzliche Kryptografie Supportinformationen auf dem AD FS Tokensignaturzertifikat, tokenentschlüsselungs-Encryption\ Funktionen:  
  
||||  
|-|-|-|  
|**Algorithmus**|**Schlüssellängen**|**Protocols\/Applications\/Kommentare**|  
|TripleDES – Standard 192 \ (unterstützte 192 – 256\) \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#tripledes\-cbc](http://www.w3.org/2001/04/xmlenc)|>\= 192|Unterstützte Verschlüsselungsalgorithmus zum Verschlüsseln von Sicherheitstoken.|  
|Aes128 \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes128\-cbc|128|Unterstützte Verschlüsselungsalgorithmus zum Verschlüsseln von Sicherheitstoken.|  
|Aes192. \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes192\-cbc|192|Unterstützte Verschlüsselungsalgorithmus zum Verschlüsseln von Sicherheitstoken.|  
|AES256 \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#aes256\-cbc](http://www.w3.org/2001/04/xmlenc)|256|**Standard-**. Unterstützte Verschlüsselungsalgorithmus zum Verschlüsseln von Sicherheitstoken.|  
|TripleDESKeyWrap \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-tripledes|Alle Schlüssel Größen von .NET 4.0\+ unterstützt|Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der ein Sicherheitstoken verschlüsselt.|  
|AES128KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes128](http://www.w3.org/2001/04/xmlenc)|128|Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der das Sicherheitstoken verschlüsselt.|  
|AES192KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes192](http://www.w3.org/2001/04/xmlenc)|192|Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der das Sicherheitstoken verschlüsselt.|  
|AES256KeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#kw\-aes256](http://www.w3.org/2001/04/xmlenc)|256|Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der das Sicherheitstoken verschlüsselt.|  
|RsaV15KeyWrap \-http:///\/ www.w3.org \/2001\/04\/xmlenc\#rsa\-1\_5|1024|Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der das Sicherheitstoken verschlüsselt.|  
|RsaOaepKeyWrap \- [http:///\/ www.w3.org \/2001\/04\/xmlenc\#rsa\-oaep\-mgf1p](http://www.w3.org/2001/04/xmlenc)|1024|Standardmäßig verwendet. Unterstützt Algorithmus zum Verschlüsseln von den symmetrischen Schlüssel, der das Sicherheitstoken verschlüsselt.|  
|SHA1\ http: / / / \ / www.w3.org \/PICS\/DSig\/SHA1\_1\_0.html|N\/A|Von AD FS-Server in Artefakt SourceId Generation verwendet: In diesem Szenario verwendet der STS SHA1 \ (gemäß der Empfehlung in das SAML 2.0-Standard\) einen kurzen 160-Bit-Wert für die Artefakt SourceiD erstellen.<br /><br />Auch von der AD FS-Web-Agent verwendet \ (legacy-Komponente von WS2003 Timeframe\) zum Identifizieren von Änderungen in einem Zeitpunkt "Letzte Aktualisierung" Wert, wann Informationen von den STS aktualisiert werden sollen.|  
|SHA1withRSA\-<br /><br />http:///\/ www.w3.org \/PICS\/DSig\/RSA\-SHA1\_1\_0.html|N\/A|Melden Sie in Fällen verwendet, wenn AD FS-Server die Signatur des SAML-AuthenticationRequest überprüft die Anforderung zur Auflösung Artefakt oder die Antwort, erstellen Sie Token\-Signaturzertifikat zu.<br /><br />In diesen Fällen SHA256 ist die Standardeinstellung und SHA1 wird nur verwendet, wenn der Partner \(relying party\) SHA256 unterstützt keine und SHA1 verwenden müssen.|  
  
## <a name="BKMK_13"></a>Erforderliche Berechtigungen  
Der Administrator, der die Installation und die Erstkonfiguration von AD FS durchführt, muss Domänenadministrator-Berechtigungen verfügen, in der lokalen Domäne \ (also die Domäne, der der Verbundserver hinzugefügt wird. \)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Entwurfshandbuch in Windows Server2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

